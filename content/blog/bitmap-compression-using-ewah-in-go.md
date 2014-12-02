+++
date = "2013-09-15T23:08:22-08:00"
title = "Bitmap Compression using EWAH in Go"
categories = [ "code", "golang", "bitmap" ]

+++

[comments/suggestions](https://news.ycombinator.com/item?id=6392197)

### tl;dr

* If you are interested in database bitmap index, then it's definitely worth learning more about bitmap compression.
* EWAH is a very interesting way of compressing bitmaps and this article talks about my port of it to Go.
* Sorry I think you should read the rest of the article. :)

### The Real Deal

For "Go Learn" project #5, I've decided to continue implementing bit-related data structures. This time I decided to port a bitmap (not image) compression data structure to Go. Unlike bloom filters, which had quite a few implementations, I couldn't really find any compressed bitmap implementations in Go. Most of them are in C/C++ or Java. (For previous projects please see previous blog posts.)

Btw, if you have any suggestions on what project I should do next, feel free to drop me a comment.

### Bitmaps

Bitmap compression is often used for database [bitmap indexing](http://en.wikipedia.org/wiki/Bitmap_index). To quote Wikipedia again:

> A bitmap index is a special kind of database index that uses bitmaps. [...] 

> Bitmap indexes use bit arrays (commonly called bitmaps) and answer queries by performing bitwise logical operations on these bitmaps. Bitmap indexes have a significant space and performance advantage over other structures for query of such data. Their drawback is they are less efficient than the traditional B-tree indexes for columns whose data is frequently updated: consequently, they are more often employed in read-only systems that are specialized for fast query - e.g., data warehouses, and generally unsuitable for online transaction processing applications. [...] 

> Some researchers argue that Bitmap indexes are also useful for moderate or even high-cardinality data (e.g., unique-valued data) which is accessed in a read-only manner, and queries access multiple bitmap-indexed columns using the AND, OR or XOR operators extensively.

There are quite a few approaches to bitmap compression. You will find most of the work listed in the wikipedia page. The two I found to be most interesting are [CONCISE](http://ricerca.mat.uniroma3.it/users/colanton/docs/concise.pdf) and [Enhanced Word-Aligned Hybrid (EWAH)](https://code.google.com/p/javaewah/). After reading throught both papers and looking at their Java implementations, I decided to start with EWAH. There's no primary reason for starting with EWAH first. But Daniel Lemire's comment intrigued me, "Out of the bitmap formats that I have often tested, Concise is the most concise, but JavaEWAH is often faster. So there is a trade-off." I wanted to see how fast the Go implementation can be so I figure I start with EWAH. I may still port CONCISE later. (Note: I am not the best Go programmer nor do I claim that my code is the most performant. This is a learning project so there will definitely be room for improvement.)

### EWAH

Enhanced Word-Aligned Hybrid (EWAH) is a bitmap compression algorithm created by Daniel Lemire, Owen Kaser, and Kamel Aouiche. ([paper](http://arxiv.org/pdf/0901.3751v4.pdf))

EWAH uses a method called [Run-Length Encoding](http://en.wikipedia.org/wiki/Run-length_encoding) to perform compression. RLE is extremely useful for dataset that tend to have long blocks of the same data. In the case of database bitmap indices, there maybe long blocks of 1's or 0's, depending on the sparsity of the data. In cases where sparsity is low, compression can be extremely high. We will show some data points on this later.

EWAH uses two types of words where the first type is a 64-bit verbatim word. The second type of word is a marker word: the first bit indicates which clean word will follow, half the bits (32 bits) are used to store the number of clean words, and the rest of the bits (31 bits) are used to store the number of dirty words following the clean words. EWAH bitmaps begin with a marker word.

Clean (empty) words are either all 0's or all 1's. Dirty (literal) words are verbatim words that have 1's and 0's. Blocks of clean words can be compressed using RLE. Dirty words cannot be compressed so they are represented vertatim.

```
3210987654321098765432109876543210987654321098765432109876543210
0000000000000000000000000000010000000000000000000000000000000100
0000000000000000000001000000000000000000000000000000000000000001
0000000000000000000000000000000000000000001000000000000000000100
```

For example, the above bits show a marker word. Bits go from right to left. So the first bit being 0 means the clean/empty words all have their bits as 0. The next 32 bits indicate the number of clean words this is encoding. "10" in this case means this marker word encodes 2 clean words that are all 0's. 

The final 31 bits (starting at position 33 from the right) indicates the number of literal words that will follow this marker word. In thise case, there are also 2 dirty (literal) words that follow the marker word.

As you can see, the overall bitmap contains 3 64-bit words. However, it encodes 4 64-bit words. So there's a space saving of 25%.

For more detailed information please read the paper. It's definitely worth the read if you are trying to understand bitmap compression.

There are a few caveats to EWAH:

1. There is no random access to any single bit, unlike a regular bit array. To access a random bit, you need to walk through the whole bitmap and find the word that contains the bit.
1. You cannot set a bit that's earlier than the last set bit. For example, if you have already set bit 100, you can not go back and set bit 99.

Technically you can solve both of these problems, but the cost of doing such operations will be extremely high.

### Go Port

Most of my nights and weekends over the past couple of weeks have gone into the porting of JavaEWAH to Go. There's also a C++ version of EWAH which I've also gone through. Code structure wise it's very similar to the Java version. You can find the [Go EWAH port on Github](https://github.com/reducedb/bitmap).

This is one of the more inovled ports I've ported to Go because it involved quite a few more classes and also the logic required much more understanding. With previous projects like [Cityhash](https://github.com/reducedb/cityhash) and [Bloom Filter](https://github.com/reducedb/bloom), I can get away with either translating directly without complete understanding (in the case of Cityhash) or the logic is fairly simple and can be coded up pretty easily (bloom filters.) 

I wanted to be able to implement multiple bitmap compression algorithms down the road, so I started with a simple [bitmap interface](https://github.com/reducedb/bitmap/blob/master/bitmap.go). It contains most the basic bit operations such as Set, Get, And, Not, Or, Xor, AndNot, Cardinality, etc. I then went through the Java source code and ported everything that's required to implement these functions.

What this means is that my Go version is NOT a complete port of JavaEWAH. There are some java classes and methods I chose not to port as they weren't required for satisfying the bit operations.

Initially I ported the classes over exactly as Java version had them. This included classes such as RunningLengthWord, BufferedRunningLengthWord, EWAHIterator, IteratingBufferedRunningLengthWord. These classes formed the bases for iterating over the bitmap and they are heavily used throughout the implementation for all the bit operations. Iterating over a bitmap usually involves multiple layers of nested iterators.

What I found is that in my Go port using this same approach was running fairly slow as there are multiple nested iterators. (Results later.) Now to be completely honest and fair, this does not mean the Java version is also slow. It's just the __My Go version__ is slow. As I have learned over the past few projects, there are always ways to make things faster. I tried to apply what I've learned in previous projects in these new projects but it certainly doesn't mean I always succeed.

#### Cursors

After porting the Java version to Go directly, I learned a ton about the structure of the algorithm and how the different bit operations are performed. Given that my Go version was running fairly slow, I decided to try a different approach. Instead of the nested iterator approach, I implemented a Cursor structure that basically collapsed RunningLengthWord, BufferedRunningLengthWord, IteratingBufferedRunningLengthWord, and EWAHIterator into a single structure. 

Whenever I need to iterate over the bitmap, I create a cursor (you can call it a iterator if you like but it's just a single layer with no nesting) and use that to keep track of where I am. Then I loop over the bitmap and perform the necessary operations.

In many cases during my benchmarks, the cursor-based performance is 2-4x faster over the previous approach.  I took great care to make sure the results of the two different implementations return exactly the same thing. You can see some of that in my tests.

#### Get

The original Java implementation did not have a Get function, which gets the bit at any random location. This is because bitmap implementation such as CONCISE and EWAH are meant to be used with bitmap indices and in most cases you don't need to check a random bit. The common use cases are to perform bit operations on two bitmaps, then find all the bits that are set.

Regardless, I wanted to have a Get function duing my testing so I can check to see the bits I set are indeed set correctly. So I did a quick Get implemention by looping over the bitmap. Daniel was gracious enough to convert my Go implementation back into Java and [incorporated it into JavaEWAH](https://github.com/lemire/javaewah/blob/master/src/main/java/com/googlecode/javaewah/EWAHCompressedBitmap.java#L1015).

However, walking the bitmap each and every time we want to check a bit is way way way too slow. In some of the use cases I am thinking about I tend to sequentially check bits. For example, I will check bits 100, 159, 302, 405, etc. The bits are almost always increasing. 

So taking a page from the [skiplist](https://github.com/reducedb/skiplist) implementation I did a few weeks back, I implemented Get with Fingers. The Finger concept is fairly simple. We basically keep a finger on the last checked word, and if the new bit to check is in or after the last checked word, we just move forward from there. If the new bit is BEFORE the current word, we restart from the beginning. The actually Get implementation keeps a getCursor as a finger to the last checked word.

The result is quite an improvement for sequential checks:

* Get with Finger and Cursor - 125 ns/op
* Get without Finger but uses Cursor - 60542 ns/op
* Get using the nested iterators approach - 822530 ns/op

### Results

The [final product](https://github.com/reducedb/bitmap) of this project is available on Github. I ran quite a few benchmarks with different bitmap density (1-sparsity) as well as running bit operations with two bitmaps of varying density. Here are some points to note.

#### Density vs Space Saving

The whole reason for bitmap compression to exist is to save space. So here are some results from that test. Probably not surprisingly, the higher the density, the lower the space savings. The charte below shows how density and space savings correlate for a bitmap that had a cardinality of 10,000.

<img src="https://docs.google.com/spreadsheet/oimg?key=0ApDLtJuUH-1rdHh2bzY1d0h3U042UXNkLUlzaENLMUE&oid=1&zx=510m225jyk7b" />

| Space Saving  | Bit Density |
|--------|-------|
| -0.62% | 50.39% |
| -0.04% | 6.46% |
| 32.68% | 0.67% |
| 91.61% | 0.07% |
| 99.15% | 0.01% |

My test data set is generated fairly uniformly. To get different density, I generate a random number between 1-N, where N is the number at the left-most column in the table. So on average the distance between bits is N/2, well, approximately. This may not be the best real-world scenario so take it with a grain of salt. But it does demonstrate how well EWAH can compress.

At the bottom, you will find the full list of bitmaps I generated for the tests. (Look at the bitmaps tab)

#### Cursor vs Nested Iterators

Another interesting benchmark I did was test the performance between the cursor-based implementation and the nested-iterators implementation. I tested the two implementations using a wide variaty of combinations, totaling 225 benchmarks per bit operation (AND, OR, XOR, ANDNOT).

<script src="https://gist.github.com/zhenjl/6577789.js"></script>

The above gist is the shell script that generates the wrappers for calling a benchmark function in Go. Btw, I love the testing package for Go as it makes it really easy for me to create tests and benchmarks. However, not having the ability to run benchmarks with different parameters without creating wrappers like these is a huge pain the butt.

The result is quite telling. The cursor-based implementation is 2-4 times faster than the nested-iterator version. See the "Performance Results" tab below.  

* AND/OR/XOR/ANDNOT 1 - This is the cursor-based implementation
* AND/OR/XOR/ANDNOT 2 - This is the nested-iterator-based implementation

#### Embedded Spreadsheet

<iframe width='800' height='500' frameborder='0' src='https://docs.google.com/spreadsheet/pub?key=0ApDLtJuUH-1rdHh2bzY1d0h3U042UXNkLUlzaENLMUE&output=html&widget=true'></iframe>


[comments/suggestions](https://news.ycombinator.com/item?id=6392197)

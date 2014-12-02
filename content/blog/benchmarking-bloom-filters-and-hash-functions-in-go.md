+++
date = "2013-09-04T00:23:22-08:00"
title = "Benchmarking Bloom Filters and Hash Functions in Go"
categories = [ "code", "golang", "bloom", "hashing" ]

+++

[discussion/comments](https://news.ycombinator.com/item?id=6329616)

Update: @bradfitz [commented](https://news.ycombinator.com/item?id=6329616) that allocating a new slice during each add/check is probably not good for performance. And he is in fact correct. After removing the allocation for each add/check and doing a single slice make during New(), the performance increased by ~27%!! Here's the gist containing the new ns/op results.

{% gist 6515577 %}

---

Another week, another "Go Learn" project. This time, in project #4, I implemented a [Go package](https://github.com/reducedb/bloom) with several bloom filters and [benchmarked](https://gist.github.com/zhenjl/6433634) them with various hash functions. (For previous projects, see [#3](http://zhen.org/blog/go-skiplist/), [#2](http://zhen.org/blog/testing-msgpack-and-bson/), [#1](https://github.com/reducedb/cityhash).)

The goal of this project, for me at least, is to implement a pure Go package that doesn't rely on wrappers to other langagues. There's already [quite a few](https://github.com/search?l=Go&q=bloom&ref=cmdform&type=Repositories) bloom filters implemented in Go. But hey, in the name of learning, why not implement another one!

### Bloom Filters

Wikipedia says,

> A Bloom filter, conceived by Burton Howard Bloom in 1970 is a space-efficient probabilistic data structure that is used to test whether an element is a member of a set. False positive matches are possible, but false negatives are not; i.e. a query returns either "inside set (may be wrong)" or "definitely not in set".

In my little project, I implemented the following three variants:

* Standard - This is the classic bloom filter as described on [Wikipedia](http://en.wikipedia.org/wiki/Bloom_filter). 
* Partitioned - This is a variant described by [these](http://www.ieee-infocom.org/2004/Papers/45_3.PDF) [papers](http://gsd.di.uminho.pt/members/cbm/ps/dbloom.pdf). Basically instead of having a single big bit array, partitioned bloom filter breaks it into *k* partitions (or slices) s.t. each partition is *m/k* size, where *m* is the total number of bits, and *k* is the number of hashes. Then each hash function is assigned to a single partition.
* Scalable - This is yet another variant described by [here](http://gsd.di.uminho.pt/members/cbm/ps/dbloom.pdf)). The idea is that the standard bloom filter requires that you know *m*, or the size of the filter a priori. This is not possible for use cases where data continue to come in without bound. So the Scalable bloom filter utilizes multiple bloom filters, each with incresing k, but decreasing *P* where *P* is the desired error probability. This bloom filter also introduces *r*, which is the error tightening ratio, and it's 0 < r < 1.

There are a ton more variants for bloom filters. You can raed all about them in [this paper](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=5&cad=rja&ved=0CE4QFjAE&url=http%3A%2F%2Fwww.tribler.org%2Ftrac%2Fraw-attachment%2Fwiki%2FJelleRoozenburg%2Fresearch_assignment_jroozenburg_20051108.pdf&ei=JHInUt6oO6GTiQK-44DYDg&usg=AFQjCNG057WVJ2m2QYPuqWzCZ0Vn4JnOug&sig2=NVlad7xGO4S_hFpMU9apGA&bvm=bv.51773540,d.cGE) and [this paper](http://www.dca.fee.unicamp.br/~chesteve/pubs/bloom-filter-ieee-survey-preprint.pdf).

### Hash Functions

To add an element, bloom filters hashes the element using *k* hashing functions, identifying *k* positions in the bit array, and setting those bits to 1. To check for an element, you essentially do the same thing (hash the element with *k* hash functions) and then check to see if all the bits at those positions are set. If all set, then most likely the element is available. If any of them are not set, then the element is definitely not avaiable. So bloom filters can have false positives, but not false negatives.

However, actually running *k* hash functions is quite expensive. So [Kirsch and Mitzenmacher](http://www.eecs.harvard.edu/~kirsch/pubs/bbbf/rsa.pdf) determined that by using a single hash function, but using the formula, *gi(x) = h1(x) + i * h2(x)*, to calculate *k* hash values, the performance is actually similar. So this is what I used here.

For the values *h1* and *h2*, we used the first 4 bytes returned from each hash function for *h1*, and second 4 bytes for *h2*. 

The following hash functions are used for this little experiement:

* FNV-64 - There's a built-in Go package for this. So that's what I used.
* CRC-64 - Again, using the built-in Go package.
* Murmur3-64 - There's no built-in package so I used [this one](https://github.com/spaolacci/murmur3).
* CityHash-64 - Again, no built-in so I am using the one [I implemented](https://github.com/reducedb/cityhash).
* MD5 - Using the built-in Go implementation.
* SHA1 - Using the built-in Go implementation.

As a side note, MD5 and SHA1 return 128 bit hash values. Since we only use the first 64 bits, we throw away the last 64 bits.

### Test Setup

The machine that ran these tests is a Macbook Air 10.8.4 1.8GHz Intel Core i5 4GB 1600MHz DDR3.

For the false positive test, I added all the words in /usr/share/dict/web2 (on my Mac) into each of the bloom filters. To check for false positives, I check for all the words in /usr/share/dict/web2a in each of the bloom filters. The two files should have completely different set of words (AFAICT).

```
  235886 /usr/share/dict/web2
   76205 /usr/share/dict/web2a
```

For each bloom filter, I ran tests using the following combinations:

```
for i in element_count[236886, 200000, 100000, 50000]
    for j in hash_functions[fnv64, crc64, murmur3-64, cityhash-64, md5, sha1]
        run test with hash_functions[j] and element_count[i]
    end
end
```

Element count in this is the initial size I set for the bloom filter. The bit array size, *m*, and number of hash values, *k*, are then calculated from there. I also set *P* (error probability) to 0.001 (0.1%) and *p* (fill ratio, or how full should the bit array be) to 0.5. The idea for the element count is to see how the bloom filters will perform when it has a high fill ratio.

For the scalable bloom filter test, I also needed to add another dimension since it uses either standard or partitioned bloom filter internally. So

```
for i in element_count[236886, 200000, 100000, 50000]
    for j in hash_functions[fnv64, crc64, murmur3-64, cityhash-64, md5, sha1]
        for k in bloom_filter[standard, partitioned]
            run test with hash_functions[j] and element_count[i] and bloom_filter[k]
        end
    end
end
```

For the performance test, I added all the words in web2 into the bloom filters. I continue to loop through the file until b.N (Go benchmark framework) is met. So some of the words will be re-added, which should not skew our test results since the operations are the same.

You can see the tests in the [github repo](https://github.com/reducedb/bloom). Just look for all the _test.go files.

### Test Results

The following is a summary of the test results. You can also feel free to look at all the [gory details](https://gist.github.com/zhenjl/6433634).

Note: FR = Fill Ratio, FP = False Positive

For the spreadsheet embedded below, here are some observations

* The MD5 Go implementation I used maybe broken, or I am not using it correctly, or MD5 is just bad. You will see that the fill ration is VERY low, 1-6%. So the false positive rate is very high (89+%).
* The CityHash Go implementation seems very slow. Could just be my implementation (anyone want to venture some optimization?). But functionally it's correct.
* Both standard and partitioned bloom filters use the same number of bits and there's not a huge difference in fill ratio and false positive rate. (Ignoring the MD5 anomaly.)
* Predictably, as fill ratio goes up, so does the false positive rate for both standard and partitioned bloom filters.
* Scalable bloom filter uses more bits as it contines to add new base bloom filters when the estimated fill ratio reaches *P* which is set to 0.5 (50%). 
* Probably not surprisingly, Scalable bloom filter maintains a fairly low false positive rate. 
* However, you will also notice that the Scalable FP increases as the total number of base filters increase. This suggests that I may want to try a lower *r* (error tightening ratio). Currently I use 0.9, but maybe 0.8 is more appropriate.
* Overall it seems FNV is probably good enough for most scenarios. 
* Also Scalable+Standard might be a good choice for anyone doing stream data processing.

<iframe width='800' height='600' frameborder='0' src='https://docs.google.com/spreadsheet/pub?key=0ApDLtJuUH-1rdEEwZ3JwaVVTZGxBX1g1NkthSFVVTXc&single=true&gid=0&output=html&widget=true'></iframe>

This chart shows the performance (ns/op) for adding elements to the bloom filters. Overall the performance is very similar for the different bloom filter implementations. 

<img src="https://docs.google.com/spreadsheet/oimg?key=0ApDLtJuUH-1rdEEwZ3JwaVVTZGxBX1g1NkthSFVVTXc&oid=1&zx=jbizsaoepc5x" />

### Feedback

Feel free to send me any feedback via [github issues](https://github.com/reducedb/bloom/issues) or on [Hacker News](https://news.ycombinator.com/item?id=6329616).

### References

During this process I referenced and leveraged some of these other projects, so thank you all!

* Referenced 
  * [willf/bloom](https://github.com/willf/bloom) - Go package implementing Bloom filters
  * [bitly/dablooms](https://github.com/bitly/dablooms) - scaling, counting, bloom filter library
  * There's also a bunch of papers, some of which I linked above.
* Leveraged 
  * [willf/bitset](https://github.com/willf/bitset) - Go package implementing bitsets 
  * [spaolacci/murmur3](https://github.com/spaolacci/murmur3) - Native MurmurHash3 Go implementation

[discussion/comments](https://news.ycombinator.com/item?id=6329616)

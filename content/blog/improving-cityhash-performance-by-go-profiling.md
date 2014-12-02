+++
date = "2013-11-10T15:04:22-08:00"
title = "Improving Cityhash Performance by Go Profiling"
categories = [ "code", "golang", "hashing" ]

+++

Comments/Feedback on [Hacker News](https://news.ycombinator.com/item?id=6710115), [Reddit](http://www.reddit.com/r/golang/comments/1qcygc/improving_cityhash_performance_by_go_profiling/)

> 2013-11-19 Update #1: After more profiling (see _top_ output in the "After modification" section), I've found that these 3 functions, unalignedLoad64, fetch64, and uint64InExpectedOrder,  add up to quite a bit of execution time. I looked at the [original cityhash implementation](https://code.google.com/p/cityhash/source/browse/trunk/src/city.cc) and realized that the combination of these functions is basically geting a LittleEndian uint64, which we can read by doing LittleEndian.Uint64(). So I updated fetch64 to do just that. Performance increased by ~20% just because of that. Also, the bloom filter test showed that cityhash is now faster than both FNV64 and CRC64.


Another month has gone by since the last post. This month has been extremely busy at work in an extraordinary good way. We had a huge POC that went quite succesfully at a large customer site. I also got a chance to visit Lisbon, Portugal as part of this POC. So things overall went pretty well.

However, since family and work pretty much occupied most of my waking hours over the past few weeks, I haven't made much progress on the "Go Learn" projects. To keep myself going, I picked a smaller task over the weekend and decided to go back to "Go Learn Project #1", my <a href="https://github.com/reducedb/cityhash">cityhash</a> Go implementation.

### Go Learn Project #1 

When I first decided to learn Go, I struggled quite a bit to find a project that I can sink my teeth into. I am not sure if others are the same way, for me to learn a new language, I have to have something meaningful to work on. I can't just write hello world programs or follow tutorials. I can read books and articles, but I will also procrastinate for weeks if I can't find a relevant project.

Luckily, I was thinking about creating a data generator at work and wanted to write that in Go. But in order to write the data generator in Go, I first have to have a cityhash implementation in Go because our backend (C/C++) is using cityhash.

Surprisingly, I looked around but couldn't find any Go implementation of cityhash. I would have thunk that given Go and Cityhash are both from Google, some Googler would have already ported cityhash over to Go. But no such luck, or maybe I just didn't look hard enough. In any case, I decided to port cityhash over to Go. 

Porting an existing project in C over to Go has a big advantage in that I don't have to invent any new data structures or algorithms. It will allow me to focus on learning the Go syntax and the standard libraries. Many many moons ago (before I converted to the dark side) I was pretty proficient in C and reading cityhash wasn't too difficult, so porting cityhash over to Go should be relatively straightforward.

In any case, the porting process wasn't too difficult, as it turned out. Overall I was able to do that over a weekend. I was also able to port the test program (city-test.cc) over as well (vim substitution FTW) to validate that my implementation was functionally correct. 

### Performance Sucked

I had always suspected that my Go cityhash implementation wasn't great performance wise. At the time I hadn't learned how to benchmark or profile Go programs, so I didn't do a whole lot except ensuring functionally the results are correct. Also my data generator at work was working fine so I left the implementation as is.

In September, I implemented a <a href="https://github.com/reducedb/bloom">Bloom Filter package</a> which required a hash function as part of the implementation. For that package, I <a href="http://zhen.org/blog/benchmarking-bloom-filters-and-hash-functions-in-go/">tested different hash functions</a> to see how they affect the performance of the bloom filter. As you can see from those benchmarks, Cityhash is consistently 3x slower compare to the others. At the time I knew it was because of my implementation but didn't look into it further.

### Profiling Go Cityhash

Since that first project, I have learned quite a bit more about benchmarking and profiling. So this weekend I finally took time to profile the Go implementation and found some interesting results. Now Go experts probably will read this and say "of course, you had no idea what you were doing." And that would be true. I had no idea at the time. Hopefully this post will make up for it. 

If you haven't read [this blog post on Go profiling](http://blog.golang.org/profiling-go-programs), you should go read it now before continuing.

In any case, I wrote a <a href="https://gist.github.com/zhenjl/7405913">short program</a> to test cityhash with a big file. This way it can collect enough samples to tell me where the bottleneck is.

The original implementation took 45 seconds to hash a 1.1G file. Below is the cpu profile output. 

```
duration = 45401991546ns
Total: 4295 samples
    2766  64.4%  64.4%     2766  64.4% runtime.memmove
     374   8.7%  73.1%      463  10.8% sweepspan
     259   6.0%  79.1%      383   8.9% MHeap_AllocLocked
     123   2.9%  82.0%      123   2.9% runtime.markspan
      95   2.2%  84.2%     1223  28.5% runtime.mallocgc
      74   1.7%  85.9%       74   1.7% runtime.MSpan_Init
      43   1.0%  86.9%     4234  98.6% github.com/reducedb/cityhash.unalignedLoad64
      40   0.9%  87.9%      595  13.9% runtime.MCache_Alloc
      32   0.7%  88.6%       32   0.7% runtime.markallocated
      31   0.7%  89.3%       56   1.3% MHeap_FreeLocked
```

As you can see, most of the time were spent copying memory (64.4%). And also the sweepspan (part of GC) is also running quite often (8.7%). 

Before this, I had no idea that there's that much memory being copied. So this is definitely interesting. I then looked the <a href="/images/2013-11-10-improving-cithhash-performance-by-go-profiling/before.svg">graph of the profile data</a> using the "web" command. 

It shows clearly that unalignedLoad64, a function that loads a uint64 from the buffer, is causing most of the memmove. Technically, it's calling binary.Read(), which creates an array of 8 bytes, and passes to another function which eventually calls runtime.copy to copy a few bytes of data from the original buffer into the array.

So now the reason for the large amount of time spent in memmove is clear. Basically, every time I call binary.Read(), it creates an 8 byte array. Up to 8 bytes of data are copied into it. Then the data in the array gets converted into an uint64. After that, the array is thrown away. And this is done over and over again for the whole 1.1G file, which means 1.1G of memory is being created in tiny 8-byte chunks, copied, and thrown away. It's no wonder the program is slow!

By this time, some of the readers are probably wondering why the heck I am using binary.Read() if I knew that I will be reading a uint64 from a slice. And they would be right again. Only excuse I have is that I had no clue and that was the first thing I found to work a few months back, so I just used it.

### Modifying the Implementation

The change turned out to be relatively simple. Instead of using binary.Read(), I used LittleEndian.Uint64() to read the uint64. After the change, I ran the same program again.

Here are the results from the post-change run. The time it took to hash the 1.1G file is only 2.8 seconds. That's 16X faster than before the change. The "top" profile output is also a lot more reasonable. 

```
duration = 2718339693ns
Total: 245 samples
      57  23.3%  23.3%       57  23.3% encoding/binary.littleEndian.Uint64
      50  20.4%  43.7%      227  92.7% github.com/reducedb/cityhash.CityHash128WithSeed
      40  16.3%  60.0%       97  39.6% github.com/reducedb/cityhash.unalignedLoad64
      35  14.3%  74.3%      146  59.6% github.com/reducedb/cityhash.fetch64
      28  11.4%  85.7%       28  11.4% github.com/reducedb/cityhash.uint64InExpectedOrder
      27  11.0%  96.7%      132  53.9% github.com/reducedb/cityhash.weakHashLen32WithSeeds_3
       8   3.3% 100.0%        8   3.3% github.com/reducedb/cityhash.weakHashLen32WithSeeds
       0   0.0% 100.0%        1   0.4% MHeap_AllocLarge
       0   0.0% 100.0%      227  92.7% _/Users/jian/Projects/cityhash_test.TestLatencyIntegers
       0   0.0% 100.0%      227  92.7% github.com/reducedb/cityhash.CityHash128
```

Also, nothing really jumps out when looking at the <a href="/images/2013-11-10-improving-cithhash-performance-by-go-profiling/after.svg">post-change profile data graph</a>. 

### Bloom Filter Benchmarks

Now that the changes are in, I went back and re-ran some of the bloom filter benchmarks. They look a lot more reasonable as well. Below is a comparison of the Scalable Bloom Filter. The post-change run is almost 2.5x faster than the pre-change run. Also, the post-change number (1442 ns/op) is a lot closer to some of the other hash functions (~1100 ns/op).

```
Scalable Bloom Filter
---------------------
BenchmarkBloomCityHash   1000000              1442 ns/op (after cityhash change)
BenchmarkBloomCityHash   1000000              3375 ns/op (before cityhash change)
```

### Summary

The Go authors have made it extermely simple to test, benchmark and profile Go programs so there's really reason for anyone not to do that often. It helps you see how your program works and where the bottlenecks are. It can also help you identify surprises that you may not have though of. A good example is in my case, I had no idea binary.Read() works the way it works until I profiled my program.

Comments/Feedback on [Hacker News](https://news.ycombinator.com/item?id=6710115), [Reddit](http://www.reddit.com/r/golang/comments/1qcygc/improving_cityhash_performance_by_go_profiling/)

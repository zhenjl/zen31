+++
Categories = ["papers", "security"]
date = "2015-02-22T19:57:56-08:00"
title = "Papers I Read: 2015 Week 8"
+++

### Random Ramblings

Another week, another report of hacks. This time, [The Great Bank Robbery](http://securelist.com/blog/research/68732/the-great-bank-robbery-the-carbanak-apt/), where up to 100 financial institutions have been hit.Total financial losses could be as a high as $1bn. You can download the [full report](http://25zbkz3k00wn2tp5092n6di7b5k.wpengine.netdna-cdn.com/files/2015/02/Carbanak_APT_eng.pdf) and learn all about it.

Sony spent $15M to clean up and remediate their hack. I wonder how much these banks are going to spend on tracing the footsteps of their intruders and trying to figure out exactly where they have gone, what they have done and what they have taken. 

I didn't make much progress this week on either [sequence](https://github.com/strace/sequence) or [surgemq](https://github.com/surgemq/surgemq) because of busy work schedule and my son getting sick AGAIN!! But I did merge the few surgemq [pull requests](https://github.com/surgemq/surgemq/pulls?q=is%3Apr+is%3Aclosed) that the community has graciously contributed. One of them actually got it tested on Raspberry! That's pretty cool.

I also did manage to finish up the [experimental json scanner](https://github.com/strace/sequence/commit/713979f70d6025308e434205973249aa3138e58e) that I've been working on for the past couple of weeks. I will write more about it in the next [sequence](http://strace.io/sequence) article.

Actually I am starting to feel a bit overwhelmed by having both projects. Both of them are very interesting and I can see both move forward in very positive ways. Lots of ideas in my head but not enough time to do them. Now that I am getting feature requests, issues and pull requests, I feel even worse because I haven't spent enough time on them. &lt;sigh&gt;

### Papers I Read

* [Memory-Efficient GroupBy-Aggregate using Compressed Buffer Trees](http://www.pdl.cmu.edu/PDL-FTP/HECStorage/git-cercs-12-08.pdf)

> Memory is rapidly becoming a precious resource in many data processing environments. This paper introduces
a new data structure called a Compressed Buffer Tree (CBT). Using a combination of buffering, compression,
and lazy aggregation, CBTs can improve the memoryefficiency of the GroupBy-Aggregate abstraction which
forms the basis of many data processing models like MapReduce and databases. We evaluate CBTs in the
context of MapReduce aggregation, and show that CBTs can provide significant advantages over existing hashbased
aggregation techniques: up to 2× less memory and 1.5× the throughput, at the cost of 2.5× CPU.

* [ELF: Efficient Lightweight Fast Stream Processing at Scale](https://www.usenix.org/system/files/conference/atc14/atc14-paper-hu.pdf)

> Stream processing has become a key means for gaining rapid insights from webserver-captured data. Challenges
include how to scale to numerous, concurrently running streaming jobs, to coordinate across those jobs to share
insights, to make online changes to job functions to adapt to new requirements or data characteristics, and for each job, to efficiently operate over different time windows. The ELF stream processing system addresses these new challenges. Implemented over a set of agents enriching the web tier of datacenter systems, ELF obtains scalability by using a decentralized “many masters” architecture where for each job, live data is extracted directly from webservers, and placed into memory-efficient compressed buffer trees (CBTs) for local parsing and temporary storage, followed by subsequent aggregation using shared reducer trees (SRTs) mapped to sets of worker processes. Job masters at the roots of SRTs can dynamically customize worker actions, obtain aggregated results for end user delivery and/or coordinate with other jobs.


* [Is Parallel Programming Hard, And, If So, What Can You Do About It?](https://www.kernel.org/pub/linux/kernel/people/paulmck/perfbook/perfbook.html)

Not just a paper, it's a whole book w/ 800+ pages.

>The purpose of this book is to help you program shared-memory parallel machines without risking your sanity.1 We hope that this book’s design principles will help you avoid at least some parallel-programming pitfalls. That said, you should think of this book as a foundation on which to build, rather than as a completed cathedral. Your mission, if you choose to accept, is to help make further progress in the exciting field of parallel programming—progress that will in time render this book obsolete. Parallel programming is not as hard as some say, and we hope that this book makes your parallel-programming projects easier and more fun.
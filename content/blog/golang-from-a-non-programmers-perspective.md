+++
Categories = ["golang"]
date = "2015-01-13T13:30:00-08:00"
title = "Go: From a Non-Programmer's Perspective"
+++

_Warning: Long Post. Over 3900 words according to `wc`. So read at your own risk. :)_

[Go](https://golang.org/) is a fairly recent programming language [created](http://golang.org/doc/faq#history) by Robert Griesemer, Rob Pike and Ken Thompson of Google. It has risen in popularity over the the past few years, especially since Go 1.0 was released. 

There are a ton of posts out there that talks about the pros and cons of Go, and why one would use it or not. In addition, there's a bunch of posts out there written by different developers coming from different perspectives, such as Python, Ruby, Node, Rust, etc, etc. Recently I even read a couple of Chinese blog posts on why Go is popular in China, and why some of the Chinese developers have abandoned Go, which are quite interesting as well. 

This post is my perspective of Go, how I picked it up, and what I think of it after using it for a while. It is not a post about why Go is better or worse than other languages.

In short, I like Go. It's the first programming language I've used in recent years that I can actually build some interesting projects, e.g., [SurgeMQ](https://github.com/surge/surgemq), in my limited spare time.


## My Background

I am not a programmer/developer. Not full-time, not part-time, not moonlight. I tell my colleagues and teams that "I am not technical."

But I do have a technical background. I have a MSCS degree from way back when, and have spent the first 6-7 years of my career performing security audits and penetration tests, and building one of the world's largest managed security services (at least at the time).

My programming langauge progression, when I was technical, has been BASIC (high school), Pascal and C (college), Perl, PHP, Java, and Javascript (during my technical career). I can't claim to be an "expert" in any of these languages, but I consider myself quite proficient in each at the time I was using them.

I was also reasonably network and system savvy, in the sense that I can get myself in and around the Solaris and Linux (UN*X) systems pretty well, and understand the networking stack sufficiently. I consider myself fairly proficient with the various system commands and tools.

For the past 12 years, however, I have not been a developer, nor a systems guy, nor a networking guy. Instead, I have been running product management for various startups and large companies in the security and infrastructure space. 

Since the career change, I've not done any meaningful code development. I've written a script here and there, but nothing that I would consider to be "software." However, I've managed engineering teams as part of my resonsibility, in addition to product management, to produce large scale software. 

In the past 12 years, my most used IDE is called Microsoft Office. So, in short, I am probably semi-technical, and know just enough to be dangerous.

### My History with Go

In 2011/2012, I had the responsibility of building a brand new engineering team (I was already running product management) at VMware to embark on a new strategic initiative. The nature of the product/service is not important now. However, at the time, because the team is brand new, we had some leeway in choosing a language for the project. VMware at the time was heavily Java, and specifically Spring given the [2009 acquisition of SpringSource](http://www.vmware.com/company/news/releases/springsource). While the new team had mostly Java experience, there was desire to choose something less bloated, and something that had good support for the emerging patterns of distributed software.

#### First Touch

Some of the team members had experience with Scala, so that became an obvious option. I did some research on the web, and found some discussions of Go. At the time, Go hasn't reached 1.0 yet, but there was already a buzz around it. I looked on Amazon, and found [The Way to Go](http://www.amazon.com/gp/product/B0083RVAJW/ref=docs-os-doi_0), which was probably the only Go book around at the time. For $3 on the Kindle, it was well worth it. However, due to the nascent nature of Go (pre 1.0), it was not a comfortable choice so I didn't put that as an option. But this was my **first touch of Go and it felt relatively painless**.

At the end, the team chose Scala because of existing experience, and that in theory, people with Java experience should move fairly easily to Scala. We were the first team in VMware to use Scala and we were pretty excited about it. 

However, to this date, I am still not sure we made the right decision to move to Scala (not that it's wrong either.) The learning curve I believe was higher than we originally anticipated. Many of the developers wrote Java code w/ Scala syntax. And hiring also became an issue. Basically every new developer that came onboard must be sent to Typesafe for training. It was simply not easy for most developers who came from a non-functional mindset to jump into a totally functional mindset. Lastly, the knowledge differences of new Scala developers and experienced ones made it more difficult for them to collaborate.

I also tried to read up Scala and at least understand the concept. I even tried to take the online course on Coursera offered by Martin Odersky. However, I just could not get my non-functional mind to wrap around the functional Scala. And since I really didn't need to code (nor the developers want me to), I gave up on learning Scala.

#### Second Touch

In any case, fast forward 2 years to Q3 of 2013. I had since left VMware and joined my current company, [Jolata](http://jolata.com), to build a big data network analytics solutions for mobile carriers and high-frequency trading financial services firms. We are a small startup that's trying to do a ton of things. So even though I run products, I have to get my hands dirty often. 

One of the things we had to do as a company is to build a repeatable demo environment. The goal is to have a prebuilt vagrant VM that we can run on our Macs, and we can demonstrate our product without connecting to the network. The requirement was that we had an interesting set of data in the database so we can walk through different scenarios.

The data set we needed was network flow data. And to make the UI look realistic, interesting and non-blocky, we wanted to generate noisy data so the UI looks like it's monitoring a real network. Because all of the developers are focused on feature development, I took on the task of building out the data set. 

By now, Go has released v1.1 and on its way to 1.2. It was then I started seriously considering Go as a candidate for this project. To build a tool that can generate the data set, we needed two libraries. The first is a [Perlin Noise](http://en.wikipedia.org/wiki/Perlin_noise) generator, and the second is [Google's Cityhash](https://code.google.com/p/cityhash/). Neither of these were available in Go (or not that I remember). I thought this would be a great opportunity to test out Go. The end results were my Go Learn Projects [#0 Perlin](https://github.com/dataence/perlinnoise), and [#1 Cityhash](https://github.com/dataence/cityhash). 

Both of these projects were relatively simple since I didn't have to spend a lot of time figuring out HOW to write them. Perlin Noise has well-established C libraries and algorithms, and Cityhash was written in C so it was easy to translate to Go. However, these projects gave me a good feel of how Go works.

In the end, I wrote the data generator in Go (private repo) and got the first taste of goroutines. Again, **this second touch with Go was also relatively painless**. The only confusion I had at the time was the Go source tree structure. Trying to understand $GOROOT, $GOPATH and other Go environment variables were all new to me. This was also the first time in 10 years that I really spent time writing a piece of software, so I just considered the confusion as my inexperience.

#### Third Touch and Beyond

Today, I no longer code at work as we have more developers now. Also, the Jolata product is mostly C/C++, Java and Node, so Go is also no longer in the mix. However, After getting a taste of Go in the first couple of Go projects, I've since spent a tremendous amount of my limited personal spare time working with it. 

I have since written various libraries for [bitmap compression](https://github.com/dataence/bitmap), [integer compression](https://github.com/dataence/encoding), [bloom filters](https://github.com/dataence/bloom), [skiplist](https://github.com/dataence/skiplist), and [many others](https://github.com/dataence). And I have [blogged my journey](http://zhen.org/blog/) along the way as I learn. With these projects, I've learned how to use the Go toolchain, how to write idiomatic Go, how to write tests with Go, and more importantly, how to optimize Go.

Interestingly, one of my most popular posts is [Go vs Java: Decoding Billions of Integers Per Second](http://zhen.org/blog/go-vs-java-decoding-billions-of-integers-per-second/). This tells me that a lot of Java developers are potentially looking to adopt Go.

All these have allowed me to learn Go enough to build a real project, [SurgeMQ](https://github.com/surge/surgemq). It is by far my most popular project and one that I expect to continue developing.

## My Views on Go

Go is not just a langauge, it also has a very active community around it. The views are based on my observation over the past 1.5 years of using Go. My Go environment is primary Sublime Text 3 with GoSublime plugin.

### As a Language...

I am not a language theorist, nor do I claim to be a language expert. In fact, prior to actually using Go, I've barely heard of generics, communicating sequential processes, and other "cool" and "advanced" concepts. I've heard of all the new cool programming languages such as Clojure and Rust, but have never looked at any of the code. So my view of Go is basically one of a developer n00b.

In a way, I consider that to be an advantage coming in to a new programming language, in that I have no preconceived notion of how things "SHOULD" be. I can learn the language and use the constructs as they were intended, and not have to question WHY it was designed that way because it's different than what I know. 

Others may consider this to be a huge disadvantage, since I don't know any better. There maybe constructs in other languages that would make my work a lot easier, or make my code a lot simpler. 

However, as long as the language doesn't slow me down, then I feel it's serving my needs. 

#### Go is Simple

As a language for a new deverloper, Go was very easy to pick up. Go's design is fairly simple and minimalistic. You can sit down and read through the [Language Specification](https://golang.org/ref/spec) fairly quickly in an idle afternoon. I actually didn't find the language reference until later. My first touch of Go was by scanning through the book _The Way To Go_. Regardless, there's not a lot to the language so it's relatively easy for someone like myself to pick up the basics. (Btw, I've also never gone through the [Go Tour](https://tour.golang.org/). I know it's highly recommended to all new Go developers. I just never did it.)

There are more advanced concepts in Go, such as interface, channel, and goroutine. Channel in general is a fairly straightforward concept. Most new programmers should be able to understand that quickly. You write stuff in, you read stuff out. It's that simple. From there, you can slowly expand on the concept as you _go_ along by adding buffered channels, or ranging over channels, or checking if the read is ok, or using quit channels.

For anyone coming from a language with threads, goroutine is not a difficult concept to understand. It's basically a light-weight thread that can be executed concurrently. You can run any function as a goroutine.

The more difficult concept is interface. That's because it's a <strike>fairly new concept that doesn't really exist in</strike> concept that's fairly different than other languages. Once you understand what interfaces are, it's fairly easy to start using them. However, designing your own interfaces is a different story. 

The one thing I've seen most developers complain about Go is the lack of generics. Egon made a nice [Summary of Go Generics Discussions](https://docs.google.com/document/d/1vrAy9gMpMoS3uaVphB32uVXX4pi-HnNjkMEgyAHX4N4) that you can read through. For me personally, I don't know any better. I have never used generics and I haven't found a situation where I strongly require it.

As a language a team, the simplicity of Go is _HUGE_. It allows develoeprs to quickly come up to speed and be productive in the shortest period of time. And in this case, time is literally money.

#### Go is Opinionated

Go is opinionated in many ways. For example, probably one of the most frustrating thing about Go is how to structure the code directory. Unlike other languages where you can just create a directory and get started, Go wants you to put things in $GOPATH. It took a few readings of [How to Write Go Code](https://golang.org/doc/code.html) for me to grasp what's going on, and it took even longer for me to really get the hang of code organization, and how Go imports packages (e.g., `go get`). 

If I go back and look at my first internal project, I would probably cry because it's all organized in a non-idiomatic way. However, once I got the hang of how Go expects things to be organized, it no longer was a obstacle for me. **Instead of fighting the way things should be organized in Go, I learned to _go_ with the flow.** At the end of the day, the $GOPATH organizational structure actually helps me track the different packages I import. 

Another way Go is opinionated is code formatting. Go, and Go developers, expect that all Go programs are formatted with [`go fmt`](http://blog.golang.org/go-fmt-your-code). A lot of developers hate it and some even listed it as a top reason for leaving Go. However, this is one of those things that you just have to learn to _go_ with the flow. Personally I love it. 

And as a team language it will save a ton of argument time. Again, time is money for a new team. When my new VMware team got started, we probably spent a good 30 person-hours debating code formatting. That's $2700 at a $180K fully-burdened rate. And that's not counting all the issues we will run into later trying to reformat code that's not properly formatted.

Go is also very opininated in terms of variable use and package import. If a variable is declared but not used, the Go compiler will complain. If a package is imported but not used, the Go compiler will complain. Personally, I like the compiler complaining about the unused variables. It keeps the code clean, and reduce the chance of unexpected bugs. I am less concerned about unused packages but have also learned to live with the compiler complains. I use [goimports](https://github.com/bradfitz/goimports) in Sublime Text 3 to effectively and quickly take care of the import statements. In fact, in 99% of the cases I don't even need to type in the import statements myself.

#### Go is Safe

Go is safe for a couple of reasons. For a new developer, Go does not make it easy for you to be lazy. For example, Go is a statically typed language, which means every variable must explicitly have a type associated with it. The Go compiler does infer types under certain situations, but regardless, there's a type for every variable. This may feel uncomfortable for developers coming from dynamic languages, but the benefit definitely outweighs the cost. I've experience first hand, as a product person waiting for bugs to be fixed, how long it takes to troubleshoot problems in Node. Having static types gives you a feeling of "correctness" after you have written the code.

Another example of Go not allowing you to be lazy is that Go's error handling is through the return of `error` from functions. There has been a ton of discussions and debates on the merit of `error` vs exception handling so I won't go through it here. However, for a new programmer, it really requires your explicit attention to handle the errors. And I consider that to be a good thing as you know what to expect at each step of the program.

Making things explicit and making it harder for developers to be lazy are a couple of the reasons that make Go safe.

Another reason is that [Go has a garbage collector](http://golang.org/doc/faq#garbage_collection). This makes it different from C/C++ as it no longer require developers to perform memory management. The difficulty in memory management is the single biggest source of memory leaks in C/C++ programs. Having a GC removes that burden from developers and makes the overall program much safer. Having said that, there's much improvement to be made to the GC given its nascent state. And, as I learned over the past 1.5 years, to write high performance programs in Go today, developers need to make serious efforts to reduce GC pressure.

Again, as a team langauge, the safety aspect is very important. The team will likely end up spending much less time dealing with memory bugs and focus more on feature development.

#### Go is Powerful

What makes Go powerful are its simplicity, its high performance, and advanced concepts such as channels, goroutines, interfaces, type composition, etc. We have discussed all of these in previous sections.

In addition to all that, one of the killer feature of Go is that all Go programs are statically compiled into a single binary. There's no shared libraries to worry about. There's no jar files to worry about. There's no packages to bundle. It's just a single binary. And that's an extremely powerful feature from the deployment and maintenance perspectives. To deploy a Go program, you just need to copy a single Go binary over. To update it, copy a single Go binary over. 

In contrast, to deploy a Node.js application, you may end up downloading hundreds of little packages at deployment time. And you have to worry about whether all these packages are compatible. The Node community has obviously developed a lot of good tools to manage dependencies and version control. But still, every time I see a Node app get deployed on a new machine, and have to download literally hundreds of little packages, I die a little inside.

Also, if you deploy C/C++ programs and depend on shared libraries, now you have to worry about OS and shared library version compatibility issues. 

Another powerful feature of Go is that you can mix C and assembly code with Go code in a single program. I haven't used this extensively, but in my attempt to [optimize](http://zhen.org/blog/go-vs-java-decoding-billions-of-integers-per-second/) the [integer compression](https://github.com/dataence/encoding) library, I added different C and assembly snippets to try to squeeze the last ounce of performance out of Go. It was fairly easy and straightforward to do.

One last thing, Go has a very large and complete standard library. It enables developers to do most, if not all, of their work quickly and efficiently. As the language matures and the community grows, there will be more and more 3rd party open source libraries one can leverage.

### As a Community

Today, Go has a very active community behind it. Specifically, the information sources I've followed and gotten help from include [#go-nuts IRC](https://botbot.me/freenode/go-nuts/), [golang subreddit](http://www.reddit.com/r/golang/search?q=golang&sort=new&restrict_sr=on&t=all), and obviously the [golang-nuts mailing list](https://groups.google.com/forum/#!forum/golang-nuts). 

I spent quite a bit of time in IRC when I first started. I've gotten help from quite a few people such as dsal, tv42, and others, and I am grateful for that. I am spending less time there now because of the limited time I have (remember, my day job is not development. :)

There's been some sentiments in the developer community that Go developers (gophers) are Google worshippers, don't accept any feedbacks on language changes, harsh to new comers who come from different languages,  difficult to ask questions because the sample code is not on play.golang.org, etc etc.

To be clear, I've never really spent much time with the different language communites, even when I was technical. So I have nothing else to compare to. So I can only speak from a human interaction level.

I can see it from both perspectives. For example, developers coming from different language backgrounds sometimes have experience with a different way of doing things. When they want to perfrom the same tasks in Go, they ask the question by saying here's how I solved this problem in language X, how do I translate that to Go? 

In some cases I've definitely seen people responding by saying that's not how Go works and you are doing it wrong. That type of response can quickly create negative sentiment and kill the conversation.

Another type of response I've seen is some developers telling the original poster (OP) that they are not asking questions the right way, and then promptly sending the OP a link to some web page on how to properly ask questions. Again, I can see how the OP can have a negative view on the matter.

I've expereinced some of this myself. When I implemented a [Bloom Filter](https://github.com/dataence/bloom) package last year, I did a bunch of performance tests and wrote a [blog post](http://zhen.org/blog/benchmarking-bloom-filters-and-hash-functions-in-go/) about the it. As a newbie learning Go, I felt like I accomplished something and I was pretty happy with it. I posted the link to reddit, and the first comment I got was

> Downvoted because I dislike this pattern of learning a new language and then immediately publishing performance data about it, before you know how to write idiomatic or performant code in it.

**Ouch!!** As a new Go developer, this is not the response I expected. In the end though, the commenter also pointed out something that helped me improve the performance of the implementation. (It was also then I realized how important it is to reduce the number of allocation in order to reduce the Go GC pressure.)

I can understand why some developers would feel annoyed about benchmarks from people who have no idea on what they are doing. Regardless, being nice is not a bad thing. Saying things like "WTF is wrong with you" (not related to the bloom filter post) will only push new developers away.

I quickly got over the sting because I am just too old to care about what others think I should or should not do. I continued my learning process by writing and optimizing Go packages, and posting the results in my blog. In fact, the [Go vs Java: Decoding Billions of Integers Per Second](http://zhen.org/blog/go-vs-java-decoding-billions-of-integers-per-second/) post has many of the optimization techniques I tried to increase the performance of Go programs.

Overall though, I felt I've learned a ton from the Go community. People have generally been helpful and are willing to offer solutions to problems. I have nothing to compare to, but I feel that the positives of the Go community far outweighs any negatives.

## Conclusion

In conclusion, it has been a tremendous 1.5 years of working with Go, and seeing Go grow both as a language and as a community has been very rewarding.

My focus now, in my limited spare personal time, is to continue the development of [SurgeMQ](https://github.com/surge/surgemq), which is a high performance MQTT broker and client library that aims to be fully compliant with MQTT 3.1 and 3.1.1 specs.
+++
Categories = ["papers", "security"]
date = "2015-02-08T19:57:56-08:00"
title = "Papers I Read: 2015 Week 6"
+++

[Papers We Love](http://paperswelove.org/) has been making rounds lately and a lot of people are excited about it. I also think it's kind of cool since I've been reading a lot of research papers over the past year or so. I have been killing some trees because of that.

My interests have been mostly around data analytics, but the specific focus areas have changed a few times. I have read papers on data structures (bloom filters, skiplist, bitmap compression, etc), security analytics, consumer behavioral analysis, loyalty analytics, and now back to security analytics. In fact, recently I started reading a few security research papers that I found on [covert.io](http://www.covert.io/), put together by Jason Trost.

In any case, I thought it might be an interesting idea to share some of the papers I read/scan/skim on weekly basis. This way I can also track what I read over time. 

### Random Ramblings

This week has been a disaster. I was the last one in the family to catch the cold, but probably lasted the longest. In fact I am still only about 50%. This whole week I have been having headaches, body aches, and haven't been able to concentrate. My body must be trying to catch up on sleep or something. For a couple days I actually slept for almost 12 hours a night!

I've been meaning to work on [sequence](https://github.com/strace/sequence) and finish updating the analyzer, but really had a hard time concentrating. Any non-working hours are basically spent in bed if I could.

So this is probably the worst week to start the "Papers I Read" series since I only technically read 1 paper. But I am going to cheat a little, and list the papers I read over the past couple of weeks, pretty much all in my spare time. 

This week we also saw Sony's accouncement that last year's hack cost them [$15 million](http://www.sony.net/SonyInfo/IR/financial/fr/150204_sony.pdf) to investigate and remediate. It's pretty crazy if you think about it. 

Let's assume that they hired a bunch of high-priced consultants, say $250/hour, to help comb through the logs and clean the systems. And let's say 2/3 of the $15m is spent on these consultants. That's `$10m / $250 = 40,000 hours`. 

Let's say these consultants worked full time, non-stop, no weekends, no breaks, for 2 months since the announcement on Nov 24, 2014, that would be a team of 56 people (`40,000 hours / 60 days / 12 hours/day = 56`) working 12 hour days!

I'll tell ya, these security guys are raking it in. They make money upfront by selling products/services to protect the company, then they make money in the back by selling forensic services to clean up after the hack.

[Disclaimer: any mistake in my calculations/assumptions I blame on my drugged brain cells.]

### Papers I Read

* [Beehive: Large-Scale Log Analysis for Detecting Suspicious Activity in Enterprise Networks](http://www.covert.io/research-papers/security/Beehive%20-%20Large-Scale%20Log%20Analysis%20for%20Detecting%20Suspicious%20Activity%20in%20Enterprise%20Networks.pdf)

> We present a novel system, Beehive, that attacks the problem of automatically mining and extracting knowledge from the dirty log data produced by a wide variety of security products in a large enterprise. We improve on signature-based approaches to detecting security incidents and instead identify suspicious host behaviors that Beehive reports as potential security incidents.

* [Data Mining for Cyber Security](http://minds.cs.umn.edu/publications/chapter.pdf)

> This chapter provides an overview of the Minnesota Intrusion Detection System (MINDS), which uses a suite of data mining based algorithms to address different aspects of cyber security. The various components of MINDS such as the scan detector, anomaly detector and the profiling module detect different types of attacks
and intrusions on a computer network.

* [VAST: Network Visibility Across Space and Time](http://www.covert.io/research-papers/security/VAST-%20Network%20Visibility%20Across%20Space%20and%20Time.pdf)

> Key operational networking tasks, such as troubleshooting and defending against attacks, greatly benefit from attaining views of network activity that are unified across space and time. This means that data from heterogeneous devices and systems is treated in a uniformfashion, and that analyzing past activity and detecting future instances follow the same procedures. Based on previous ideas that formulated principles for comprehensive
network visibility [AKP+08], we present the design and architecture of Visibility Across Space and Time (VAST), an intelligent database that serves as a single vantage point into the network. The system is based on a generic event model to handle network data from disparate sources and provides a query architecture that allows operators or remote applications to extract events matching a given condition. We implemented a proof-of-principle prototype that can archive and index events from a wide range of sources. Moreover, we conducted a preliminary performance evaluation to verify that our implementation works efficient and as expected.

* [Finding The Needle: Suppression of False Alarms in Large Intrusion Detection Data Sets](http://www.covert.io/research-papers/security/Finding%20The%20Needle-%20Suppression%20of%20False%20Alarms%20in%20Large%20Intrusion%20Detection%20Data%20Sets.pdf)

> Managed security service providers (MSSPs) must manage and monitor thousands of intrusion detection sensors.
The sensors often vary by manufacturer and software version, making the problem of creating generalized tools to separate true attacks from false positives particularly difficult. Often times it is useful from an operations perspective to know if a particular sensor is acting out of character. We propose a solution to this problem using anomaly detection techniques over the set of alarms produced by the sensors. Similar to the manner in which an anomaly based sensor detects deviations from normal user or system behavior, we establish the baseline
behavior of a sensor and detect deviations from this baseline. We show that departures from this profile by a sensor have a high probability of being artifacts of genuine attacks. We evaluate a set of time-based Markovian heuristics against a simple compression algorithm and show that we are able to detect the existence of all attacks which were manually identified by security personnel, drastically reduce the number of false positives, and identify attacks which were overlooked during manual evaluation.

* [A Close Look on n-Grams in Intrusion Detection: Anomaly Detection vs. Classification](http://user.informatik.uni-goettingen.de/~krieck/docs/2013a-aisec.pdf)

> Detection methods based on n-gram models have been widely studied for the identification of attacks and malicious software. These methods usually build on one of two learning schemes: anomaly detection, where a model of normality is constructed from n-grams, or classification, where a discrimination between benign and malicious n-grams is learned. Although successful in many security domains, previous work falls short of explaining why a particular scheme is used and more importantly what renders one favorable over the other for a given type of data. In this paper we provide a close look on n-gram models for intrusion detection. We specifically study anomaly detection and classification using n-grams and develop criteria for data being used in one or the other
scheme. Furthermore, we apply these criteria in the scope of web intrusion detection and empirically validate their effectiveness with different learning-based detection methods for client-side and service-side attacks.

* [Searching 20 GB/sec: Systems Engineering Before Algorithms](http://blog.scalyr.com/2014/05/searching-20-gbsec-systems-engineering-before-algorithms/)

Ok, this is a blog post, not a research paper, but it's somewhat interesting nonetheless. 

> This article describes how we met that challenge using an “old school”, brute-force approach, by eliminating layers and avoiding complex data structures. There are lessons here that you can apply to your own engineering challenges.

+++
Categories = ["cloud"]
date = "2009-05-06T07:41:57+00:00"
title = "The Reality of Workload Mobility, Federation, and Distribution"
+++


[ See bottom of the post for #workloadmob related discussions on Twitter ]

There, I covered my *aaS by listing all of the terms that people use for moving or distributing workloads around the clouds. Throughout this article I will use the term federation. There's been quite a bit written on this topic already, including several [great pieces](http://news.cnet.com/wisdom-of-clouds/?keyword=workload+mobility) from [James Urquhart](http://news.cnet.com/wisdom-of-clouds/?tag=rb_content;overviewHead). Any attempt to define something in the clouds will generate a ton of discussion, so I will attempt that here. :) Let's define what we mean by workload federation.



> 
**Workload** is the amount of work that's performed within some period of time. In many cases workloads are performed by an application, thus sometimes _workload_ and _application_ are used interchangeably.

**Workload federation** is about dynamically distributing or balancing the workloads as effectively as possible, regardless of physical location and optimizing business and operational goals.




The reality is, workload federation is HARD. It's a great vision and I am totally onboard with it. But still, this stuff is DIFFICULT to do! It's not that it's impossible, it's just not as simple as "Beam me up Scotty." In this series of posts, I want to explore this topic from several perspectives: goals, use cases and workloads.



### Goals



There are really two types of goals: business and operational. Business goals are what IT and LOB executives care about the most. These goals are generally factors that go into running a business. Operational goals are really technical goals that are related to running the infrastructure and providing the best user experience. The goals are summarized as follows:




  * **Optimize Cost** - The goal is the perform the workload in the most cost effective environment.

There's always a cost associated with running an application or performing some workload. There are many factors that go into the cost model, including compute, storage, network, I/O, and potentially some facility costs such as power and cooling. To truly optimize cost, sometimes you will need to better understand your applications. Is your application more compute intensive (like Hadoop type of apps)? Will it require large data set transfers? 

The idea is to be able to build a cost model for your application and set that as a policy for workload federation. Where the workload should be performed depends on the cost of moving that workload to various environments. You should be practical about the whole cost model and don't lose sight of the other goals you are trying to achieve.  



  * **Optimize Efficiency** - The goal is to perform the work in the environment so overall resources are utilized in the most efficient manner.

The idea here is that if you have a lot of work and you have different resources already reserved/allocated, you should distribute the work amongst the different resources so that all resources are being utilized. This may mean the overall cost is higher because you may be performing work in an expensive environment. However, the benefit is that your work maybe performed more quickly and results are returned to you faster.



  * **Minimize Risk** - The goal is to perform the work in the environment that has the lowest political and/or corporate risk.

I have written extensively in previous posts on the topic of security and compliance. At the end of the day, it's all about risk management. Enterprises want to minimize the risk they are exposed to, whether it's risk of data (IP or PII or others) breaches, non-compliance with regulations or mandates, or potential legal actions. Enterprises want control and transparency of their data and workloads. 

For example, in many EU and South America countries, certain types of data cannot leave the country because of potentially sensitive information. In addition to the issue of local laws, there's also the question of whose jurisdiction the data falls under when an investigation occurs. In most cases, the government where the data is housed will likely win. A good example of this type of concern is when the [French cabinet banned the use of Blackberry devices](http://www.ft.com/cms/s/2/dde45086-1e97-11dc-bc22-000b5df10621.html).  Again, the federation policy should include parameters that allows you to specify the location where the data and workload will be moved to. 



  * **Optimize Response Time** - The goal is to perform the work in the environment that has the best response time.

Response time can be defined in may different ways, including the round trip time between the user clicking on a link or button and the data being presented to the user, or the transaction time for database operations. Different workloads may have different requirements on response time. And sometimes workload may not necessarily be performed in the environment that has the fastest response time, as it may cost 10X more in terms of actual dollars spent to process that workload. So the it's usually a good idea to define an acceptable response time range and optimize another vector in the federation policy.

There are three major components to response time, including network latency, network throughput, and processing time. Processing time is the amount of time it took the application to process the request and prepare the result set. According to [Wikipedia](http://en.wikipedia.org/wiki/Comparison_of_latency_and_throughput):



> 
_Latency_ is the delay between the initiation of a network transmission by a sender and the receipt of that transmission by a receiver. In two-way communication, it may be measured as the time from the transmission of a request for a message, to the time when the message is successfully received.

_Throughput_ is the number of messages successfully delivered per unit time. Throughput is controlled by available bandwidth, as well as the available signal-to-noise ratio and hardware limitations.




All three of these components determine and affect user experience and perception. A good example of optimizing response time is serving web pages. In general, the best user experience is when the web page is returned the fastest (yes I know it depends on the browser rendering time as well.) To accomplish this goal of serving web pages fast, the request maybe processed by an environment that's actually physically farther away from the user compare to some other environments.




Note that all these goals are interrelated and all of the examples given above can be dissected in different ways. Enterprises are encouraged to prioritize and weigh all of these goals in creating their federation policy. 

In the next two posts, we will look at the vision of workload federation from two other aspects:


  * Use Scenarios - what are the different uses scenarios that enterprises are thinking with respect to workload federation?


  * Workloads - what are the different workload types that will be running in the clouds and does it make sense for these workloads to federate?




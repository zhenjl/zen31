+++
Categories = ["cloud"]
date = "2008-06-26T06:09:17+00:00"
title = "CloudCamp: Cloud Definition, SLAs, Security and Others"
+++

Reuven Cohen, Dave Nielsen, Sam Charrington and a group of awesome volunteers organized a very successful [CloudCamp](http://www.cloudcamp.com) event last night. This was organized in 3.5 weeks, which is an amazing feat. The event probably attracted 200-300 people. You can see some of the [pictures](http://www.flickr.com/search/?q=cloudcamp) of the event on flickr. The format was an [unconference](http://en.wikipedia.org/wiki/Unconference). There were 20+ sessions proposed and they were all very interesting. The topics range from cloud computing definition to transactions processing.

Here are some of the topics that I gathered based on the sessions I attended and people I've talked to.



### The definition is very cloudy!



There's no agreement on the definition of Cloud Computing. Reuven Cohen held a very popular session on "What is Cloud Computing?" There were at least 40 people in the room that was supposed to hold only 20. There were a wide variant of definitions, going from Reuven's very open definition (internet centric software) to another person's very restrictive definition (cloud computing must use web services, XML, SOAP, etc). 

There were also discussions (and disagreements) on whether Google App engine is considered a cloud or not. Interesting enough, some of the people there didn't consider GAE as a cloud. In one of the sessions, someone put an even more restrictive constraint on cloud computing. He said that a cloud MUST run any existing application without modification. So in that case, GAE would not be a cloud by his definition. I am definitely in the camp of that GAE is a cloud. 

Some interesting questions were asked as well, such as the question from a Microsoft guy, "Does the operating system still matter, if the the application is running in the cloud. My answer to that was it depends on the type of application. If it's a web centric application that has a web front end, uses a database for storage, and doesn't use any of the low level file IO, then really there's no need to know what the OS is. In that case, the OS doesn't matter. 

The term that's used most to describe cloud computing is _elasticity_: the ability to quickly provision and de-provision computing resources on demand. Almost everyone I've talked to or listened to agrees to that. Some of the enterprise attendees also noted this as one of the biggest benefits of the cloud. When business units come to IT with new application requirements, IT now has a way to quickly spin up resources without having to wait weeks or months to procure equipment. The other thing that everyone agrees on is the _utility_ model: the ability to pay for what you use. 



### Service level agreements



This topic was heavily discussed in the "No Cure for Cancer: Manage the Expectations of Cloud Computing" session. To summarize, there's almost no SLAs provided by the cloud providers today. Even Jeff Barr from Amazon said that AWS only provides SLA for their S3 service. I haven't researched the SLA issue so not sure how true that is. But if it's true, I think this will be one of the biggest factor, if not the biggest factor, in enterprise adoption. Can you imagine enterprises signing up cloud computing contracts without SLAs clearly defined? It's like going to host their business critical infrastructure in a data center that doesn't have clearly defined SLA. 

We all know that SLAs really doesn't buy you much. In most cases, enterprises get refunded for the amount of time that the network was down. No SLA will cover business loss. However, as one of the CSOs I met said, it's about risk transfer. As long as there's a defined SLA on paper, when the network/site goes down, they can go after somebody. If there's no SLA, it will be the CIO/CSO's head that's on the chopping block.



### Security



Another topic that was discussed in Sam Charrington's "How Cloud Impacts Enterprise Computing" session is security in the cloud. When Sam asked the group what are the factors that prevent enterprise from adopting the cloud, Ben Charian from ServiceCloud empathically said "security." He talked about that the clouds must be certified or audited against standards or frameworks such as PCI. I've written about cloud security requirements [here](http://onsaas.net/2008/06/10/tough-security-questions-for-saas-providers-part-1/) and [here](http://onsaas.net/2008/06/18/tough-security-questions-for-saas-providers-part-2/) so I won't elaborate on this topic. Needless to say, I am in total agreement with Ben. What I didn't agree with Ben on is the need to rewrite these frameworks or standards specifically for the cloud. I believe many of the controls such as identity management and segregation of duties are the same in the cloud or out of the cloud.



### Other observations and interesting tidbits


* As the enterprise use more cloud resources, there will be a point where it may make sense to bring things back in house rather than continuing to use the cloud. 
* The cloud computing discussions are focused mainly on the infrastructure/platform-in-the-cloud. Applications-in-the-cloud or SaaS was hardly discussed. I get the feeling that most of the attendees don't consider SaaS to be cloud computing, rather, it's applications running on top of (or in) the clouds.
* Cloud computing spending is opex instead of capex, allowing business units to make their own decisions.
* Make sure you partner with someone who you trust and work with you on deploying to the cloud.




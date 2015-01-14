+++
Categories = ["cloud"]
date = "2008-07-02T04:57:28+00:00"
title = "Response to \"10 Reasons Enterprises Aren’t Ready to Trust the Cloud\""
+++


Stacey Higginbotham over at GigaOM wrote an interesting piece on [10 Reasons Enterprises Aren’t Ready to Trust the Cloud](http://gigaom.com/2008/07/01/10-reasons-enterprises-arent-ready-to-trust-the-cloud/). Even though I agree that some of these points are valid reasons on why enterprises are hesitant in moving into the cloud, I have to wonder whether Stacey meant to be provocative (read: flame bait) on the piece. Also, the piece seems to be quite opinionated and lack support in many cases. Let's drill down on it a bit.

### 1. It’s not secure.

I have written extensively on this blog ([here](http://onsaas.net/2008/06/10/tough-security-questions-for-saas-providers-part-1/) and [here](http://onsaas.net/2008/06/18/tough-security-questions-for-saas-providers-part-2/)) regarding the security concerns of SaaS and cloud computing. However, saying that the cloud is not secure is definitely a stretch. I would like to see some supporting evidence on this. The only major "security breach" I've seen is probably the [Salesforce case](http://blog.washingtonpost.com/securityfix/2007/10/database_theft_leads_to_target.html).

In addition, none of the regulations or industry mandates, including HIPAA, GLBA, SOX, PCI, FISMA, etc etc, say anything about not allowing data to be outside of the corporate firewalls. In fact, many of the enterprises in the affected industries are already outsourcing some of their critical data. For example, financial companies using credit card processing services such as ViewPointe. There's also plenty of hospitals using external services. PCI also has a specific section on hosting providers. Again, no regulation or mandate explicitly state that data cannot leave the corporate firewalls. 

What CIOs/CSOs care mostly about is that cloud (application or platform) providers must meet their security requirements, there's transparency in the security and operational practices, and that they can audit the provider or review the appropriate audit reports from the provider. The issue comes down to trust. 

### 2. It can’t be logged. 

Again, this is really about auditability, especially for compliance. This is definitely an area that's lacking and cloud providers would be wise to do more in this area. Again, I wrote about that here: [4. Access Audit - Who has accessed my data and where’s my access logs?](http://onsaas.net/2008/06/10/tough-security-questions-for-saas-providers-part-1/)

### 3. It’s not platform agnostic.


Seriously though, is this really an issue? We are still in the world of multiple OS platforms, including different variants of Linux, Microsoft Windows, Mac OS X, Sun Solaris, IBM AIX, HP UX, etc etc etc. Is platform agnostic really that critical? Just like in the on-premise world, enterprises would be wise to evaluate the cloud platforms they plan to use based on a predefined set of requirements. Also, is supporting multiple cloud platforms really a concern that will prevent enterprise adoption? 

### 4. Reliability is still an issue.

Again, I agree that reliability is a concern. However, that's a concern regardless of what you decide. You have to worry about reliability if you choose to go with your own data center or cloud. You have to worry about reliability if you choose to partner with a data center provider to hose your gears. You have to worry about reliability if you choose to go into the cloud. Heck, you have to worry about reliability even if you just host your gears in your own IT network.

Stacey said "Even inside an enterprise, data centers or servers go down, but generally the communication around such outages is better and in many cases, fail-over options exist." I am sorry, but by definition, the cloud platforms usually have these capabilities built-in already. A single server or multiple servers failing is usually not going to affect your cloud applications or platforms.

I believe the real issue is service level agreement. Are the cloud providers providing adequate SLAs and do the CIOs feel comfortable with the SLA that they are getting? 

### 5. Portability isn’t seamless. 

No disagreement here. Currently there's not an enterprise version of the [data portability standard](http://www.dataportability.org/). That can turn many enterprises away if they have no way of retrieving/migrating their data if they choose to go with another provider.

### 6. It’s not environmentally sustainable.

Again, a good issue to raise. However, I would like to see some evidence to show that creating and maintaining your own data center is more efficient than going into the cloud. There will always be excess capacity in order to handle spikes, regardless whether you build your own data center or go into the cloud. 

### 7. Cloud computing still has to exist on physical servers.

No disagreement that data locality is an important consideration when moving into the cloud. I wrote about it in a previous blog. However, that just means enterprises should be aware of this issue and make sure that's part of their requirement for evaluating the cloud vendors. This however does not mean enterprises won't adopt because of this concern.

### 8. The need for speed still reigns at some firms. 

The increase in bandwidth to home and offices is one of the main reasons why clouds are hot these days. However, I agree with Stacey that speed is definitely a concern for certain types of applications. At CloudCamp, during Jeff Barr's AWS feedback session, the first hot topic that came up was how do people move a HUGE amount of data into the cloud and back. People talked about shipping hard drives as a solution to this type of problem.

However, this is not going to be an issue for most enterprises in the US, UK and countries with adequate bandwidth. Take for example applications such as Salesforce.com CRM, NetSuite, and many others, these applications do not require the need to transfer large amount of data back and forth so they are ideal for delivering via the web.

So again, a valid concern, but not a show stopper.

### 9. Large companies already have an internal cloud.

Again, I would like to hear more evidence from Stacey to back this up. I agree that most enterprises already have IT infrastructure in place, but most of these infrastructures are not considered clouds. My conversations with enterprises, including discussion from CloudCamp, is that enterprise IT groups are stretched thin and they can't respond fast enough to business requirements. When the business require certain applications to do their job, they have to go provision hardware, software, space, etc and that process can take months. Going with the cloud allows them to quickly react to the business requirements and makes it a win-win situation.

Even if enterprises have their internal clouds, does that mean that shouldn't consider external clouds? Enterprises should, and will, always weigh the cost/benefits to determine what's the right solution for them.

### 10. Bureaucracy will cause the transition to take longer than building replacement housing in New Orleans.

Agreed. In big companies that's ways going to be the case. No one is suggesting that all enterprises will move into the cloud overnight. Many of the enterprises are just starting to experiment with the cloud to see what can and cannot be done. This is healthy and it's the right approach. A good example is [New York Times using Amazon EC2 to convert millions of articles and TIFF image into PDF files](http://open.blogs.nytimes.com/2008/05/21/the-new-york-times-archives-amazon-web-services-timesmachine/).

Again, enterprises are adopting the cloud, just cautiously. 


+++
Categories = ["cloud"]
date = "2009-05-15T22:43:27+00:00"
title = "The Thousand Faces of Cloud Computing"
+++

It's amazing that people are still [arguing](http://bit.ly/19RyZx) over what cloud computing is and what is a cloud. I am certainly not immune to such [naive arguments](http://groups.google.com/group/cloudsecurityalliance/browse_thread/thread/e2f9836c28c30589). Claims such as "EC2 is NOT a cloud" just makes my head spin and wonder what the heck people are thinking. But if I taking a step back and try to understand why people are so passionate about this subject, I start to realize why there are so many definitions for Cloud Computing and why people continue to passionately argue over these definitions.

The short of it is that cloud means different things to different people. The Cloud has different characteristics to people coming from service provider backgrounds than people from a developer background; it has different meanings to people who care more about architectures than people who are more business-oriented; and it certainly .. to people who are building the clouds than the consumers of the cloud.

So instead of creating a single definition for Cloud Computing, let's look at it from


* Two perspectives
* Five architecture characteristics
* Three delivery models
* Three deployment models
* Three consumption models
* Two pricing models
* Six types of users
* Four business benefits
* Five characteristics


### Two Perspectives



There are passionate discussions on the definition of Cloud and Cloud Computing. If we summarize the arguments, we can see that there are really two camps of people: those who looks at Cloud as an architecture and those who looks at Cloud as a business model. In many cases they agree on many of the characteristics but there's usually one topic that really heats up the discussion and that is whether pricing and billing should be a defining characteristic of the Cloud.

The Cloud Architecture camp usually argues that how the Cloud is priced and billed should not be a defining characteristic of the Cloud since that's a business decision. And they are absolutely right about that.

The Cloud Business camp also passionately argues that how the Cloud is priced must be a defining characteristic, otherwise how else can the user be billed? And they are absolutely right about that as well.

At the end of the day it's about perspectives. Here are the characteristics again and where I think they fall:






CharacteristicArchitectureBusiness



Infrastructure Abstraction
✓



Resource Pooling
✓



Ubiquitous Network Access
✓



On-Demand Self-Service
✓



Elasticity
✓



Pricing Model
✓



Consumption Model
✓







### Five Architecture Characteristics



* Infrastructure Abstraction
* Resource Pooling
* Ubiquitous Network Access
* On-Demand Self-Service
* Elasticity



I am going to refer you to the write ups in [Guidance for Critical Areas of Focus in Cloud Computing](http://www.cloudsecurityalliance.org/guidance/csaguide.pdf) from [Cloud Security Alliance](http://www.cloudsecurityalliance.org/), as well as the [Draft NIST Working Definition of Cloud Computing](http://www.elasticvapor.com/2009/05/us-federal-government-defines-cloud.html). These folks have done an awesome job of writing these up so I won't elaborate here. Notice that these five are architecture characteristics so I didn't include the utility-based pricing characteristics here.



### Three Delivery Models



* Software as a Service
* Platform as a Service
* Infrastructure as a Service



Again, I am going to refer you to the write ups in [Guidance for Critical Areas of Focus in Cloud Computing](http://www.cloudsecurityalliance.org/guidance/csaguide.pdf) from [Cloud Security Alliance](http://www.cloudsecurityalliance.org/), as well as the [Draft NIST Working Definition of Cloud Computing](http://www.elasticvapor.com/2009/05/us-federal-government-defines-cloud.html). This is generally referred to as the SPI model.



### Three Deploy Models



I found that the distinction of _public, private, managed, community and hybrid_ clouds in both the NIST and CSA documents somewhat difficult to comprehend. I don't mean that they don't make sense but you really have to think through them before you can understand them. In most cases, the follow three seem to be easier to understand.





* Internal Cloud - An internal cloud lives within the 4 walls of the enterprises (like their data center.) It's fully built, operated, controlled and managed by the enterprises themselves. It has all five of the architecture characteristics of a Cloud. It may or may not have the pricing model required for external clouds since some enterprises may not care about chargebacks.
* External Cloud - An external cloud lives outside of the enterprises and it's usually built and operated by service providers but the resources maybe controlled and managed by the customers. The external cloud can either be shared (multi-tenant) or dedicated (single-tenant). It has all five of the architecture characteristics of a Cloud. The service provider will usually dictate the consumption and pricing models of the external clouds.
* Private Cloud - A private cloud is a combination of internal and external clouds. In most cases enterprises have more than one cloud just like they have some infrastructures inside the 4 walls and some outside. Even though there's both internal and external clouds, enterprises will want to control and manage all of the resources that belong to them, potentially through a single pane of glass. The cloud resoures are **_private_** to the customers, thus the name private cloud.





### Three Consumption Models



* Allocation-based
* Resource pool-based
* Usage-based



I've [previously written](http://www.zhen.org/zen20/2009/05/09/three-cloud-resource-consumption-models/) about the consumption models so please use that as reference.



### Two Pricing Models



One of the interesting debates out there is whether Clouds must have utility-based pricing, that is, consumers are only billed for what they used/allocated. I've generally seen the following two pricing models from service providers who have cloud offerings.



* Utility-based - This is the pay-per-use model that most people associate with cloud infrastructures. Amazon and Google App Engine are based on these models.
* Subscription-based - Most people tend to forget the subscription model is very popular in the cloud as well. For example, Salesforce is based on a per-user-per-month charge, so is Google Apps Premium Edition (per-user-per-year.) In fact, most of the cloud applications (SaaS) are based on this model. In addition, we are seeing some of the traditional service providers who are launching clouds also offer this pricing model as well.





### Six Types of Users


We will take a look at it from the angle of cloud consumers and why they care about clouds. On a high level, there are probably six types of cloud users.


* Enterprise IT
* Independent Software Vendors (ISVs)
* System Integrators (SIs)
* Web Developers
* Community Developers
* Consumers



#### Enterprise IT



Enterprise IT teams are the ones that manages and operates corporate IT infrastructures. They are responsible for delivering applications and infrastructure to support the lines of businesses (LOBs). They are the ones that care most about enterprise features such as security, manageability, reliability, availability, etc etc. 

However, they are also the ones that are under huge pressure to innovate and accelerate the solution delivery. Gone are the days that IT can take 3 months to provision servers to support a new business application. LOBs want their solutions and they want them now!

Clouds are appealing to the enterprise IT teams because it provides seemingly infinite resources at their fingertip and the IT teams can provision the resources on-demand. So instead of requiring the LOBs to wait 3 months, IT teams can now do that much quicker.



#### Independent Software Vendors (ISVs)



ISVs are users who develop products and solutions for enterprises. Traditionally they have delivered their products as software or hardware appliances. The ISVs will need to support multiple versions of their software as most of their customers will not likely upgrade as soon as new versions come out. They may support 2 versions back or 10 versions back, depending on the size of the customers, how much influence the customers have and the maturity of the ISVs. Government entities are notorious in their slowness in upgrade as each version will need to go through rigorous testing process. For ISVs who deliver products as software, they have to also worry about the runtime environments such as the OS, application stack, etc. There are ISVs that have hundreds of combinations they have to test for each version they release. Last but not least, some ISVs simply don't have the resource to acquire a TON of hardware for test and development due to load/performance testing requirements or the number of environments the have to worry about.

Supporting existing versions and testing for hundreds of runtime environments take a huge amount of resources and limits the resource available for innovation. So clouds are appealing to the ISVs as they can now deliver their software as a service (SaaS). By going the SaaS route, the ISVs can largely eliminate the runtime environment concerns as they can have much better control of the infrastructure they use to run their SaaS. The ISVs can also have better control over how and when they upgrade their products as they generally only have one environment to upgrade, instead of potentially thousands of different environments. And with the cloud, the ISVs can provision additional resources as needed to test their products and not have to worry about paying huge capex upfront.



#### System Integrators (SIs)



System integrators, such as Accenture and Cap Gemini, are almost extensions to the enterprise IT teams. Their solutions are generally developed as consulting projects. They develop and deliver solutions to clients who have engaged them to solve specific problems. The solutions they develop sometimes are large scale projects that can take months or years to deliver. For years, SIs have been creating best practices from the custom solutions they developed so they can speed up the development of delivery of other projects (but charge the same regardless. :) 

Clouds are appealing to them because they see clouds as one way to help them accelerate the development and delivery of solutions to their clients. They clients will see quick turnaround for solutions and the SIs can easily replicate some of the solutions they developed for one client to another. It's a win-win situation for both of them.



#### Web Developers



Web developers are the early adopters of the clouds. They are the ones who are developing Web 2.0 sites such as Smugmug and others. AWS highlights many of these web developers on [their blog](http://aws.typepad.com/). These web developers care about time to market and usually don't have the expertise, desire and/or capital to provision and manage large infrastructures. They are focused on solving a specific problem and the less they have to worry about infrastructure, the better it is for them.

Clouds are appealing to the web developers because of these exact reasons. Clouds deliver to the web developers on-demand and elastic resources, thus removing the concern of infrastructure provisioning. The clouds allow web developers to focus on their problems.



#### Community Developers



Community developers are individual and open source developers who just wants to have their own playground but don't want to concern themselves with hardware provisioning. They are very similar to the web developers category but they are not developing a business in the cloud. 



#### Consumers



The consumers in general loves the clouds. Consider the number of users there are for cloud applications such as Yahoo! Mail, Gmail, Google Apps, Salesforce.com, Qualys, NetSuite and many others, then you will start to see the scale and reach of cloud applications. In many cases, consumers don't even care whether you call these "cloud applications." To them they care about the ease of use and access, and that they don't have to worry about any software installation or configurations. The wide spread of cloud applications is one reason why Netbooks are so appealing these days.


### Four Business Benefits

Where the Cloud Architecture camp is focused on how to create the best architecture to handle the business needs, the Cloud Business camp is zeroed in on translating the architectural benefits into financial terms. It’s great that enterprises can have ubiquitous access and elasticity, but if it costs them 10x more in investment for a 2x return, that’s not going to fly. In this section we will look at some of the business benefits of Cloud Computing:




  * Reduce Cost


  * Minimize Risk


  * Increase Agility


  * Maintain Focus





#### Reduce Cost



One large enterprise has outsourced their test and development environments to an outsourcer, and paying approximately $10,000 per environment per year, regardless of whether the resources are virtual or physical. They have 3000 such environments, so they are essentially paying $30 million per year on just test and development environments. They did a user survey to find out the utilization of these environments, and all the developers responded saying that these environments are heavily utilized and there’s tight handoff from one team to another. An audit, however, revealed that overall, the environments are utilized < 10%, and that 70% of the environments are logged into once per year by developers.

Another large financial services firm said that their infrastructure is utilized less than 2% overall. 

Enterprises can lower CAPEX by not having to procure additional hardware and software but to use cloud providers and their pay-per-use utility pricing to handle resource spikes; they can lower OPEX by abstracting the hardware differences, and providing self-service capabilities to the end users so IT don’t always have to be the middle man; and they can lower their CAPEX and OPEX by increasing utilization of these expensive resources, or reduce the amount of resources required to accomplish the same tasks.



#### Minimize Risk



It still shocks me that in this age, companies are still running some of their mission critical applications on servers sitting under a IT administrator’s desk. But more often than not, when I talk to enterprises, this very scenario always comes up. IT administrators do this for different reasons. Some just don’t want to give up control; some don’t want to go through the arduous procurement process; some don’t have the time; and some simply don’t see why it’s a problem. In majority of these cases, if enterprises can provide these IT administrators the ability to quickly migrate these servers into the Cloud, they are more than willing to do so.

The Cloud, by design, is architected to be highly available and fault tolerant. Any one component going down should not affect the availability of applications. The Cloud is one way for enterprises to reduce risk of mission critical applications going down.

Another way that Cloud helps enterprises reduce risk is it can give IT more control over the resources. Imagine a large organization that allows their end users to procure their own hardware and software because IT simply doesn’t have the cycles to manage that. Soon enough there will 100 different hardware suppliers and 1000 different software suppliers. IT will have no idea how these resources are being used and what the utilization levels are. In addition, this scenario presents a huge security risk to the enterprises, as there’s no control of the procurement process.

The Cloud centralizing the procurement and management of hardware and software, IT can maintain control but at the same time provide users the resources they are looking for. It will be a win-win situation for both sides.



#### Increase Agility



Joe Weinman, AT&T;’s VP of Strategy, said that “an on-demand service provider typically charges a utility premium — a higher cost per unit time for a resource than if it were owned, financed or leased.” Joe is absolutely correct here, and the recent McKenzie report validates this as well. To determine whether Cloud Computing is the right approach, enterprises must look at other business benefits in addition to hard cost. 

What is it worth to an enterprise when they can respond faster to business requirements and enable businesses to bring products to market quicker? For example, going from 8 weeks to 3 days to 10 minutes in provisioning of resources to run enterprise services or spinning up 500 servers in minutes to test an application.

The global economy is forcing companies to be global as well. One such company has 10’s of 1000’s of developers/consultants spread all over the world, all requiring quick access to test and development environments. It’s impractical for this company to build and operate data centers around the world, and it’s also not the company’s core competency and strategy to have all these data centers. One of the things they are looking to do is build a “cloud abstraction layer” on top of multiple clouds, and allow developers to request resources. Depending on the developer’s location and resource requirement, the software will automatically provision the right resources and inform the user when ready. The ability to distribute the workload onto multiple clouds gives this company the flexibility and speed to respond to business needs. How much does this worth?



#### Maintain Focus



Like the company described above, most enterprises do not consider building and operating data centers as their core competency. These enterprises consider it to be more of a distraction to their core business. By utilizing the service provider clouds, the enterprises can maintain their focus and accelerate innovation on their core business.

The classic example here is the New York Times case study, where the developers processed 4TB of data in matter of minutes to convert scans of 15 million news stories into PDFs for online distribution. Instead of worrying about taking months to procure hardware for this one time task and spending much more money, New York Times took it to the Cloud and completed the task in less than 24 hours and with much less money.

The Cloud allows allow IT organizations to focus on providing the best infrastructure possible, and developers to focus on their applications instead of the infrastructure.

### Five Characteristics

In this section, I will describe somewhat of a revised set of architecture characteristics that define Cloud Computing. 



#### Abstraction



A key characteristic of the Cloud is to provide an abstraction layer for the lower level resources, including compute, network and storage components. Users are strongly discouraged, or disallowed, to think in terms of the physical hardware, but instead consider in terms of the resources required. The users don’t need to worry about whether the underlying hardware is from IBM, HP, Cisco, Juniper, NetApp or EMC. What’s presented to them is a homogenous set of resources. This removes the users from having to worry about the differences in hardware or software configuration. The resources may be shared amongst many different users, or dedicated to a single user; and maybe presented as a set of virtual machines or a set of APIs.



#### On-Demand



The set of resources presented by the Cloud can be provision or de-provisioned as needed by the users. The term “on-demand” also conveys a notion of speed. When resources are requested, they are provisioned within minutes, not days, weeks or even months. In most enterprises today, hardware procurement is a multi-month long process that can slow down projects and frustrate employees. One large system integrator has recently trimmed the process of provisioning environments from 8 weeks to 3 days. However, to truly meet the business needs, they must go from 3 days to hours, if not minutes.



#### Elasticity



Elasticity is probably the most defining characteristic for Cloud Computing. In addition to the need to provision on demand, enterprises are increasingly required to scale for anticipated or unanticipated resource requirements. For example, one top university that we recently talked had a housing application that gets HAMMERED two weeks before the start of the school year, EVERY year. Traffic dies down and there’s very little activity after the initial period. A large financial services firm has 30 servers dedicated to handling a 15-minute job every day. These are examples of anticipated resource requirements. Enterprises know when they will need the additional resources, how much resources are required and the duration of time they will need the resources for.

An example of unanticipated resource requirement is when the market department rolls out a huge campaign and drove 10 times the traffic to the enterprise website, and the IT department was never informed. This is a real life scenario that I am sure many of you have experienced. The question at that point is not to point fingers, but to figure out how to rapidly provision 10 times the resources to handle that traffic. Another example that we have heard from a large software vendor is their need to periodically spin up anywhere from 50 to 500 servers for software testing, and then quickly spin down when finished.

Elasticity, or the ability to rapidly provision and quickly scale up and down the resources, is an architecture model that affects not just infrastructure, but also the application design. In addition, given that most of these scenarios, whether anticipated or unanticipated, do not happen often, so it’s unrealistic financially for enterprises to provision enough resource to handle these spikes. The Cloud would allow enterprises to rent the additional resources in any quantity at any time.



#### Self-Service



The traditional process of application owners or developer asking IT to procure and provision resources is arduous and long. Consider the software vendor scenario we described earlier where developers need to spin up 50 to 500 servers for software testing. The developers need to modify this environment often to test different configurations and application architectures, and they need to have these modifications done in real-time so they don’t miss their delivery schedule. IT organizations are not resourced to handle this type of scenarios. The best resolution would be to provide the developers a pool of resources that they can do their own configurations. The self-service model not only works for these developers, but more and more business users are asking for similar capabilities as they are asked to be more efficient.



#### Ubiquitous



Ubiquitous access, or the ability to access from anywhere, using any device, is one of the great promises of the Web. This promise will become real as smart phones, netbooks and laptops become the prevalent way of access information. Ray Ozzie, Micrisoft’s Chief Software Architect, described his vision of “3 Windows in the Cloud,” where the 3 Windows included Windows on PC, Windows on mobile devices, and Windows on TVs. As you can see, one of key messages in this vision is ubiquitous access.

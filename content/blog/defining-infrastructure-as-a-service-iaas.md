+++
Categories = ["cloud"]
date = "2008-06-03T18:28:28+00:00"
title = "Defining Infrastructure-as-a-Service (IaaS)"
+++


As described in [a previous post](http://onsaas.net/blog/defining-saas-paas-iaas-cloud-computing-etc), the infrastructure layer of the whole setup is about space, pipe, firewalls, VPNs, routers, switches, physical server and storage. In order to maintain such infrastructure, a company must employ a whole team of network, security and storage engineers. Even with hosting providers such as Savvis and Rackspace providing professional services, the amount of work companies must do in order to setup and maintain this type of infrastructure is still tremendous. To scale this infrastructure, the companies must monitor the usage and acquire new servers as needed. In addition, space and pipe are usually the biggest cost factor when it comes to hosting. That's why the dotCom hosting providers such as Exodus were such high flying companies during the boom days.

The announcements of Amazon's S3 and EC2 service in 2006 changed this whole game. Instead of provisioning for all the stuff that's required before a single OS is installed, companies now have an option of simply provisioning for resources in the EC2 cloud and use S3 as storage. This also eliminates the need to staff teams of network, security and storage engineers. Amazon, in fact, is providing "infrastructure as a service."

"Infrastructure-as-a-Service" or IaaS is essentially new fancy marketing term for "[utility computing](http://en.wikipedia.org/wiki/Utility_computing)", which, according to [Simon Wardley](http://blog.gardeviance.org/2008/03/saas-utility-and-clouds.html), is "the packaging of computing resources, such as computation and storage, as a metered service similar to a physical public utility, This system has the advantage of a low or no initial cost to acquire hardware; instead, computational resources are essentially rented". 

So to summarize: 

> Infrastructure-as-a-service is about replacing critical data center resources such as space, pipe, firewalls, VPNs, routers, switches, physical servers and storage with scalable and highly-available resources in the cloud. It is about having a data-center-in-the-cloud.

So what are the characteristics of an infrastructure service? In my opinion, the following list are must-have requirements:


* **On-Demand** Must be able to rapidly provision or de-provision resources as necessary. One of the main advantage of having the data center in the cloud is that you don't have to go provision your own servers, storage and bandwidth. You should be able to simply request more as you need them, and remove them as you are done. The IaaS provider should simply charge you for what you have used and nothing more. Remember, one of the keyword here is "**rapid**".
* **Scalable** Must be able to scale infinitely if necessary. Ok, maybe not infinitely but the service should be scalable enough that you can quickly add tens or hundreds of servers as needed. 
* **Self-Sustaining or Self-Healing** Must be able to self-sustain without end-user intervention. Some folks call this self-healing and that's fine too. The point is that there should be enough redundancy and high-availability features built into the service that a physical servers going down must not affect the virtual servers running on that infrastructure.
* **Multi-Tenant** Must be able to share this same infrastructure with multiple end customers.
* **Customer Segregation** Must be able to segregate the data by end customers. Security and privacy is one of the major obstacle for companies in adopting cloud services, so it is critical that proper security measures are put in place to segregate customer data. Some of the definitions also listed "Virtualization" as one of the requirements for IaaS or cloud computing. To me, that's not really a requirement per se. It is a technical solution to the problem of data or customer segregation.



The poster child of IaaS is undoubtedly Amazon. Their EC2 and S3 service have more or less defined the pricing and service in this market. Some of the posts listed [here](http://onsaas.net/blog/defining-saas-paas-iaas-cloud-computing-etc) have listed other vendors such as EngineYard and Joyent. However, I consider these vendors to be more Platform-as-a-Service providers, rather than IaaS, as they provide the OS and the whole application stack, rather than just space, pipe, storage and servers.

Remember from the above illustration, once you have all the data center infrastructure, you still need to install the OS and application server stack, etc. So what IaaS does not help you with is the ongoing maintenance of the operating system, the stack and your application. So you still have to deal with patches, securing your OS, etc. These areas are where Platform-as-a-Service (PaaS) providers can add value. 

We will discuss PaaS in the next post.

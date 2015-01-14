+++
Categories = ["cloud"]
date = "2008-08-29T04:43:54+00:00"
title = "The Rise of Cloud Platforms and Why the OS Doesn't Matter"
+++

Platform-as-a-Service (PaaS) is one of the buzzwords that's mentioned often in the cloud computing space. I've written a [blog post](http://onsaas.net/2008/06/03/defining-saas-paas-iaas-etc/) describing IaaS, PaaS and SaaS. In short, PaaS is a platform for delivering applications, similar to a pre-built system with hardware, OS and application stack all built in. In the PaaS case, this system is hosted. All you have to do is "upload" the application code and it should take care of the executing and scaling of it.

[![](http://zhen.org/zen20/wp-content/uploads/2008/06/iaas-paas-saas.png)](http://zhen.org/zen20/wp-content/uploads/2008/06/iaas-paas-saas.png)

A quick survey of the land (by no means comprehensive, I am also including ONLY application platforms, not service-specific platforms such as DabbleDB) shows that there's a plethora of PaaS players out there, each with their own target audience. Some provide more of a raw execution platform, some provide a full suite of tools for creating applications online. Unfortunately, most of these vendor approaches will lock you into their proprietary platform. If you ever want to move to another platform, you have to rewrite at least a portion of code using the new vendor's API. Phil Wainewright has written about this in his blog post "[A plethora of PaaS options](http://blogs.zdnet.com/SAAS/?p=472)."








Company
Application Type





Bungee Labs
Web applications



Coghead
Web applications



Google App Engine
Python web applications



LongJump
Business applications



NetSuite NS-BOS
Business applications



Ning
Social networking applications



Joyent
Web applications



Mosso
Web applications



Rollbase
Business applications



Salesforce Force.com
Business applications




In one of the [CloudCamp SF](http://www.cloudcamp.com/) sessions in July, one of the guys from Microsoft asked whether the OS matters in cloud computing. My answer to that was it depends on the type of application. If it’s a web centric application that has a web front end, uses a database for storage, and doesn’t use any of the low level file IO, then really there’s no need to know what the OS is. In that case, the OS doesn’t matter.

All these vendors have targeted applications that are delivered over the web, and almost all of the vendors listed above try to abstract the OS from the developers so that they don't have to worry about the underlying infrastructure. As Mosso's slogan claims, "Code, load and go."

Even though cloud computing is still in its infancy; however, as it matures, cloud providers will move upmarket to provide additional business value to customers. We will see a rise of cloud application platforms appear on the horizon. Specifically, we will see more domain-specific cloud platforms for different verticals or application types. For example, I can imagine there are developers working on a MMORPG cloud platform (maybe it's here already if you consider Metaplace to be that) that will provide execution and management (of virtual goods, zones, accounts) for MMO developers; or a data analytics cloud platform that provides all the basic OLAP functions.

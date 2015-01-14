+++
Categories = ["cloud"]
date = "2008-09-04T14:16:39+00:00"
title = "The Rise of Cloud Privatization"
+++


The world of clouds these days is full of definitions and counter-definitions. There are many posts that try to define the concept of cloud computing; many that try to distinguish utility computing, grid computing and cloud computing; many that try to define public vs private clouds; and many that dismisses the notion of private clouds. 

Jonh Foley, in his article "[The Rise Of Enterprise-Class Cloud Computing](http://www.informationweek.com/blog/main/archives/2008/07/the_rise_of_ent.html)", referred to private cloud as an oxymoron,



> 
That's an oxymoron since cloud computing, **by definition**, happens outside of the corporate data center, but it's the technology that's important here, not the semantics.




But by whose definition? The industry as a whole haven't even been able to nail down a concrete definition of cloud computing. Given that there's no concrete definition, then by definition, private cloud is not an oxymoron. But I do agree with John, let's focus on the technology and not the semantics.

[Geva Perry](http://gevaperry.typepad.com/), chief marketing officer at GigaSpace Technologies, did just that. By focusing on the technology and architectural aspects of cloud computing, he wrote in a GigaOM [blog post](http://gigaom.com/2008/02/28/how-cloud-utility-computing-are-different/),



> 
Cloud computing is a broader concept than utility computing and relates to the underlying architecture in which the services are designed. **It may be applied equally to utility services and internal corporate data centers**, as George Gilder reported in a story for Wired Magazine titled [The Information Factories](http://www.wired.com/wired/archive/14.10/cloudware.html?pg=1&topic=cloudware&topic_set=).






### Cloud Attributes



But instead of everyone trying to create their own definition of clouds, let's look at the list of attributes that clouds have and compare public and private clouds.





  * **Elasticity**: The ability to dynamically provision (expand) or de-provision (shrink) the computing capacity as needed.

  * **Utility**: The ability to be charged by the amount of resources used. Great examples would include Amazon Web Services' charge model. In an enterprise setting, sometimes business units are charged by the internal IT groups for the resources they requested. The utility model would allow IT groups to perform chargebacks in a similar model to AWS.

  * **Scalability**: The ability to either handle growing amounts of work in a graceful manner, or to be readily enlarged. For example, it can refer to the capability of a system to increase total throughput under an increased load when resources (typically hardware) are added. [ via [wikipedia](http://en.wikipedia.org/wiki/Scalability) ]

  * **Reliability & Availability**: No failed whale! The cloud infrastructure and platforms must be reliable and available to the applications that are using them. There's probably a lot of technology involved here to make this happen. For example, the ability to transparently migrate a virtual server when the running node has failed.

  * **Manageability**: The ability to effectively manage (start/stop/migrate/expand/shrink/etc) the different server and application instances in the cloud.

  * **Security**: The ability to secure the data and access to the cloud. Public clouds still have a [trust issue](http://cloudfeed.net/2008/08/23/challenges-of-enterprise-cloud-computing/) with many of the enterprise customers, which is why the ? is there.

  * **Performance**: The ability to execute and complete tasks within the acceptable timeframe (defined by the SLA).

  * **API**: I consider this to be a desired attribute. This refers to the ability of doing resource management via some type of documented programming interface.

  * **Virtualization**: Applications are decoupled from the underlying hardware. Multiple applications can run on one computer (virtualization a la VMWare) or multiple computers can be used to run one application (grid computing). [ via [GigaOM](http://gigaom.com/2008/02/28/how-cloud-utility-computing-are-different/) ]

  * **Multi-Tenancy**: The ability to house multiple customers using the same infrastructure and still be able to segregate the data.

  * **SLA-Driven**: The system is dynamically managed by service-level agreements that define policies such as how quickly responses to requests need to be delivered. If the system is experiencing peaks in load, it will create additional instances of the application on more servers in order to comply with the committed service levels — even at the expense of a low-priority application. [ via [GigaOM](http://gigaom.com/2008/02/28/how-cloud-utility-computing-are-different/) ]

  * **Support**: The ability to smack someone upside the head when something fails.








AttributesPublicPrivate



Elasticity
✓
✓



Utility
✓
✓



Scalability
✓
✓



Reliability & Availability
✓
✓



Security
?
✓



Performance
✓
✓



API
✓
✓



Virtualization
✓
✓



Multi-Tenant
✓
✓



SLA-Driven
?
✓



24x7 Support
✓
✓




So if we are looking purely from a technology perspective, private clouds can absolutely exist. In fact, given the questions for the public cloud, enterprises are more likely to experiment with private clouds for mission critical applications. 



### Market and Vendors



According to Merrill Lynch, the public and private cloud infrastructure, platform, applications and advertising together will be a $160 billion market by 2011, or roughly 12% of the total worldwide software market.



> 
The total $160bn addressable market opportunity includes $95billion in 
business and productivity apps, and another $65 billion in online advertising. 

IBM and Sun have comprehensive solutions for ‘internal Clouds’. Dell targets large scale data centers, and HP provides ‘everything as a service’, making their solutions attractive for ‘external Clouds’.   




So who are some of the private cloud infrastructure/platform startups that are taking advantage of this $160 billion market? (Feel free to leave a comment if I missed anyone.)







CompanyProduct




3Tera
AppLogic



Arjuna
Agility



Cassatt
Active Response?



Elastra
Elastra Cloud Server



Enomaly
Enomalism



GigaSpaces
XAP, EDG, and Community Edition






### Private Cloud Links





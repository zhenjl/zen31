+++
Categories = ["cloud"]
date = "2008-09-05T04:28:01+00:00"
title = "Google Group Discussion on \"Private\" Clouds"
+++


I asked a totally unrelated question on the [Cloud Computing google group](http://groups.google.ca/group/cloud-computing/) a few days ago and triggered a [very active discussion](http://groups.google.ca/group/cloud-computing/browse_thread/thread/42b3784a39af2707?hl=en) on where "private" cloud is an oxymoron or not.

_[ Please let me know if I am taking any of the quotes blow out of context. ]_

Ben Yamin called "**private cloud computing a paradoxical phenomenon**" and Ray Nugent called it an "**oxymoron**." But even Ray agrees that many of his customers are asking about it,



> 
Correct me if I'm wrong but most, if not all, of what I'm hearing from customers is around how to take AWS like services and tuck them within the four walls of their enterprise to somehow get economies of scale, lower costs and quicker scale/customer service to their constituents. Therein lay the Foggy part...




Rich Wellner agrees that we should "**not care so much what things are called as much as what they do**," so he explained that "private" clouds does exist based on the list of attributes he's compiled:



> 
1) Multiple vendors accessible through open standards and not centrally
administered

2) Non-trivial QOS (see the gmail debate thread)

3) On demand provisioning

4) Virtualization

5) The ability for one company to use anothers resources (e.g. bobco 
using ec2)

6) Discoverability across multiple administrative domains (e.g. brokering to multiple cloud vendors)

7) Data storage

8) Per usage billing

9) Resource metering and basic analytics

10) Access to the data could me bandwidth/latency limitations, security,

11) Compliance – Architecture/implementation, Audit, verification

12) Policy based access – to data, applications and visibility

13) Security not only for data but also for applications

Now here we start to see some things that aren't applicable to enterprise clouds (i.e. 1, 5, 6). But the bulk of the list still works.  And it's worth noting that EC2 fails on more than three of those things (i.e. 1, 11, 12, 13), but people don't hesitate to allow them the use of the term cloud.




I think Jim Starkey from NimbusDB summed it up best,



> 
As I understand it, if you use Amazon EC2, it is cloud computing.  But if Amazon itself uses EC2, it's only fog computing.  Or maybe (shudder) internal cloud computing. This is, of course, utter nonsense.




Laurent Therond also brought up an interesting point,



> 
Amazon and Google would love for external entities to cofinance their clouds, because they own the infrastructure *and* they actually use it to run their own affairs. On the other hand, if you were to offer them to migrate their mission critical systems to some other Cloud Computing vendor (let's assume you could find one up to the task), they would laugh at you loudly.




I am quite happy to see this level of discussion on this. My stand on this is quite clear and explained [here](http://cloudfeed.net/2008/09/04/the-rise-of-cloud-privatization/).

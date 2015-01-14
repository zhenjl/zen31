+++
Categories = ["cloud"]
date = "2009-05-13T08:01:43+00:00"
title = "Google Lost Grip on Enterprise Reality"
+++


A couple weeks ago Rajen Sheth, Senior Product Manager for Google Apps, wrote an interesting blog post titled "[What we talk about when we talk about cloud computing](http://googleenterprise.blogspot.com/2009/04/what-we-talk-about-when-we-talk-about.html)." This week, Network World wrote an piece on "[Google, VMware argue over private clouds](http://www.networkworld.com/news/2009/051209-google-vmware-clouds.html?hpg1=bn)," essentially comparing the Google blog and an upcoming blog piece from Dan Chu, VMware's VP of Emerging Markets. In this blog I want to share some of my thoughts on this topic. 



[ Full disclosure: I work for VMware and Dan's my boss. However, this is my personal blog and the opinions expressed in this blog are my views and do not necessarily reflect the views and opinions of VMware. ]





### Enterprise IT



First of all, Google has lost grip on the reality of enterprise computing. Or maybe Google never really got it since it never truly was an enterprise IT provider. Remember, in 2008, Google got 97% of its revenues from web advertising. Even though Google does probably run one of the biggest enterprise IT shops in the world (their own,) the applications they use and maintain are vastly different than 90% of the enterprise IT shops out there. 

Secondly, enterprise IT teams will never run EVERYTHING in the clouds, and that goes for Google's cloud offerings (GAE, GMail, etc) as well as any other external cloud. There are plenty of applications and data that have very strict regulations that will prevent them from ever going to external clouds. At May 7th's [Churchill Club CIO Agenda event](http://churchillclub.org/eventDetail.jsp?EVT_ID=817), Karenann Terrell, Corporate VP & CIO of Baxter, talked specifically about some of the applications that are under HIPAA regulation and cannot move to external clouds. Some of the comments on the Google post also pointed to the same issue.

Thirdly, for many of the applications that enterprise IT want to move into the cloud, they will not want to rewrite them to fit Google's cloud requirements. Enterprise IT teams have invest many person-years in selecting the best application components (frameworks, message bus, etc), developing and testing their applications. They want to move these applications into the cloud with as few changes as possible, preferably with no changes at all. In this case, I am not even talking about ISV applications like Exchange and SharePoint. I am talking about custom built corporate applications that enterprise IT teams built for their LOBs.

Last but not least, with respect to the section about Google can innovate faster, enterprise IT teams would much prefer to innovate on their own terms instead of Google dictating innovation. When was the last time someone or some organization can influence Google in their product direction?



### Enterprise Workloads



Google's cloud offerings (GAE, GMail, etc) are definitely good for some enterprise workloads, assuming they are not mission critical and do not contain any sensitive data. If businesses depend on the applications or the data contain sensitive information such as credit card or PII, Google's likely not the best option. Let's look at some common enterprise use cases that Google cannot support with the "supercomputer."



1. Applications such as SAP, Oracle Financials, and Microsoft Exchange are business-critical core IT applications that many IT shops are consider virtualizing and moving into the cloud. These are applications that Google cannot handle. 
2. Enterprise IT teams have strict guidelines on what application frameworks and components they will support in production environments. So developers must develop an application using enterprise-proven and enterprise-approved software components. Google's "supercomputer" does not provide any type of options for enterprises to be able to use their own components such as their own message bus or database.
3. To extend the previous example a bit, enterprise IT teams would love to be able to develop and test applications in the cloud and eventually run in their own production environment. Again, given the strict guidelines to software components, Google will not be able to handle this.
4. An interesting scenario is that many companies want to have their DR site in the cloud so they can reduce DR costs. Again, nothing Google can do about this.
5. Many enterprises are interested in the ability to overflow additional capacity requirements to the clouds operated by service providers. For example, a company might be expecting to run a huge marketing campaign and need extra capacity. What they don't want to do is buy new servers and software and only run them for the campaign period. In this case, moving some of the workload into the cloud makes perfect sense. Again, nothing Google can do about this.





### Enterprise Requirements



Notwithstanding the fact that Google cannot handle most of the enterprise workload, Google also cannot support some of the key enterprise requirements.


* Manageability - Google does not provide enterprise IT teams much in the way of manageability. You get to drop your code into Google and that's about all you can do.
* Security and Compliance - Please read my [previous blog on this topic](http://www.zhen.org/zen20/2009/05/03/security-and-compliance-in-the-age-of-clouds/)
* Interoperability - What you write for GAE is pretty much locked in. You will need to at least rewrite portions of the application in order to work outside of GAE.
* Integration - GAE can only execute calls from an HTTP request and (pls correct me if I am wrong) can only integrate with other web/cloud services via HTTP requests. This definitely limits the type of applications that can be developed.





### Summary



Google's cloud offerings have their places and they obviously work very well for Google in many cases. For example, GAE is great when you need to develop a brand new web-based application that doesn't require enterprise-class features. Gmail and Google Apps are awesome as well (I use both) but they just can't replace the enterprise products at this time.

It's great that Google can claim hardware and software infrastructures as their true differentiators. I have no doubt that they probably have the most efficient infrastructure. It's just that for majority of the enterprise workloads and requirements, Google is just not a good fit. Enterprise IT wants to have their own private cloud that potentially can span both internal cloud built by the IT teams and external clouds hosted by service providers. 

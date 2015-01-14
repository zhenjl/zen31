+++
Categories = ["saas", "cloud"]
date = "2008-06-10T13:06:31+00:00"
title = "Tough security questions for SaaS providers"
+++


We will be writing a series of blog posts on the tough questions that SaaS providers can expect to get from customers or they should ask themselves. The questions will span many different areas including security, compliance, sales, marketing and operations. This is Part 1 of the security questions.

As we mentioned previously here, one of the biggest obstacle to enterprise SaaS adoption is the issue of trust. Customers are asking SaaS providers "Can I Trust You?!" The security analysts and warriors are [asking](http://www.networkworld.com/supp/2008/ndc3/051908-cloud-storage-five-questions.html) [similar](http://searchsecurity.techtarget.com/magazinePrintFriendly/0,296905,sid14_gci1313252,00.html) [questions](http://rationalsecurity.typepad.com/blog/2007/11/reprise-on-dema.html).

Some SaaS advocates have [argued](http://www.cxotoday.com/cxo/jsp/article.jsp?article_id=73540&cat_id=908) that concerns for SaaS security are just [red herring](http://www.ebizq.net/blogs/saasweek/2008/06/common_saas_misconceptions/). It is true that, to date, there hasn't been any major breaches amongst SaaS providers. However, we have already seen some activities such as the [breach at Salesforce.com](http://blog.washingtonpost.com/securityfix/2007/10/database_theft_leads_to_target.html). In addition, we have seen many anecdote evidence that multi-tenant architectures in the B2C (e.g., Flickr, YouTube) world are [prone to data leakage](http://markeseremet.blogspot.com/2007/02/is-flickr-secure-whos-cookies-are-these.html). I have also personally experienced this on YouTube. The following screen capture shows an account that's NOT mine (again, that's NOT me in the video!!) but it popped up in my browser when I tried to go to YouTube.

[![](http://onsaas.net/wp-content/uploads/2008/06/notmyacct.jpg)](http://onsaas.net/wp-content/uploads/2008/06/notmyacct.jpg)

One may argue that these are consumer sites and are not relevant for the SaaS providers. However, the same technologies and architectures are being used in both the consumer and enterprise world. In fact, as the trend of IT consumerization continues, we will see more and more of the consumer technologies being used in enterprise applications. Think about it this way, what if this Salesforce.com and your customer list popped up in your competitor's screen?

SaaS providers should be prepared to answer security questions from customers and enterprises. Here are a list of questions that SaaS providers will likely get asked during customer trials/evaulations.



### 1. Data Locality - Where's my data?



Due to compliance and data privacy laws in various countries, locality of data is of utmost importance in many enterprise architecture. For example, in many EU and South America countries, certain types of data cannot leave the country because of potentially sensitive information. In addition to the issue of local laws, there's also the question of whose jurisdiction the data falls under when an investigation occurs. In most cases, the government where the data is housed will likely win. A good example of this type of concern is when the [French cabinet banned the use of Blackberry devices](http://www.ft.com/cms/s/2/dde45086-1e97-11dc-bc22-000b5df10621.html). 

Many enterprises have architected around these issues for the on-premise software they install. However, with cloud computing and SaaS, this issue is even more exasperated. In a cloud computing environment, sometimes you don't know where your data is stored or where your application is being run; and some proponents of cloud computing are also saying that you shouldn't have to worry about where the computing resources are as long as your application is running and behaving as it should. However, other leaders in the cloud computing space are taking note of the data privacy and locality issues. For example, [Amazon recently announced the availability of an European S3 cloud](http://www.allthingsdistributed.com/2007/11/amazon_s3_in_europe.html), and [Salesforce.com is also planning Singapore data center](http://www.datacenterknowledge.com/archives/2008/May/21/salesforcecom_plans_singapore_data_center.html).  

Given the regulatory compliance and data privacy concerns, SaaS providers should be ready to answer tough questions about where their computing resources are and will customer data be ever transferred outside to another jurisdiction with different laws.



### 2. ata Segregation - How is my data segregated with other customers, potentially my competitors?



Everyone's talking about the benefits of multi-tenancy in the SaaS world, but many seem to ignore one of the biggest security concerns, mixing customer data together, that came along with multi-tenancy.   

One of the reasons that hampered SaaS adoption initially was trust. End users must _trust_ that the SaaS providers have the best security in place to protect their data and never expose their data to anyone outside of the authorized domain. Therefore, the ability to segregate data by end customer is a critical requirement for the SaaS providers. There are [many architectural methods](http://msdn.microsoft.com/en-us/library/aa479086(printer).aspx) in [segregating the end customer data](http://www.ibm.com/developerworks/library/ar-saassec/index.html). At the end, the requirements come down to that users must never see the data that they are not authorized to see, and that end customer's data should never be exposed to other end customers. 

Saas Providers would be wise to consider data segregation early on in the architectural design. For most ISVs turning into SaaS providers, this is an unfamiliar territory and should seek guidance if possible. SaaS providers should also understand the customer concerns and address them early on.



### 3. Data Access - Who can access my data in your company? 



Enterprises have spent hundreds of thousands of dollars on identity and access management systems, log management systems and other software to ensure that employees access only information they are allowed. Within the confines of their firewalls, IT organizations may feel that they have the situation somewhat under control. The advent of SaaS have changed that. With the company data outside of the firewall and in a "cloud," IT organizations no longer can control who and when their data-in-the-cloud will be accessed. Without visibility into the cloud, IT organizations are accepting a much bigger risk compare to when everything's inside the firewall. Even though many SaaS providers have offered various capabilities such as authentication integration with customers' own LDAP servers, this perception of lost control is a difficult hurdle to get over.

SaaS providers offering cloud services, whether it's infrastructure, platform or application, should accept the responsibility of protecting customer data as a single breach could affect all of the customers. SaaS providers must be prepared to help customers understand their security policies on user access, activity monitoring as well as segregation of duties.



### 4. Access Audit - Who has accessed my data and where's my access logs?



The last few years we have seen a rise of [log management](http://www.loglogic.com) and [SIEM](http://www.arcsight.com) solutions aimed at compliance-aware organizations. These products is responsible for collecting, analyzing, correlating, archiving and reporting on all activities happening inside an IT infrastructure. Part of the reason these products became such a success is because of the need to track and monitor user activities in the world of regulatory compliance. In addition to compliance, IT organizations use logs to help them identify security issues, perform troubleshooting and forensics analysis, and analyze traffic and user patterns.

With software in the cloud, network, system and application logs are no longer easily accessible by IT organizations. They either have to negotiate access to these logs during contract time, or they have find new ways of monitoring user activities. Given that the IT organizations don't "own" the software, it makes it even more difficult to "hack" around the system. Without access logs, IT organizations may not be able to answer simple questions from auditors, such as "who have accessed the financial information in the past quarter?"

Knowing how critical access logs are to compliance, operations and security matters for IT organizations, SaaS providers should consider providing access logs as a part of their normal service or have it as an option for customers. As an example, [Amazon's S3 service offers options to enable and download access logs.](http://docs.amazonwebservices.com/AmazonS3/2006-03-01/ServerLogs.html)


### 5. How are the users authenticated and authorized?



Companies have spent hundreds of man years and millions of dollars trying to setup single-sign-on systems inside the corporate firewalls. Most companies, if not all, are storing their employee information in some type of LDAP servers. In the case of SMB companies, a segment that has the highest SaaS adoption rate, Active Directory seems to be the most popular tool for managing users. In many cases, companies have designed their IT infrastructure so that all authentication, including VPN, web proxy, file server, and others will go through this single infrastructure. The process of employee onboarding and termination is much easier this way.

Just as companies start to have some success, the advent of the SaaS model changes the scenario again. With SaaS, the software is hosted outside of the corporate firewall. Many times user credentials are stored in the SaaS providers' databases and not part of the corporate IT infrastructure. This means SaaS customers must remember to remove/disable accounts as employees leave the company and create/enable accounts as come onboard. In essence, having multiple SaaS products will increase IT management overhead.

SaaS customers will start asking questions on identity and access integration and providers would be wise to design such features in early on. For example, SaaS providers can provide delegate the authentication process to the customer's internal LDAP/AD server so that companies can retain control over the management of users.



### 6. Web Application Security - How secure is the SaaS provider's web application?



One of the "must-have" requirements for a SaaS application is that it has to be used and managed over the web (in a browser.) This creates an interesting scenario. In the on-premise scenario, when a vulnerability is found, at least you have your firewall protecting the application so you may get a bit more time to patch it (assuming the application vendor provides the patch in a timely fashion.) However, in the SaaS world, there is no such luxury. Any vulnerability identified can potentially have detrimental impact on all of the customers. Even leading security companies [aren't immune to security holes](http://www.darkreading.com/document.asp?doc_id=155995&f_src=drdaily) in their web applications.

Web application security is quite a hot topic these days and it's discussed by many security researchers such as [rmogull](http://securosis.com/2008/06/11/there-are-no-safe-web-sites-2/) and [RSnake](http://ha.ckers.org/). Here's an interesting article on "[What web application security really is](http://www.tssci-security.com/archives/2008/06/15/what-web-application-security-really-is)".

Verizon Business recently released their [Verizon Business 2008 Data Breach Investigations Report](http://www.verizonbusiness.com/resources/security/databreachreport.pdf). Of all the breaches, 59% of the breaches involve hacking, with the following breakdown:


>   * Application/Service layer -39%
>   * OS/Platform layer - 23%
>   * Exploit known vulnerability -18%
>   * Exploit unknown vulnerability - 5%
>   * Use of back door -15%

Attacks targeting applications, software, and services were by far the most common technique, representing 39 percent of all hacking activity leading to data compromise. This follows a trend in recent years of attacks moving up the stack. Far from passé, operating system, platform, and server-level attacks accounted for a sizable portion of breaches. Eighteen percent of hacks exploited a specific known vulnerability while 5 percent exploited unknown vulnerabilities for which a patch was not available at the time of the attack. Evidence of re-entry via backdoors, which enable prolonged access to and control of compromised systems, was found in 15 percent of hacking-related breaches. The attractiveness of this to criminals desiring large quantities of information is obvious.


Currently there's really no mandate or requirement for SaaS providers to provide detailed security analysis of the SaaS application. However, it would be wise for the SaaS providers to start considering something similar to what PCI DSS has required of the merchants:



>   1. 6.5 Develop all web applications based on secure coding guidelines such as the Open Web Application Security Project guidelines. Review custom application code to identify coding vulnerabilities. Cover prevention of common coding vulnerabilities in software development processes, to include the following: 
>     1. 6.5.1 Unvalidated input 
>     2. 6.5.2 Broken access control (for example, malicious use of user IDs) 
>     3. 6.5.3 Broken authentication and session management (use of account credentials and session cookies) 
>     4. 6.5.4 Cross-site scripting (XSS) attacks 
>     5. 6.5.5 Buffer overflows 
>     6. 6.5.6 Injection flaws (for example, structured query language (SQL) injection) 
>     7. 6.5.7 Improper error handling 
>     8. 6.5.8 Insecure storage 
>     9. 6.5.9 Denial of service 
>     10. 6.5.10 Insecure configuration management 
>
>   2. 6.6 Ensure that all web-facing applications are protected against known attacks by applying either of the following methods:  
>     * Having all custom application code reviewed for common vulnerabilities by an organization that specializes in application security 
>     * Installing an application layer firewall in front of web-facing applications. 


Additional sources of information provided as a starting point for more information on web application security would include

* OWASP Top Ten
* OWASP Countermeasures Reference
* OWASP Application Security FAQ
* Build Security In (Dept. of Homeland Security, National Cyber Security Division)
* Web Application Vulnerability Scanners (National Institute of Standards and Technology)
* Web Application Firewall Evaluation Criteria (Web Application Security Consortium)


[Trey Ford of Security Spin Control](http://treyford.wordpress.com/) has a [fairly good explanation](http://treyford.wordpress.com/2008/04/22/pci-66-information-supplement-released/) of the recently released [PCI information supplement on requirement 6.6](https://www.pcisecuritystandards.org/pdfs/infosupp_6_6_applicationfirewalls_codereviews.pdf).

SC Magazine also has an article on [Deconstructing PCI 6.6](http://www.scmagazineus.com/Deconstructing-PCI-66/article/110013/) for the management folks.



### 7. Data Breaches - How do you protect my data from insider breaches?



In the [Verizon Business breach report blog](http://securityblog.verizonbusiness.com/2008/06/10/2008-data-breach-investigations-report/), Verizon Business stated that



> While criminals more often came from external sources, and insider attacks result in the greatest losses, criminals at, or via partner connections actually represent the greatest risk. This is due to our risk equation: Threat X Impact = Risk
>   * External criminals pose the greatest threat (73%), but achieve the least impact (30,000 compromised records), resulting in a Psuedo Risk Score of 21,900
>   * Insiders pose the least threat (18%), and achieve the greatest impact (375,000 compromised records), resulting in a Pseudo Risk Score of 67,500
>   * Partners are middle in both (73 39% and 187,500), resulting in a Pseudo Risk Score of 73,125




Many SaaS advocates claim that SaaS providers can do a better job at protecting the customers' data. Unfortunately, just because the data is now in the cloud, it does not reduce the risk of insider breaches. Insiders still have access to the data, they are just accessing it a different way. Just because the data is in the cloud, the responsibility of segregation of duties and access authorization still fall on the customers, not the SaaS or cloud computing providers. So yes, it may reduce the chance of insiders getting direct access to, say, a database, it does not in any way reduce the risk of insider breaches. In fact, it may even increase the possibility as you now have to take into consideration of the cloud or SaaS providers’ employees. They have access to a lot more information and a single incident could expose information from many customers.

SaaS providers should be prepared to answer questions on what tools and processes are utilized to ensure segregation of duties and protect from insider breaches. Remember, in the case of the mult-billion dollar insider incident at Société Générale, IT management had implemented all of the controls recommended by auditors, but nobody was monitoring them. So it's extremely critical to be able to show the processes around these security controls.



### 8. PCI DSS - Are you compliant with PCI DSS?



PCI DSS has a specific section for hosting providers (including SaaS providers):

> **Requirement A.1: Hosting providers protect cardholder data environment**

As referenced in Requirement 12.8, all service providers with access to cardholder data (including hosting providers) must adhere to the PCI DSS. In addition, Requirement 2.4 states that hosting providers must protect each entity’s hosted environment and data. Therefore, hosting providers must give special consideration to the following: 

A.1 Protect each entity’s (that is merchant, service provider, or other entity) hosted environment and data, as in A.1.1 through A.1.4: 

>   1. A.1.1 Ensure that each entity only has access to own cardholder data environment 
>   2. A.1.2 Restrict each entity’s access and privileges to own cardholder data environment only 
>   3. A.1.3 Ensure logging and audit trails are enabled and unique to each entity’s cardholder data environment and consistent with PCI DSS Requirement 10 
>   4. A.1.4  Enable processes to provide for timely forensic investigation in the event of a compromise to any hosted merchant or service provider. 

A hosting provider must fulfill these requirements as well as all other relevant sections of the PCI DSS. Note: Even though a hosting provider may meet these requirements, the compliance of the entity that uses the hosting provider is not necessarily guaranteed. Each entity must comply with the PCI DSS and validate compliance as applicable. 




Simply put, SaaS providers must be compliant with PCI DSS in order to host merchants that must comply with PCI DSS. 



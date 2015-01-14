+++
Categories = ["log"]
date = "2004-11-19T09:39:12+00:00"
title = "Regex-less Parsing of Messages"
+++


A very [interesting and useful discussion](http://lists.shmoo.com/pipermail/loganalysis/2005-December/date.html) took place the last week on the [LogAnalysis mailing list](http://lists.shmoo.com/pipermail/loganalysis/).

[Anton Chuvakin](http://www.chuvakin.org/) started the thread by [asking](http://lists.shmoo.com/pipermail/loganalysis/2005-December/002906.html) other than parsing the individual messages (that could potentially have thousands of different formats), what other methods can be used in analyzing logs?

Some suggestions out of this discussion are listed here.
 


### Clustering



Anton listed this as an option using tools such as [slct](http://www.estpak.ee/~risto/slct/). Another effort that I am aware of that's using this approach is [Securimine for Snort (SFS) from Securimine](http://www.securimine.com/).

Securimine is founded by Ophir Rachman, who also founded [Entercept Security Technologies](http://www.mcafee.com/us/products/mcafee/host_ips/category.htm) (later on acquired by McAfee).



### Brute-force Parsing



This method basically tries to guess some of the data structures inside a log message, such as IP address, hostname, username, password, action, etc etc. 

Being able to correctly guess what data is a message without first knowing the message format is a tough problem. It relies on the parser knowing the exact structure of some of the data. 

However, it can still be used to assist in parsing unknown messages. You can also apply some simple logics to classify the messages. Such as, if you see keywords such as from or to and IP addresses, that may be a firewall message.

Obviously this is not a fool-proof way, but given the alternative (not doing anything with the message at all!), it is a viable solution. 

(One may ask the question of, is it better to not do anything so the users won't be misled? or is it better to attempt in guessing and possibly give the wrong information? what do you think?)



### Bayes/Markov/Expert Systems/Neural Nets/Genetic Algorithms

Several of the statisitical type of analysis were mentioned here. 

1. Expert system  - a collection of empirical data and decision algorithms compiled by developers
2. Hidden Markov models - since they are used in natural language and speech processing they might be applicable to log entries (they are after all some type of  "natural speech").
3. Neural nets - Once built, the neural net would be trained by experienced teachers (log analysis gurus).
4. Genetic algorithms - The trick would be to 1. define the right requirements (for example, determine the least number of message types without discarding significant data) and 2. define the genetic codes for the solution organisms. Maybe GAs are a bit far fetched but I wouldn't exclude them.
5. Bayes - Bayesian classifiers have been extremely popular and successful in spam filtering. The success of baysian in spam filtering is partly due to the simplicity of classifying emails into ham and spam. In the log world, it is much tougher to tell from good to bad. Also, lots of not-bad messages may also indicate something bad. So it is tough to say how one can apply this type of technology to log analysis.

Obviously I am no mathematician nor do I claim to understand the nitty-gritty details of statistical analysis, so I can't comment much on the technical merit of these methods. But love to hear from anyone who have more knowledge.

### Indexing

One of the newer methods of analyzing logs is indexing and providing Google like search capabilities for all logs. This is something [LogLogic](http://www.loglogic.com) and [Splunk](http://www.splunk.com) are doing. 

The basic idea is that instead of parsing the messages by understanding every single format, use the full-text indexing approaches to break the messages into tokens, then allow users to use boolean search expressions to search the logs. 

This method is great when it comes to troubleshooting and forensic analysis. If complemented with the understanding of the log formats, it can be as powerful as other methods.

I wrote an article on [Searching for Root Cause](http://www.computerworld.com/developmenttopics/development/webservices/story/0,10801,105905,00.html) a while back on the benefit of using Google-like indexed search on logs.



### Tokenizing



This is the way most log analyzers are using today. This method generally require writing regular expressions or similar methods to parse the individual pieces of information out of the log messages.

Rainer Gerhards has a great summary in his paper [On the Nature of Syslog Data](http://www.monitorware.com/en/workinprogress/nature-of-syslog-data.php).



### Various standards



[About Windows Event Log](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/wes/wes/about_the_windows_event_log.asp)

[IBM's Common Base Event XML format](http://www-128.ibm.com/developerworks/autonomic/library/ac-cbe1/) - This is a VERY complicated XML based format that tries to cover everything. I see two huge problem with this type of format. First, it hugely expands the storage requirement given that raw log storage is required. Second, it could make parsing that much slower given the size of a single log (multiple KBs instead of hundres of bytes). It's been morphed into the [OASIS standard WSDM Management Using Web 
Services v1.0 (WSDM-MUWS)](http://www.oasis-open.org/committees/tc_home.php?wg_abbrev=wsdm) .

[RFC 3881 - Security Audit and Access Accountability Message XML Data Definitions for Healthcare Applications](http://www.faqs.org/rfcs/rfc3881.html)

WELF

W3C

IDMEF - Intrusion Detection Message Exchange Format

IDIOM - Intrusion Detection Interaction and Operations Messages (Cisco message format)

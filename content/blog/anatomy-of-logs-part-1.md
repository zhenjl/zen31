+++
Categories = ["log"]
date = "2004-12-15T04:54:28+00:00"
title = "What's In A Log: Part 1"
+++

Much ink has been spilled all over the web and in print writing about log management and analysis. Google returned over 640,000 hits for the search '["log management" OR "log analysis"](http://www.google.com/search?hl=en&lr=&c2coff=1&q=%22log+management%22+OR+%22log+analysis%22&btnG=Search)'.

A whole technology segment has been created just for this purpose. IDC and Gartner both predicted that the log management space will be over $500M the next couple of years.

Many Global 2000 corporations have started log management projects, mostly driven by regulatory or standards compliance. Public companies have to be SOX compliant. Healthcare companies have to be HIPAA compliant. Financial companies have to be FFIEC or Basel II compliant. Government agencies have a whole list of federal and state regulations and standards they have to compliant with.

Yet many people are still wondering why they should look at logs.

What are logs? What's in them? What makes them so important to the world of IT performance, availability, troubleshooting, security and regulatory compliance?

To best understand how logs affect all areas of IT management, it is necessary for us to dissect the logs and see what information they provide.


### What's in a log

Firewalls probably generate the most logs amongst all devices. A busy PIX firewall, with debug logging turned on, can generate 2,000 to 3,000 messages per second (MPS).


```
%PIX-6-302013: Built inbound TCP connection 543127891 for 
outside:192.168.11.250/41612 (192.168.11.250/41612) to 
inside:10.1.241.2/80 (10.1.241.2/80)
```    

This is a fairly typical log message from a PIX firewall. Most administrator will probably ignore these logs as there are a ton of them. However, let's look closely to see what information we can find.

#### %PIX

This first 4 characters immediately tells us that the log message is a PIX message. With this information, if you are writing a parser for multiple log types, you can throw this over to the PIX parser and go on to the next message. You can also use this to classify or categorize your logs based on device type.

#### -6-

The dashes are just delimiters so we will ignore them for now.

The number "6" is interesting for us because it tells us the severity level of the message. 6 in this case means Informational. Other levels are 0 (Emergency), 1 (Alert), 2 (Critical), 3 (Error), 4 (Warning), 5 (Notification) and 7 (Debug).

These 7 severity levels are fairly standard in the syslog world. Almost all devices and applications logging via syslog will follow these severity levels.

In any case, Informational messages are usually harmless in that they don't require our immediate attention. However, **excessive** of informational messages may indicate something suspicious and will need drilling down.

#### 302013:

This number represents the message ID of the PIX message. It gives us an idea what information we will find in the remainder of the message, as well as the format of the message. 

The message ID is extremely useful in a distribution report. A distribution report shows us the count of each message time over a specific period of time. Tracking that information over time, we can discover things that we cannot see by looking at individual messages. 

For example, if we track the daily distribution count of the message types over a course of a month, we may see that our average wednesday count for message type 302013 is around 5 million. If one wednesday we saw a count of 6 million, we might suspect that something anomalous is going on. The 1 million messages averages out to be about 11 per second, which is probably not high enough to trigger any alerts on its own. 

If we didn't track the distribution report over a longer period, we would probably have missed the 1 million message increase as well.

We will ignore the colon as it doesn't represent anything important.

#### Built

This is probably one of the most important words of the whole message as it tells us the action that the firewall took.

The word "Built" tells us that the connection has been accepted based on the security policy and the PIX firewall is going to create a tunnel (figuratively) from the outside world to the inside of the firewall.

Other firewalls may use the words "accept" or "allow" to represent the same information.

Most log management products will normalize this into "accept." By doing so, we can run reports across many different firewall types and identify trends and anomalies. 

It is also important in the compliance world to track all access by users and machines. For example, the SOX regulation requires that all access to financial systems be logged and reviewed. In this case, successful connections should be reviewed periodically to see whether users accessing the financial systems are authorized.

Because majority of our logs probably contain this type of information, it's generally a bad idea to use it in a real-time correlation rule. It will overwhelm your correlation engine in no time. However, thresholds can be set using this, probably along with the source or destination information (see below).

#### inbound

In this PIX message, the words "inbound" and "outbound" may appear here. "Inbound" tells us that the original connection was initiated from outside of the firewall. Vice versa, "outbound" means that the original connection was initiated from inside of the firewall.

This word is significant for several reasons.

First of all, if we see the word "inbound" in a message, but the connection is initiated from the inside, or "outbound" connection initiated from the outside, then immediately we know something weird is going on. It could mean that there's a mis-configuration, or a bug in the PIX software :). It's worth an investigation nonetheless.

Secondly, if we run a firewall that normally doesn't allow "inbound" connections, and all the sudden we are seeing them in our logs, we would want to drill down and investigate what's happening. Some administrator may have accidentally opened the firewall to the inside for some reason. Whatever it may be, two questions should be answered. First, why did the administrator open up the firewall? And second, why did she leave it open? We may also want to setup alerts based on this scenario.

Last but not least, we can run a distribution report as we did with the message ID and track it over time. Any sudden increase (or even decrease) in the count may be worth checking into.

#### TCP

TCP stands for Transmission Control Protocol. It is used by many internet services such as HTTP, SMTP, FTP, SSH, etc. By itself, the word "TCP" isn't all that interesting. However, the protocol and the destination port together determines the service that the connection is for. For example
   
    
    shell           514/tcp
    syslog          514/udp
    



As we can see, the port number for these two services are the same, 514. However, the "shell" service uses TCP and "syslog" uses UDP. Without the protocol, we would have not been able to determine the service.

Most log management systems don't have reports defined for the common protocols such as TCP or UDP. It might, however, be interesting to track the uncommon ones, if you run anything weird.

#### connection 543127891 for

We will skip the words "connection" and "for".

The number, 543127891, is a unique number that represents this specific session inside the PIX's connection table. It is used to track information such as duration and bytes transferred for this connection. These information will become available in another message (ID 302014), once the connection is closed.

Information such as duration and bytes transferred can be extremely valuable for performance and utilization tracking. We will go over these in more details in Part 2 of Anatomy of Logs.

#### outside:

We will skip the colon.

The word "outside" represents the source interface of the PIX firewall. It is the interface where the connection is originally initiated. Other firewalls may use the word "zone" to describe this.

Having this information allows us to quickly map the network from the logs. For example, we can easily identify all the IPs that are "outside" of the firewall vs "inside" of the firewall. If we identified IPs that have appeared both "outside" and "inside", it may be a cause for concern: there maybe a backdoor out of your network. We have seen this happen many times on bridged networks. It is probably one of the weirdest scenarios in network troubleshooting as it leaves you scratching your head trying to figure out where/what the backdoor is.

#### 192.168.11.250/41612 (192.168.11.250/41612)

This whole section here shows the source IP address and port of the connection. In this case, the source IP is 192.168.11.250 and the source port is 41612. There are two parts to this section. The first are the "real" IP and port, before any translation is done. The second part, inside the parenthesis, are the mapped IP and port, after the network address translation is applied. 

For firewalls with no NAT, these two should be exactly the same. For "inbound" connections from the outside, these two are probably the same as well. However, if you, for whatever wacky reason, decide to NAT incoming traffic, then these will be different. (Ok, so maybe not wacky, I have seen people who have a second layer of firewall, something about defense-in-depth or some wacky idea like that ;), that will only accept connections from a single source IP. So in this case, NAT might be used.)

The source port is generally not significant; however, in specific scenarios, it may indicate an exploit attempt. For example, [BEWARE ftp clients from SOURCE PORT 1](http://www.dshield.org/pipermail/intrusions/2003-April/007503.php)!

In other cases, it may indicate the the source host is using network address translation. E.g. PIX firewalls' Port Address Translation uses ports to track the connections, so it's possible that port 1 is used.

There's all kinds of reports that can be generated from the source IP address. We can track




  * how often the IPs visit our site by doing a summary report over time


  * which company/domain/country visit our site by performing a reverse DNS looking (or whois) and summarizing


  * which IPs are attempting to scan our network by summarizing the destination IP/ports (see below) attempted





#### inside:



This represents "inside" of the firewall, or the internal network. It is similar to the "outside" interface as described above. 



#### 10.1.241.2/80 (10.1.241.2/80)



This section describes the destination IP and port of the connection. The first part shows the original, or untranslated, IP and port. The second shows the translated, or mapped, IP and port. For networks that use NAT, these two parts will be different. 

The IP address, 10.1.241.2, shows the destination of the connection. 

The destination port, 80, unlike the source port, is very significant. Together with the protocol (see above), the port will tell us exactly what service is being requested. In this case, port 80 of protocol TCP is HTTP, which means this connection is requesting a web server connection.

Just like the source IP, many reports can be generated for the destination IP and ports. For example,




  * what are the most accessed servers


  * what are the most requested services


  * what are the most denied servers and/or services


  * what's the distribution of servers and services over time



As before, seeing a distribution over time will tell us whether we are getting more traffic and whether we should consider upgrading our servers to handle the additional load. Trend analysis is very important for most IT shops.

One of the more interesting reports to see is "what are the LEAST requested services or servers?"

When hackers install a backdoor on your system, they don't normally make a lot of noises by connecting to it a thousand times. They try to hide their tracks by connecting at odd hours and very infrequently. So seeing the least requested service may actually tell you if there's any backdoor activities.



### What about the time



At this point you are probably wondering, "where does it tell me when this log was generated?!"

Unfortunately, most logs generated by devices do not include the time. The devices depend on the log management server to include the time when the log is received. So most of the time when you see the time stamp in front of a log, it's the server's time, not the device time.

In some cases, such as the PIX, the device will allow you to send the time as well. In that case, you will see something like this:


    
    
    Apr 30 2004 08:23:36: %PIX-6-302013: Built inbound TCP connection 543127891 for 
    outside:192.168.11.250/41612 (192.168.11.250/41612) to 
    inside:10.1.241.2/80 (10.1.241.2/80)
    



---

As you can see, there's a wealth of information in just a single log message. Next time, we will take a look at the corresponding Teardown message in PIX.

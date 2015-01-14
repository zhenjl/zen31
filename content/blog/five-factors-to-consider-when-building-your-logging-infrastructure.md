+++
Categories = ["log"]
date = "2004-11-19T09:39:12+00:00"
title = "Five Factors to Consider When Building Your Logging Infrastructure"
+++


Whether you are building your own home-grown logging infrastructure (which of course I do not recommend ;)) or evaluating a log management solution, there are at least five factors you should consider.



### 1. Log Retention



The log retention period obviously depends on your requirements. If you are building out the infrastructure for troubleshooting and short term reporting, you may only need to keep 1-2 months of logs. But if you are doing it so you can be in compliance with SOX or HIPAA regulations, you will need to keep AT LEAST 6 months for the auditors.

As a rule of thumb, if your requirement is regulatory compliance, make the retention period 12 months to be safe. If you can afford it or the product can support it, go even longer. 

Obviously how long your retention period is also depend on the volume of logs you receive as well as the product/tool's ability to manage the log storage. If you are building your own, be sure to take into consideration of building a log rotation process. For example, if your retention period is 12 months. Your process should remove the old logs or put them on tape. If you are evaluating a product, be sure the product has the capability of rotating/purging old logs for you. Don't spend $200K and then have to write your own scripts.



### 2. Log Volume



Log volume is probably one of the most critical factors in building your infrastructure. It has direct impacts on your retention policy, report/search performance, aggregation performance and correlation performance.

Vendors talk about log volumes in many ways but it all comes down to the number of log message per second you receive. With that number in hand, you can calculate how much storage space you will need. For example, if your log message rate is 2000/second, assuming 200 bytes per message (which is fairly normal), we have

2000 * 3600 * 24 = 172.8 million messages / day 
172.8M * 200 bytes =~ 33GB / day * 30 days = ~100GB / month

That's quite a bit of data. This exercise brings up a few things you should be aware of.

First, you need a product or develop a solution that can handle the message rate that your environment generates. In this example, get something that can handle at least 3000 messages per second: 2000 for your requirement, another 30% for growth and possible spikes. If you are evaluating a product, test it to make sure it doesn't drop any of your logs due to performance issues of the software/appliance.

Second, you need something that will compress the log archives. With 100GB/month, your storage requirement will go through the roof!! Even gzip will give you atleast 10:1 compression on the logs. 

Third, note how I used a 200 byte per message? Well, if you parse it and put it in a database, the storage requirement per message will increase. For example, ArcSight uses a 2KB/message for their calculations. That basically takes the 1 month retention storage requirement to over 1TB! Ask your vendors or do your own calculation on what the **REAL** storage requirement is. Make sure the product you are looking at has enough storage space for your retention policy. 

Last but not least, your log volume really impacts the performance of the product you choose. Some of the products, as the volume grow in the database, will have problem running reports for a long period of time. If you need to run a report for over a month or two, sometimes it may take hours for a single report. It's difficult to test this during a evaluation period, but many of the implementations fail because of this.



### 3. Log Sources



What are all the devices, servers and applications that will be logging? If you are developing your own solution, there may be a lot of work for you to do in order to parse the various log messages. The good thing is you will only need to parse the specific logs you need and not everything.

There are many different logging methods (file, database, syslog, proprietary) and formats (single-line, multi-line, XML, database records).

Most vendors will show you a list of all the logs their product will support. Some vendors will support 100's of log sources across many different categories, such as firewalls, routers, switches, IDSes, web servers, mail servers, access control software, operating systems, etc etc etc.

Make sure the product you are looking at supports all your log sources. If not, make sure that there's a way for you to develop new parsers for it. Most of the time it will just be some regular expression for parsing logs.

Make sure the product will support some of the native logging methods and formats. For example, Check Point logs can be retrieved via the LEA protocol and Cisco IDS via RDEP. Windows event logs are just a pain in the butt if your central log retriever is a non-windows platform. 

Some products will accept **ANY** log even if it doesn't parse them. That will allow you to archive the logs and do some rudimentary search and alerts on them, but not do detailed reports.

However, some products will hardcode the parsers in their code and no way for you to create any new parsing intelligence. Beware of what you are getting into if that's the product you are looking at.



### 4. Log Analysis



Ok, so this is a huge area. Log analysis includes everything from reports, correlation, anomaly detection, and trend analysis. It again depends on your requirements. However, your solution or product should have some of the basic functions such as threshold and rule-based alerts via email or SNMP.

Most vendors will provide pre-defined reports that covers the Top N reports across most of the log sources they support. The pre-defined reports are basically the intelligence of the products. Without them, the product is basically useless and you will need to spend a lot of time configuring it instead of using it.

Log analysis can cover many different areas, including security incidents detection, virus infected machines discovery, device/application up/down, usage analysis and capacity planning. Most of the SIM products basically focus on just security incidents detection. If your requirement is not just security, make sure the products can handle it.

Report and correlation performance is a critical factor. If reports takes hours, it'd be somewhat useless when you need a quick ad-hoc report to figure out which IPs are DOSing you. Build your infrastructure w/ at least 30% more performance than you need. That way you have some room to grow and also allow you to do quick reports when you are receiving a spike of logs.



### 5. Network Topology



Your network topology impacts how you should architect your logging infrastructure. If you have a fairly distributed topology, e.g. many remote locations, you will want to design a solution or look for a product that have a distributed architecture, that can retrieve/receive logs in a distributed manner and forward logs back to a central location for analysis and archival.

If you just have a single central location (I can't imagine anyone having that kind of infrastructure these days), you can probably get away with a product that can't be architected in a distributed manner.

Ok, so here comes the downside of distributed architecture. Price! Any additional component you add will cost you. Be sure to check w/ the vendors to see how much it will REALLY cost. Also, some of the smaller devices vendors provide for remote locations can handle a lower message rate, make sure the ones you choose for each location can meet the requirement and have some room to grow.

---

I hope this helps you in understanding what's needed to build your logging infrastructure. Please let me know if you have any questions or comments.

P.S. I would love to see a review of log management products w/ these 5 factors in mind and actually score the products for each factor. 

+++
Categories = ["IT"]
date = "2005-06-22T06:17:29+00:00"
title = "IT Problem Management Process"
+++


These are scary figures that are sure to keep all CIOs, IT directors and managers up at night. According to the report, The Cost of Enterprise Downtime, North America 2004, conducted by Infonectics Research, network downtime is costing companies 3.6 percent of annual revenue. After studying over 80 large corporations, Infonectics Research found that companies experience an average of 501 hours of network downtime per year. This adds up to millions of dollars of lost productivity and revenue.

Each year, millions of dollars are invested in various technologies to attempt to solve IT infrastructure problems faster so companies can reduce downtime. However, these companies are no closer to the Holy Grail of automated root-cause analysis and problem resolution.

In order to understand why thats the case, it is necessary to understand the process of IT problem management. There are generally five steps in the problem management process: detection, identification, determination, resolution, and reflection.



### Detection



The ability to detect whats happening in your infrastructure is a crucial first step in managing problems. Is your router or switch down? Is your web server or email server down? Is your network connection degraded? Is someone intruding your network or servers? Has someone transferred intellectual property out of your network?

Most of the technologies we have seen in the past five to ten years have been designed to solve the problem of detection. Network Management Systems (NMS) such as IBM Tivoli, HP OpenView, CA Unicenter and many others were first designed to monitor the enterprise infrastructure by polling network devices and servers periodically. When the polling fails for a predetermined number of times, a problem is detected and an alert is sent to the administrators. In the security world, network and host intrusion detection systems (IDS) have been developed to identify problems on the network and servers. 

All the technologies, however, are designed for detection but cannot tell you where the actual cause of the problem might be nor can it tell you what caused the problem to occur.



### Identification



Given that most of the technologies only perform detection, IT administrators must spent a lot of their time in identifying where the problem has actually occurred. These IT administrators utilize the most basic network tools such as ping and traceroute, rely on domain knowledge of their own network to perform process of elimination, or analyzing network traffic using sniffers to help determine the actual location of the problem. 

To accelerate the process, some companies have developed technologies in the attempt to identify where the problem actually occurred. One such example is EMC Smarts. Smarts starts by mapping out an infrastructure using various automated tools as well as human knowledge. The mapping will identify, for example, which switch ports are connected via the same cable or what servers are behind the same router or switch. Once the mapping is complete, Smarts will utilize its proprietary Codebook Correlation Technology, SNMP traps and log messages from routers/switches/servers to identify where the fault or problem may have occurred.  



### Determination



Even though some of these newer technologies may help IT administrators identify where the problem might be, they are still very limited in determining the actual root cause. Why did my web server go down? Was it due to memory corruption? Was it due to a security exploit? Was it due to misconfiguration? Why is my network so slow? Is it because of a router or switch interface mismatch? Is it because someone is transferring a movie over the wire?

There is no doubt that problem determination is the most difficult stage of the problem management process. As any experienced IT administrators will confirm, majority of the troubleshooting time are in determining exactly whats causing the problem to happen. 

However, even today, IT administrators must manually perform root-cause or forensic analysis by digging through mountains of log files or analyzing seas of traffic packets. No technologies have been developed to help IT administrators to automate the determination process. 



### Resolution



Once the problem has been identified and root cause has been determined, IT administrators can most of the time fix the problem quickly, e.g., fix the interface mismatch or restart the web server. There are obviously some problems that require long-term resolution such as fixing the memory corruption of applications or upgrading the network bandwidth due to increase in number of users. 

Some companies have also developed technologies that jump from problem identification to resolution, skipping the determination stage. These automated resolutions can range from simply blocking an offending IP by modifying router, switch or firewall configurations to executing a program or script to perform much more complex instructions. 

This type of technology can be extremely dangerous as mistakes can lead to the network or infrastructure to become unavailable. Intruders may also be able to exploit these automated resolution mechanisms to perform Denial-of-Service attacks against the IT infrastructure.



### Reflection



Reflection, or post mortem is probably one of the most important stages in this whole process. The idea of reflection is that IT administrators should take time to

* Document the process of detection, identification, determination and resolution
* Determine how to prevent same problems from happening in the future
* Identify and resolve other similar problems
* Review the whole process to see how it can be improved

It is no wonder that enterprises are losing millions of dollars due to infrastructure downtime. As we can see, most of the current technologies are designed to help with the detection stage of the problem management process; few technologies have been developed to help IT administrators to identify where the problem has occurred; but no technologies have been developed to automate the process of determining the root-cause. 

Root-cause and forensic analysis are very difficult problems to solve. Hopefully in the near future we will see new technologies in this area to make IT administrators life easier.

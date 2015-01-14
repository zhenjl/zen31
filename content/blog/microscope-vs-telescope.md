+++
Categories = ["log"]
date = "2004-11-06T17:47:32+00:00"
title = "Microscope vs. Telescope"
+++

Any good log analysis software should be able to provide two different views: microscopic and telescopic.

Under a **microscope**, the user should be able to see all the nitty-gritty details of an event or incident. An event under a microscope should show details of the fields that makes up that event. For example, if you are looking at a network connection of a firewall event under the microscope, the view should give you the source host, destination host, source port, destination port, and any other information that came with the connection.

If you are looking at an incident under a microscope, the view should show you all the events that made up the incident. The events can come from different devices, such as firewall, IDS, routers, switches, or applications such as web/application servers, databases, or operating systems such as Windows or Linux. From that view, you can examine each event under a microscopic view as well.

Under a **telescope**, the user should be provided a high level view of the infrastructure. It may be that the highest level view is a world map of your infrastructure. From there, you can drill down to each site, then each machine, each application, each incident, each event. 

Another type of telescopic view may be a graph, e.g. a line graph showing the connection count of a device over a day/week/month period. From this telescopic view, if one sees something abnormal, such as a spike in connection count, one can select that time period and drill down to find out what makes up the spike. For example, the following graph is a graph of connections of a device over a year.

![Firewall Connection Graph](http://www.trustpath.com/logmatters/wp-content/fw_conns.png)

Yet another type of telescopic view may be a attack pattern graph showing all the alerts you have received from the various IDS sensors. You can then select a specific attack to drill down to view all the events that made up the attack. The following example shows a list of hosts attacking a single one. The number shows the number of attacks and the color shows the standard deviation.

![Attack Pattern Graph](http://www.trustpath.com/logmatters/wp-content/attack_pattern.jpg)

The ability to transition from a telescopic view to a microscopic view is extremely important to any log analysis software. Imagine being able to select a portion of the "Firewall Connection Graph" and drill down to the events or click on the "Attack Pattern Graph" and bring up the attacks from a specific host.

As you are evaluating various tools and products for your environment, 




  * Ask the vendor to see if they provide that capability


  * Use to the software to see how easy it is to drill down


  * Compare the products and tools to see if they give you the same results



Think Microscope == Details and Telescope == Trends, Graphs, Charts, Summaries.

Side Note: I borrowed the terms **Microscope** and **Telescope** from [Guy Kawasaki](http://www.guykawasaki.com)'s new book. I started reading [The Art of the Start](http://www.guykawasaki.com/books/) couple of nights ago and found it to be one of the best **practical** books for entrepreneurs. You can find favorable reviews of the book almost everywhere. Just [Google It](http://www.google.com).


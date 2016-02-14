+++
categories = [ "code" ]
date = "2016-02-14T10:57:56-08:00"
title = "A Modern App Developer and An Old-Timer System Developer Walk Into a Bar"
+++

[Hacker News Discussion](https://news.ycombinator.com/item?id=11099925), please feel free to upvote!

<i class="fa fa-heart"></i> <i class="fa fa-heart"></i> Happy Valentine's Day! <i class="fa fa-heart"></i> <i class="fa fa-heart"></i>


A modern app developer and an old-timer system developer walk into a bar. They had a couple drinks and started talking about the current state of security on the Internet. In a flash of genius, they both decided it would be useful to map the Internet and see what IPs have vulnerable ports open. After some discussion, they decided on the following

* They will port scan all of the IPv4 address (2^32=4,294,967,296) on a monthly basis
* They will focus on a total of 20 ports including some well-known ports such as FTP (20, 21), telnet (23), ssh (22), SMTP (25), etc
* They will use nmap to scan the IPs and ports
* They need to store the port states as [open, closed, filtered, unfiltered, openfiltered and closedfiltered](https://nmap.org/book/man-port-scanning-basics.html)
* They also need to store whether the host is up or down. One of the following two conditions must be met for a host to be "up":
  * If the host has any of the ports open, it would be considered up
  * If the host responds to ping, it would be considered up
* They will store the results so they can post process to generate reports, e.g.,
  * Count the Number of "Up" Hosts
  * Determine the Up/Down State of a Specific Host
  * Determine Which Hosts are "Up" in a Particular /24 Subnet
  * Count the Number of Hosts That Have Each of the Ports Open
  * How Many Total Hosts Were Seen as "Up" in the Past 3 Months?
  * How Many Hosts Changed State This Month (was "up" but now "down", or was "down" but now "up")
  * How Many Hosts Were "Down" Last Month But Now It's "Up"
  * How Many Hosts Were "Up" Last Month But Now It's "Down"

## Modern App Developer vs Old-Timer Developer

Let's assume 300 million IPs are up, and has an average of 3 ports open.

* _**How would you architect this?**_
* _**Which approach is faster for each of these tasks?**_
* _**Which approach is easier to extend, e.g., add more ports?**_
* _**Which approach is more resource (cpu, memory, disk) intensive?**_

_Disclaimer: I don't know ElasticSearch all that well, so feel free to correct me on any of the following._

### Choose a Language

Modern App Developer: 
	
> I will use Python. It's quick to get started and easy to understaind/maintain.


Old-Timer Developer: 

> I will use Go. It's fast, performant, and easy to understand/maintain!

### Store the Host and Port States

Modern App Developer: 

> I will use JSON! It's human-readable, easy to parse (i.e., built in libraries), and everyone knows it!

```
{
	"ip": "10.1.1.1",
	"state": "up",
	"ports": {
		"20": "closed",
		"21": "closed",
		"22": "open",
		"23": "closed",
		.
		.
		.
	}
}
```

> For each host, I will need approximately 400 bytes to represent the host, the up/down state and the 20 port states.
>
> For 300 million IPs, it will take me about 112GB of space to store all host and port states. 

Old-Timer System Developer: 

> I will use one bit array (memory mapped file) to store the host state, with 1 bit per host. If the bit is 1, then the host up; if it's 0, then the host is down.
>
> Given there are 2^32 IPv4 addresses, the bit array will be 2^32 / 8=536,870,912 or 512MBs
>
> I don't need to store the IP address separately since the IPv4 address will convert into a number, which can then be used to index into the bit array.
>
> ---
>
> I will then use a second bit array (memory mapped file) to store the port states. Given there are 6 port states, I will use 3 bits to represent each port state, and 60 bits to represent the 20 port states. I will basically use one uint64 to represent the port states for each host.
>
> For all 4B IPs, I will need approximately 32GB of space to store the port states. Together, it will take me about 33GB of space to store all host and port states. 
>
>I can probably use [EWAH bitmap compression](/blog/bitmap-compression-using-ewah-in-go/)
 to gain some space efficiency, but let's assume we are not compressing for now. Also if I do EWAH bitmap compression, I may lose out on the ability to do population counting (see below). 

### Count the Number of "Up" Hosts

Modern App Developer:

> This is a big data problem. Let's use Hadoop!
>
> I will write a map/reduce hadoop job to process all 300 million host JSON results (documents), and count all the IPs that are "up".
>
> ---
>
> Maybe this is a search problem. Let's use ElasticSearch!
>
> I will index all 300M JSON documents with ElasticSearch (ES) on the "state" field. Then I can just run a query that counts the results of the search where "state" is "up".
>
> I do realize there's additional storage required for the ES index. Let's assume it's 1/8 of the original document sizes. This means there's possibly another 14GB of index data, bringing the total to 126GB.

Old-Timer System Developer:

> This is a [bit counting](https://github.com/zhenjl/bitmap/blob/master/ewah/bitcounter.go#L69), or _popcount()_, problem. It's just simple math. I can iterate through the array of uint64's (~8.4M uint64's), count the bits for each, and add them up!
>
> I can also split the work by creating multiple goroutines (assuming Go), similar to map/reduce, to gain faster calculation.

### Determine the Up/Down State of a Specific Host

Modern App Developer:

> I know, this is a search problem. Let's use ElasticSearch!
>
> I will have ElasticSearch index the "ip" field, in addition to the "state" field from earlier. Then for any IP, I can search for the document where "ip" equals the requested IP. From that document, I can then find the value of the "state".

Old-Timer System Developer:

> This should be easy. I just need to index into the bit array using the integer value of the IPv4, and find out if the bit value is 1 or 0.

### Determine Which Hosts are "Up" in a Particular /24 Subnet

Modern App Developer:

> This is similar to searching for a single IP. I will search for documents where IP is in the subnet (using CIDR notation search in ES) AND the "state" is "up". This will return a list of search results which I can then iterate and retrieve the host IP.
>
> Or
>
> This is a map reduce job that I can write to process the 300 million JSON documents and return all the host IPs that are "up" in that /24 subnet.

Old-Timer System Developer:

> This is just another bit iteration problem. I will use the first IP address of the subnet to determine where in the bit array I should start. Then I calculate the number of IPs in that subnet. From there, I just iterate through the bit array and for every bit that's 1, I convert the index of that bit into an IPv4 address and add to the list of "Up" hosts.

### Count the Number of Hosts That Have Each of the Ports Open

For example, the report could simply be:

```
20: 3,023
21: 3,023
22: 1,203,840
.
.
.
```

Modern App Developer:

> This is a big data problem. I will use Hadoop and write a map/reduce job. The job will return the host count for each of the port.
>
> This can probably also be done with ElasticSearch. It would require the port state to be index, which will increase the index size. I can then count the results for the search for ports 22 = "open", and repeat for each port.

Old-Timer System Developer:

> This is a simple counting problem. I will walk through the host state bit array, and for every host that's up, I will use the bit index to index into the port state uint64 array and get the uint64 that represents all the port states for that host. I will then walk through each of the 3-bit bundles for the ports, and add up the counts if the port is "open".
>
> Again, this can easily be paralleized by creating multiple goroutines (assuming Go).

### How Many Total Hosts Were Seen as "Up" in the Past 3 Months

Modern App Developer:

> I can retrieve the "Up" host list for each month, and then go through all 3 lists and dedup into a single list. This would require quite a bit of processing and iteration.

Old-Timer System Developer:

> I can perform a simple AND operation on the 3 monthly bit arrays, and then count the number of "1" bits.


### How Many Hosts Changed State This Month (was "up" but now "down", or was "down" but now "up")

Modern App Developer:

> Hm...I am not sure how to do that easily. I guess I can just iterate through last month's hosts, and for each host check to see if it changed state this month. Then for each host that I haven't checked this month, iterate and check that list against last month's result. 

Old-Timer System Developer:

> I can perform a simple XOR operation on the bit arrays from this and last month. Then count the number of "1" bits of the resulting bit array.

### How Many Hosts Were "Up" Last Month But Now It's "Down"

Modern App Developer:

> I can retrieve the "Up" hosts from last month from ES, then for each "Up" host, search for it with the state equals to "Down" this month, and accumulate the results.

Old-Timer System Developer:

> I can perform this opeartion: `(this_month XOR last_month) XOR last_month`. This will return a bit array that has the bit set if the host was "up" last month but now it's "down". Then count the number of "1" bits of the resulting bit array.

### How Many Hosts Were "Down" Last Month But Now It's "Up"

Modern App Developer:

> I can retrieve the "Down" hosts from last month from ES, then for each "Down" host, search for it with the state equals to "Up" this month, and accumulate the results.

Old-Timer System Developer:

> I can perform this opeartion: `(this_month XOR last_month) XOR this_month`. This will return a bit array that has the bit set if the host was "down" last month but now it's "up". Then count the number of "1" bits of the resulting bit array.

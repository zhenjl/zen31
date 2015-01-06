+++
Categories = [ "message queue", "golang", "code", "surgemq" ]
date = "2014-12-25T00:00:33-08:00"
title = "PingMQ: A SurgeMQ-based ICMP Monitoring Tool"
+++

[pingmq](https://github.com/surge/surgemq/tree/master/cmd/pingmq) is developed to demonstrate the different use cases one can use [SurgeMQ](//surgemq.com), a high performance MQTT server and client library. In this simplified use case, a network administrator can setup server uptime monitoring system by periodically sending ICMP ECHO_REQUEST to all the IPs in their network, and send the results to SurgeMQ.

Then multiple clients can subscribe to results based on their different needs. For example, a client maybe only interested in any failed ping attempts, as that would indicate a host might be down. After a certain number of failures the client may then raise some type of flag to indicate host down.

There are three benefits of using SurgeMQ for this use case. 

* First, with all the different monitoring tools out there that wants to know if hosts are up or down, they can all now subscribe to a single source of information. They no longer need to write their own uptime tools. 
* Second, assuming there are 5 monitoring tools on the network that wants to ping each and every host, the small packets are going to congest the network. The company can save 80% on their uptime monitoring bandwidth by having a single tool that pings the hosts, and have the rest subscribe to the results. 
* Third/last, the company can enhance their security posture by placing tighter restrictions on their firewalls if there's only a single host that can send ICMP ECHO_REQUESTS to all other hosts.

The following commands will run pingmq as a server, pinging the 8.8.8.0/28 CIDR block, and publishing the results to /ping/success/{ip} and /ping/failure/{ip} topics every 30 seconds. `sudo` is needed because we are using RAW sockets and that requires root privilege.

```
$ go build
$ sudo ./pingmq server -p 8.8.8.0/28 -i 30
```

The following command will run pingmq as a client, subscribing to /ping/failure/+ topic and receiving any failed ping attempts.

```
$ ./pingmq client -t /ping/failure/+
8.8.8.6: Request timed out for seq 1
```

The following command will run pingmq as a client, subscribing to /ping/failure/+ topic and receiving any failed ping attempts.

```
$ ./pingmq client -t /ping/success/+
8 bytes from 8.8.8.8: seq=1 ttl=56 tos=32 time=21.753711ms
```

One can also subscribe to a specific IP by using the following command.

```
$ ./pingmq client -t /ping/+/8.8.8.8
8 bytes from 8.8.8.8: seq=1 ttl=56 tos=32 time=21.753711ms
```
### Commands

There are two builtin commands for `pingmq`.

**`pingmq server`**

```
Usage:
  pingmq server [flags]

 Available Flags:
  -h, --help=false: help for server
  -i, --interval=60: ping interval in seconds
  -p, --ping=[]: Comma separated list of IPv4 addresses to ping
  -q, --quiet=false: print out ping results
  -u, --uri="tcp://:5836": URI to run the server on
```

**`pingmq client`**

```
Usage:
  pingmq client [flags]

 Available Flags:
  -h, --help=false: help for client
  -s, --server="tcp://127.0.0.1:5836": PingMQ server to connect to
  -t, --topic=[]: Comma separated list of topics to subscribe to
```


### IP Addresses

To list IPs you like to use with `pingmq`, you can use the following formats:

```
10.1.1.1      -> 10.1.1.1
10.1.1.1,2    -> 10.1.1.1, 10.1.1.2
10.1.1,2.1    -> 10.1.1.1, 10.1.2.1
10.1.1,2.1,2  -> 10.1.1.1, 10.1.1.2 10.1.2.1, 10.1.2.2
10.1.1.1-2    -> 10.1.1.1, 10.1.1.2
10.1.1.-2     -> 10.1.1.0, 10.1.1.1, 10.1.1.2
10.1.1.1-10   -> 10.1.1.1, 10.1.1.2 ... 10.1.1.10
10.1.1.1-     -> 10.1.1.1 ... 10.1.1.254, 10.1.1.255
10.1.1-3.1    -> 10.1.1.1, 10.1.2.1, 10.1.3.1
10.1-3.1-3.1  -> 10.1.1.1, 10.1.2.1, 10.1.3.1, 10.2.1.1, 10.2.2.1, 10.2.3.1, 10.3.1.1, 10.3.2.1, 10.3.3.1
10.1.1        -> 10.1.1.0, 10.1.1.1 ... 10.1.1.254, 10.1.1.255
10.1.1-2      -> 10.1.1.0, 10.1.1.1 ... 10.1.1.255, 10.1.2.0, 10.1.2.1 ... 10.1.2.255
10.1-2        -> 10.1.0.0, 10.1.0,1 ... 10.2.255.254, 10..2.255.255
10            -> 10.0.0.0 ... 10.255.255.255
10.1.1.2,3,4  -> 10.1.1.1, 10.1.1.2, 10.1.1.3, 10.1.1.4
10.1.1,2      -> 10.1.1.0, 10.1.1.1 ... 10.1.1.255, 10.1.2.0, 10.1.2.1 ... 10.1.2.255
10.1.1/28     -> 10.1.1.0 ... 10.1.1.255
10.1.1.0/28   -> 10.1.1.0 ... 10.1.1.15
10.1.1.0/30   -> 10.1.1.0, 10.1.1.1, 10.1.1.2, 10.1.1.3
10.1.1.128/25 -> 10.1.1.128 ... 10.1.1.255
```

### Topic Format

TO subscribe to the `pingmq` results, you can use the following formats:

* `/ping/#` will subscribe to both success and failed pings for all IP addresses
* `ping/success/+` will subscribe to success pings for all IP addresses
* `ping/failure/+` will subscribe to failed pings for all IP addresses
* `ping/+/8.8.8.8` will subscribe to both success and failed pings for all IP 8.8.8.8

### Building

To build `pingmq`, you need to have installed [Go 1.3.3 or 1.4](http://golang.org). Then run the following:

```
# go get github.com/surge/surgemq
# cd surgemq/examples/pingmq
# go build
```

After that, you should see the `pingmq` command in the pingmq directory.
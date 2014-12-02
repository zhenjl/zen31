+++
date = "2013-08-28T14:20:22-08:00"
title = "Testing MsgPack and BSON"
categories = [ "golang", "code", "json" ]

+++

In one of the projects I am working on we are trying to select a message encoding scheme. The use case is pretty simple. We have a server that accepts data records from different clients, and our goal is support 100K messages per second per node. Our selection criteria are pretty simple as well:

* Compactness: how compact is the post-encoding byte array
* Performance: how fast is marshalling and unmarshalling of data

Out of the various encoding schemes out there, including [BSON](http://bsonspec.org), [MessagePack](http://msgpack.org), ProtoBuf, Thrift, etc etc, we decided to test BSON and MessagePack due to their closeness to JSON (we use JSON format quite a bit internally). 

Here's a very short and simple [Go](http://golang.org) program we wrote to test the performance. The libraries I am using are [Go codec](http://github.com/ugorji/go/codec) and [Go BSON library](http://labix.org/gobson). (I am sure one can argue that the library used affects the result, which I would agree. However, these are the best libraries for Go AFAICT.)

The results are as follows:

* For marshalling, BSON is about 15-20% slower than MsgPack. 
* For Unmarshalling, BSON is 300% slower than MsgPack. 
* Size-wise, BSON is about 20% more than MsgPack.

So looks like msgpack is the way to go!

Special thanks(!) to realrocker in #go-nuts and [Ugorji](https://github.com/ugorji) for their help in cleaning up my code and helping me figure out my problems.

Some notes about the codec library:

* According to Ugorji, decoding without schema in the codec library uses largest type for decoding, i.e. int64, uint64, float64. So if you don't have a schema, the result will not pass reflect.DeepEqual test unless you initially type convert to those types. This is documented [here](https://github.com/ugorji/go/commit/7d844bb938783105c48aa9f4a34663f7d4190c32)
* Ugorji also quickly fixed a bug where "codec should be able to decode into a byte slice from both msgpack str/raw format or msgpack bin format (new in finalized spec)." AWESOME response time!
* To get string support (encode/decode strings), make sure RawToString is set to true (see below)

[discussion](https://news.ycombinator.com/item?id=6293642)

{% gist 6371433 %}


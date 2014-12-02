+++
date = "2013-11-30T23:20:22-08:00"
title = "Ring Buffer - Variable-Length, Low-Latency, Lock-Free, Disruptor-Style"
categories = [ "golang", "code", "buffer" ]

+++

Comments/feedbacks on [Hacker News](https://news.ycombinator.com/item?id=6831293), [Reddit](http://www.reddit.com/r/golang/comments/1rvvb6/ring_buffer_variablelength_lowlatency_lockfree/)

> 2013-12-04 Update #1: Read a [very interesting thread on golang-nuts list](https://groups.google.com/forum/#!topic/golang-nuts/7tUShPuPfNM) on the performance of interface. Seems like using interfaces really affects performance. In Joshua's test he saw a 3-4x performance difference. I decided to try this on the ring buffer implementation since I am currently using interface. A quick test laster, looks like NOT using interface increased performance 2.4x. For now the code is in the "[nointerface](https://github.com/reducedb/ringbuffer/tree/nointerface)" branch.

```
Benchmark1ProducerAnd1Consumer-3         5000000               353 ns/op
Benchmark1ProducerAnd1ConsumerInBytes-3 10000000               147 ns/op
```

### tl;dr

* [This project](https://github.com/reducedb/ringbuffer) implements a low-latency lock-free ring buffer for variable length byte slices. It is modeled after the [LMAX Disruptor](https://github.com/LMAX-Exchange/disruptor/), but not a direct port.
* If you have only a single core, don't use this. Use Go channels instead! In fact, unless you can spare as many cores as the number of producers and consumers, don't use this ring buffer. 
* In fact, for MOST use cases, Go channel is a better approach. This ring buffer is really a specialized solution for very specific use cases.
* Primary pattern of this ring buffer is single producer and multiple consumer, where the single producer put bytes into the buffer, and each consumer will process ALL of the items in the buffer. (Other patterns can be implemented later but this is what's here now.)
* This ring buffer is designed to deal with situations where we don't know the length of the byte slice before hand. It will write the byte slice to the buffer across multiple slots in the ring if necessary.
* The ring buffer currently employs a lock-free busy-wait strategy, where the producer and consumers will continue to loop until data is available. As such, it performs very well in a multi-core environment (almost twice as fast as Go channels) if you can spare 1 core per produer/consumer, but extremely poorly in a single-core environment (600 times worse compare to Go channels).
* You can find a lot of information on the LMAX Disruptor. The resources I used include [Trisha's Disruptor blog series](http://mechanitis.blogspot.com/search/label/disruptor), [LMAX Disruptor main page](http://lmax-exchange.github.io/disruptor/), [Disruptor technical whitepaper](http://lmax-exchange.github.com/disruptor/files/Disruptor-1.0.pdf), and Martin Fowler's [LMAX Architecture article](http://martinfowler.com/articles/lmax.html).
* You can also read more about [circular buffer](http://en.wikipedia.org/wiki/Circular_buffer), [producer–consumer problem](http://en.wikipedia.org/wiki/Producer-consumer_problem).

### Go Learn Project #7 - Ring Buffer

For the past several projects ([#6](http://zhen.org/blog/benchmarking-integer-compression-in-go/), [#5](http://zhen.org/blog/bitmap-compression-using-ewah-in-go/), [#4](http://zhen.org/blog/benchmarking-bloom-filters-and-hash-functions-in-go/)), I've mostly been hacking bits, and optimizing them as much as possible for a single core.

For project #7, I decided to do something slightly different. This time we will create a ring buffer that can support variable length byte slices, and leverage multi-cores using multiple goroutines.

Primary target use case is for a producer to read bytes from sockets, ZMQ, files, etc that require process, like JSON, csv, and tsv strings, at a very high speed, such as millions of lines per second, and put these lines into a buffer so other consumers can process these. 

A good example is when we import files with millions of lines of JSON object. These JSON objects are read from files, inserted into the buffer, and then they are unmarshalled into other structures. 

The goal is to process millions of data items per second. 

#### Ring Buffer

There are several ways to tackle this. A queue or ring buffer is usually a good data structure for this. You can think of a ring buffer is just a special type of queue that's just contiguous by wrapping itself. As Wikipedia said,

> A circular buffer, cyclic buffer or ring buffer is a data structure that uses a single, fixed-size buffer as if it were connected end-to-end. This structure lends itself easily to buffering data streams.

So, implementation-wise, we can tackle this problem using a standard ring buffer. The most common way of implementing a standard ring buffer is to keep track of a head and a tail pointer, and keep putting items into the buffer but ensuring that head and tail don't cross each other. 

In most implementations, the pointers are mod'ed with the ring size to determine the next slot size. Also, mutex is used to ensure only one thread is modifying these pointers at the same time.

#### Go Channels

In Go, an idiomatic and fairly common way is to use [buffered channels](http://golang.org/doc/effective_go.html#channels) to solve this problem. It is effectively a queue where a producer puts data items into one end of the channel, and the consumer reads the data items on the other end of the channel. There are certainly pros and cons to to this approach.

First, it is Go idiomatic! Need I say more... :)

This is probably the easiest approach since Go Channel is already a battle-tested data structure and it's readily available. An example is provided below in the examples section. Performance-wise it is actually not too bad. In a multi-core environment, it's about 60% of the performance compare to the ring buffer. However, in a single-core environment, it is MUCH faster. In fact, 1300 times faster than my ring buffer!

There is one major difference between using channels vs this ring buffer. When the channel has multiple consumers, the data is multiplexed to the consumers. So each consumer will get only part of the data rather than going through all the data. This is illustrated by [this play](http://play.golang.org/p/ACC5LIohIe). The current design of the ring buffer allows multiple consumers to go through every item in the queue. A obvious workaround is to send the data items to multiple channels. 

One down side with my channel approach is that I end up creating a lot of garbage over time and will need to be GC'ed. Specifically, I am creating a new byte slice for each new data item. Again, there is workaround for this. One can implement a [leaky buffer](http://golang.org/doc/effective_go.html#leaky_buffer). However, because we don't know how big the data items are before hand, it's more difficult to preallocate the buffers up front.

There might actually be a way to implement the leaky buffer with a big preallocated slice. I may just do that as the next project. The goal is to see if we can avoid having to allocate individual byte slices and leverage CPU caching for the big buffer.

#### Lock-Free Ring Buffer

The way that I've decided to tackle this problem is to model the ring buffer after the LMAX Disruptor. If you haven't read Martin Fowler's [article on LMAX Architecture](http://martinfowler.com/articles/lmax.html), at this time I would recommend that you stop and go read it first. After that, you should go read [Trisha's Disruptor blog series](http://mechanitis.blogspot.com/search/label/disruptor) that explains in even more details how the Disruptor works. 

One thing to keep in mind is that the Disruptor-style ring buffer has significant resource requirement, i.e., it requires N cores, where N is the number of producers and consumers, to be performant. And it will keep cores busy by busy waiting (looping). So huge downside. If you don't need this type of low latency architecture, it's much better to stay with channels.

### Performance Comparison

These benchmarks are performed on a MacBook Pro with 2.8GHz Intel Core i7 procesor (Haswell), and 16 GB 1600MHz DDR3 memory. Go version 1.2rc5.

The 2 channel consumers benchmark is a single producer sending to 2 channels, each channel consumed by a separate goroutine. So it is apples-to-apples compare to the ring buffer 2 consumers benchmark.

You can see clearly the requirement of 1 core per consumer/producer in the ring buffer implementation (first 6 lines). Without that, performance suffer greately!

Also notice that the channel benchmark (last 6 lines) is faster for a single core than multi-cores. This is probably due to your friendly cache at play.

```
$ go test -bench=. -run=xxx -cpu=1,2,3
PASS
Benchmark1ProducerAnd1Consumer     10000            339807 ns/op
Benchmark1ProducerAnd1Consumer-2        10000000               258 ns/op
Benchmark1ProducerAnd1Consumer-3        10000000               260 ns/op
Benchmark1ProducerAnd2Consumers    10000            341859 ns/op
Benchmark1ProducerAnd2Consumers-2         200000             14967 ns/op
Benchmark1ProducerAnd2Consumers-3        5000000               340 ns/op
BenchmarkChannels1Consumer      10000000               241 ns/op
BenchmarkChannels1Consumer-2     5000000               436 ns/op
BenchmarkChannels1Consumer-3     5000000               446 ns/op
BenchmarkChannels2Consumers      5000000               319 ns/op
BenchmarkChannels2Consumers-2    5000000               647 ns/op
BenchmarkChannels2Consumers-3    5000000               570 ns/op
```

### Examples

#### Go Channel: 1 Producer and 1 Consumer

```
func BenchmarkChannels(b *testing.B) {
	dataSize := 256
	data := make([]byte, dataSize)
	for i := 0; i < dataSize; i++ {
		data[i] = byte(i % 256)
	}

	ch := make(chan []byte, 128)
	go func() {
		for i := 0; i < b.N; i++ {
			// To be fair, we want to make a copy of the data, otherwise we are just
			// sending the same slice header over and over. In the real-world, the
			// original data slice may get over-written by the next set of bytes.
			tmp := make([]byte, dataSize)
			copy(tmp, data)
			ch <- tmp
		}
	}()

	for i := 0; i < b.N; i++ {
		out := <-ch
		if !bytes.Equal(out, data) {
			b.Fatalf("bytes not the same")
		}
	}
}
```

#### Ring Buffer: 1 Producer and 1 Consumer

This test function creates a 256-slot ring buffer, with each slot being 128 bytes long. It also creates 1 producer and 1 consumer, where the producer will put the same byte slice into the buffer 10,000 times, and the consumer will read from the buffer and then make sure we read the correct byte slice.

```
func Test1ProducerAnd1ConsumerAgain(t *testing.T) {
	// Creates a new ring buffer that's 256 slots and each slot 128 bytes long.
	r, err := New(128, 256)
	if err != nil {
		t.Fatal(err)
	}

	// Gets a single producer from the the ring buffer. If NewProducer() is called
	// the second time, an error will be returned.
	p, err := r.NewProducer()
	if err != nil {
		t.Fatal(err)
	}

	// Gets a singel consumer from the ring buffer. You can call NewConsumer() multiple
	// times and get back a new consumer each time. The consumers are independent and will
	// go through the ring buffers separately. In other words, each consumer will have 
	// their own independent sequence tracker.
	c, err := r.NewConsumer()
	if err != nil {
		t.Fatal(err)
	}

	// We are going to write 10,000 items into the buffer.
	var count int64 = 10000

	// Let's prepare the data to write. It's just a basic byte slice that's 256 bytes long.
	dataSize := 256
	data := make([]byte, dataSize)
	for i := 0; i < dataSize; i++ {
		data[i] = byte(i % 256)
	}

	// Producer goroutine
	go func() {
		// Producer will put the same data slice into the buffer _count_ times
		for i := int64(0); i < count; i++ {
			if _, err := p.Put(data); err != nil {
				// Unfortuantely we have an issue here. If the producer gets an error 
				// and exits, the consumer will continue to wait and not exit. In the
				// real-world, we need to notify all the consumers that there's been
				// an error and ensure they exit as well.
				t.Fatal(err)
			}
		}
	}()

	var total int64

	// Consumer goroutine
	
	// The consumer will also read from the buffer _count_ times
	for i := int64(0); i < count; i++ {
		if out, err := c.Get(); err != nil {
			t.Fatal(err)
		} else {
			// Check to see if the byte slice we got is the same as the original data
			if !bytes.Equal(out.([]byte), data) {
				t.Fatalf("bytes not the same")
			}

			total++
		}
	}

	// Check to make sure the count matches
	if total != count {
		t.Fatalf("Expected to have read %d items, got %d\n", count, total)
	}
}

```

#### Ring Buffer: 1 Producer and 2 Consumers

As mentioned before, the ring buffer supports multiple consumers. [This example](https://github.com/reducedb/ringbuffer/blob/master/bytebuffer/ringbuffer_test.go#L304) shows how you would create two consumers.

### Conclusion

See tl;dr on top.

Comments/feedbacks on [Hacker News](https://news.ycombinator.com/item?id=6831293), [Reddit](http://www.reddit.com/r/golang/comments/1rvvb6/ring_buffer_variablelength_lowlatency_lockfree/)

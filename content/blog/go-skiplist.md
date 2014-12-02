+++
date = "2013-09-02T13:09:22-08:00"
title = "Go Skiplist"
categories = [ "code", "golang", "skiplist" ]

+++

Most of my nights and weekends in the past week have been immersed in my [new skiplist library](https://github.com/reducedb/skiplist), even sacrificing some family time (yikes, not good!). It's one of those projects I picked up in order to learn [Go](http://golang.org). 

Wikipedia defines a skip list as

> A skip list is a data structure for storing a sorted list of items using a hierarchy of linked lists that connect increasingly sparse subsequences of the items. These auxiliary lists allow item lookup with efficiency comparable to balanced binary search trees (that is, with number of probes proportional to log n instead of n).

You can imagine using a skiplist data structure whenver you want to use a binary search tree.

This skiplist implementation also uses search fingers, based on William Pugh's work, [A Skiplist Cookbook](http://drum.lib.umd.edu/bitstream/1903/544/2/CS-TR-2286.1.pdf). So the efficiency is O(log k) where k is the distance between the last searched/updated item and the current one.

### Performance

{% gist e8779545c102c69aae10 %}

These numbers are from my Macbook Air 10.8.4 1.8GHz Intel Core i5 4GB 1600MHz DDR3.

Notice the fastest time is BenchmarkInsertTimeDescending. This is because the keys for that test is generated using time.Now().UnixNano(), which is always ascending. And because the sort order of the skiplist is descending, so the new item is ALWAYS inserted at the front of the list. This happens to have the best case of O(1).

The next best time is BenchmarkInsertTimeAscending. This is still pretty good, but because the sort order is ascending, so the new items are ALWAYS inserted at the end. This required the skiplist to walk all the levels so it took a bit longer.

The other benchmarks should have the average O(log k) efficiency.

### Example (Int)

You can see additional examples in the [test file](https://github.com/reducedb/skiplist/blob/master/skiplist_test.go).

```
// Creating a new skiplist, using the built-in Less Than function as the comparator.
// There are also two other built in comparators: BuiltinGreaterThan, BuiltinEqual
list := New(skiplist.BuiltinLessThan)

// Inserting key, value pairs into the skiplist. The skiplist is sorted by key,
// using the comparator function to determine order
list.Insert(1,1)
list.Insert(1,2)
list.Insert(2,1)
list.Insert(2,2)
list.Insert(2,3)
list.Insert(2,4)
list.Insert(2,5)
list.Insert(1,3)
list.Insert(1,4)
list.Insert(1,5)

// Selecting items that have the key == 1. Select returns a Skiplist.Iterator
rIter, err := list.Select(1)

// Iterate through the list of items. Keys and Values are turned as interface{}, so you
// need to type assert them to your type
for rIter.Next() {
	fmt.Println(rIter.Key().(int), rIter.Value().(int))
}

// Delete the items that match key. An iterator is returned with the list of deleted items.
rIter, err = list.Delete(1)

// You can also SelectRange or DeleteRange
rIter, err = list.SelectRange(1, 2)

rIter, err = list.DeleteRange(1, 2)
```

### Bultin Comparators

There are three built-in comparator functions:

* BuiltinLessThan: if you want to sort the skiplist in ascending order
* BuiltinGreaterThan: if you want to sort the skiplist in descending order
* BuiltinEqual: just to compare

Currently these built-in comparator functions work for all built-in Go types, including:

* string
* uint64, uint32, uint16, uint8, uint
* int64, int32, int16, int8, int
* float32, float64
* unitptr

[discussion/comments](https://news.ycombinator.com/item?id=6317109)

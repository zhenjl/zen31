+++
categories = [ "code", "golang", "stemming" ]
date = "2015-01-21T20:48:44-08:00"
title = "Generating Porter2 FSM For Fun and Performance in Go"
+++

[![GoDoc](http://godoc.org/github.com/surgebase/porter2?status.svg)](http://godoc.org/github.com/surgebase/porter2)

## tl;dr

* This post describes the [Porter2](https://github.com/surgebase/porter2) package I implemented. It is written in Go (#golang).
* By using a [finite-state-machine](http://en.wikipedia.org/wiki/Finite-state_machine) approach to [Porter2](http://snowball.tartarus.org/algorithms/english/stemmer.html) [stemming](http://en.wikipedia.org/wiki/Stemming), I was able to achieve 660% better performance compare to other Go implementations.
* FSM-based approach is great for known/fixed data set, but obviously not workable if the data set changes at runtime.
* Hand-coding FSM is a PITA!!! [Automate](https://github.com/surgebase/porter2/tree/master/cmd/suffixfsm) if possible.

## Introduction

In a personal project I am working on, I had the need to perform word stemming in two scenarios. First, I need to perform stemming for all the string literals in a LARGE corpus and then determine if the words are in a fixed set of literals. Second, I need to perform stemming for a subset of words in real-time, as messages stream in.

In the first case, performance is important but not critical; in the second case, performance is a huge factor.

### Stemming 

To start, according to [wikipedia](http://en.wikipedia.org/wiki/Stemming):

> Stemming is the term used in linguistic morphology and information retrieval to describe the process for reducing inflected (or sometimes derived) words to their word stem, base or root form—generally a written word form.

As a quick example, the words _fail_, _failed_, and _failing_ all mean something has _failed_. By stemming these three words, I will get a single form which is _fail_. I can then just use _fail_ going forward instead of having to compare all three forms all the time.

The [Porter](http://tartarus.org/martin/PorterStemmer/def.txt) stemming algorithm is by far the most commonly used stemmer and also considered to be one of the most gentle stemmers. The Porter stemming algorithm (or ‘Porter stemmer’) works by removing the commoner morphological and inflexional endings from words in English. Its main use is as part of a term normalisation process that is usually done when setting up Information Retrieval systems. ([ref](http://tartarus.org/martin/PorterStemmer/))

[Porter2](http://snowball.tartarus.org/algorithms/english/stemmer.html) is universally considered to be an enhancement over the original Porter algorithm. Porter2 has an improved set of rules and it's widely used as well.

## Implementation 

This package, [Porter2](https://github.com/surgebase/porter2), implements the Porter2 stemmer. It is written completely using finite state machines to perform suffix comparison, rather than the usual string-based or tree-based approaches. As a result, it is 660% faster compare to string comparison-based approach written in the same (Go) language.

This implementation has been successfully validated with the dataset from http://snowball.tartarus.org/algorithms/english/, so it should be in a usable state. If you encounter any issues, please feel free to [open an issue](https://github.com/surgebase/porter2/issues).

Usage is fairly simple:

```
import "github.com/surgebase/porter2"

fmt.Println(porter2.Stem("seaweed")) // should get seawe
```

### Performance

This implementation by far has the highest performance of the various Go-based implementations, AFAICT. I tested a few of the implementations and the results are below. 

| Implementation | Time | Algorithm |
|----------------|------|-----------|
| [surgebase](https://github.com/surgebase/porter2) | 319.009358ms | Porter2 |
| [dchest](https://github.com/dchest/stemmer) | 2.106912401s | Porter2 |
| [kljensen](https://github.com/kljensen/snowball) | 5.725917198s | Porter2 |

To run the test again, you can run [compare.go](https://github.com/surgebase/porter2/tree/master/cmd/compare) (`go run compare.go`).

### State Machines

Most of the implementations, like the ones in the table above, rely completely on suffix string comparison. Basically there's a list of suffixes, and the code will loop through the list to see if there's a match. Given most of the time you are looking for the longest match, so you order the list so the longest is the first one. So if you are luckly, the match will be early on the list. But regardless that's a huge performance hit.

This implementation is based completely on finite state machines to perform suffix comparison. You compare each chacter of the string starting at the last character going backwards. The state machines will determine what the longest suffix is. 

As an example, let's look at the 3 suffixes from step0 of the porte2 algorithm. The goal, and it's the same for all the other steps, it's to find the longest matching suffix.

```
'
's
's'
```

If you were to build a non-space-optimized [suffix tree](http://en.wikipedia.org/wiki/Suffix_tree), you would get this, where R is the root of the tree, and any node with * is designated as a final state:

```
        R
       / \
      '*  s
     /     \
    s       '*
   /
  '*
```

This is a fairly easy tree to build, and we actually did that in the FSM generator we will talk about later. However, to build a working suffix tree in Go, we would need to use a `map[rune]*node` structure at each of the nodes. And then search the map for each rune we encounter. 

To test the performance of using a switch statement vs using a map, I wrote a [quick test](https://github.com/surgebase/porter2/tree/master/cmd/switchvsmap):

```
switch: 4.956523ms
   map: 10.016601ms
```

The test basically runs a switch statement and a map each for 1,000,000 times. So it seems like using a switch statement is faster than a map. Though I think the compiler basically builds a map for all the switch case statements.  (Maybe we should call this post _Microbenchmarking for fun and performance_?)

In any case, let's go with the switch approach. We basically need to unroll the suffix tree into a finite state machine. 


```
        R0
       / \
      '1* s2
     /     \
    s3      '4*
   /
  '5*
```

To do that, we need to assign a state number to each of the nodes in the suffix tree, and output each of the states and the transitions based on the rune encountered. The tree above is the same as the one before, but now has a state number assigned to each node.

### Generator

I actually started building all the porter2 FSMs manually with a completely different approach than what I am describing here. I won't go into details here but needless to say, it was disastrous. Not only was hand coding state machines extremely error-prone, the approach I was taking also had a lot of potential for bugs. It took me MANY HOURS to hand build those FSMs but at the end, I was happy to abandon all of them for the approach I am taking now.

To reduce errors and make updating the FSM easier, I wrote a quick tool called [suffixfsm](https://github.com/surgebase/porter2/tree/master/cmd/suffixfsm) to generate the FSMs. The tool basically takes a list of suffixes, creates a suffix tree as described above, and unrolls the tree into a set of states using the `switch` statement. 

It took me just a couple hours to write and debug the tool, and I was well on my way to fixing other bugs! 

For example, running the command `go run suffixfsm.go step0.txt` generated the following code. This is a complete function for step0 of the porter2 algorithm. The only thing missing is what to do with each of the final states, which are in the last `switch` statement.

```
var (
		l int = len(rs) // string length
		m int			// suffix length
		s int			// state
		f int			// end state of longgest suffix
		r rune			// current rune
	)

loop:
	for i := 0; i < l; i++ {
		r = rs[l-i-1]

		switch s {
		case 0:
			switch r {
			case '\'':
				s = 1
				m = 1
				f = 1
				// ' - final
			case 's':
				s = 2
			default:
				break loop
			}
		case 1:
			switch r {
			case 's':
				s = 4
			default:
				break loop
			}
		case 2:
			switch r {
			case '\'':
				s = 3
				m = 2
				f = 3
				// 's - final
			default:
				break loop
			}
		case 4:
			switch r {
			case '\'':
				s = 5
				m = 3
				f = 5
				// 's' - final
			default:
				break loop
			}
		default:
			break loop
		}
	}

	switch f {
	case 1:
		// ' - final

	case 3:
		// 's - final

	case 5:
		// 's' - final

	}

	return rs
```

## Finally

This is a technique that can probably be applied to any fixed data set. The performance may vary based on the size of the state machine so test it with both maps and FSM to see what works best.

Happy Go'ing!
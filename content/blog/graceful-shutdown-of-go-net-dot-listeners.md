+++
date = "2013-12-12T23:33:22-08:00"
title = "Graceful Shutdown of Go net.Listeners"
categories = [ "code", "golang" ]

+++

Comments/Feedbacks at [Hacker News](https://news.ycombinator.com/item?id=6899568), [Reddit](http://www.reddit.com/r/golang/comments/1ss929/graceful_shutdown_of_go_netlisteners/)

The past few evenings I've been working on a Go program that listens on a TCP socket, accepts new connections, processes some data and then return some data to the client. This is actually fairly simple in Go. The [top](http://golang.org/pkg/net) of the _net_ package has some fairly simple examples of how to do that. Another example can be found about [mid-section](http://golang.org/pkg/net/#example_Listener) of the page. You can also find a TON of examples online that shows you how to build a simple TCP listener. 

However, one thing I noticed in all these examples is that none of them shows you how to gracefully shutdown the TCP listener. Most of the examples expect to program to exit so there's no need to clean up anything. However, if you have a program that's a long-running server, and need to, for whatever reason, need to shutdown the TCP listener, you will need to clean up after yourself. Otherwise you may leave a bunch of goroutines behind unintentionally.

Another reason I wanted a way to shutdown the TCP listener is I want to be able to start a listener in my tests, then start up a bunch of clients, test some stuff, then afterwards shutdown the server. Then I can start another listener in another test for some other tests.

After some help from jhoto and foobaz on the #go-nuts IRC channel, I wrote the following example to demonstrate the graceful shutdown approach.

The basic idea is to leverage a quit channel to tell the Accept() goroutine that it's time to quit. Using quit channel is a fairly common practice in Go. However, in this case, the Accept() call is blocking waiting for new connections, so closing the quit channel won't have any effect unless the goroutine actually checks it. So to force Accept() to return from blocking, we can close the net.Listener. 

The order of the operation matters somewhat. We will want to first close the quit channel, then close the net.Listener. If we reverse the order, you will likely see a few more errors from the Accept() call.

The netgrace_test.go file below shows an example of how to use the quit channel to help gracefully shutdown net.Listeners.

Hopefully you will find this tip useful. You can find it as a [gist](https://gist.github.com/zhenjl/7940977) as well.

<script src="https://gist.github.com/zhenjl/7940977.js"></script>

Comments/Feedbacks at [Hacker News](https://news.ycombinator.com/item?id=6899568), [Reddit](http://www.reddit.com/r/golang/comments/1ss929/graceful_shutdown_of_go_netlisteners/)

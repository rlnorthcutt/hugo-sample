---
title: "new httperf results : 572000 reqs/s"
date: 2010-10-23
---

This morning I came across [this interesting post](http://kristianlyng.wordpress.com/2010/10/23/275k-req/) from Kristian Lyngstol about the performance tests he ran on the [Varnish](http://www.varnish-cache.org/) cache. What struck me was the number of requests per second Kristian managed to reach : 275000, not less. I'm not surprized at all that Varnish can withstand such high rates, it's known for being very fast. My surprize came from the fact that Kristian managed to find fast enough tools to run this test. My old injector is limited to around 100k requests per second on my machines, as it does not support keep-alive, and Apache's ab to around 150k with keep-alive enabled. And when I managed to reach 2 millions requests per second, I was feeding a constant stream of pipelined requests with netcat, which is particularly inconvenient to use.

Kristian said he used [httperf](http://www.hpl.hp.com/research/linux/httperf/). I tried it in the past but did not manage to get good numbers out of it. He said he found some "httperf secrets", so that made me want to try again. First tests were limited to approximately 50000 requests per second with httperf at 100% CPU. Something close to my memories. But reading the man, I found that httperf can work in a session-based mode with the "--wsess" parameter, where it also support HTTP pipelining. Hmmm nice, we'll be less sensible to packet round-trips :-) So I tried again with haproxy simply doing redirects. Performance was still limited to 50000 requests per second.

In fact, there appears to be a default limit of 50000 requests per second when "--rate" is not specified. I set it to 1 million and ran the test again. Result: about 158000 requests per second at 100% CPU and with haproxy at 44%. Since my machine is a Core2 Quad at 3 GHz, I fired 3 httperf against one haproxy process. The load reached a max of 572000 requests/s with an average around 450000 requests per second. This time, haproxy and all 3 httperf were using 100% CPU. What an improvement!

[![](img/haproxy-572krps-sm.gif)](img/haproxy-572krps.gif)  

These tests mean nothing at all for real world uses of course, because when you have many clients, they won't send you massive amounts of pipelined requests. However it's very nice to be able to stress-test the HTTP engine for regression testing. And this will be an invaluable measurement tool to test the end-to-end keep-alive when it's finished. I still have to figure out the meaning of some options and how to make the process less verbose. Right now it fills a screen with many zeroes, making it hard to extract the useful numbers. I'm grateful to Kristian to have made me revisit httperf !

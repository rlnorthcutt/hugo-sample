---
title: "Several users reported on the mailing list that they were experiencing abnormal concurrent connection counts higher than the maxconn they configured."
date: 2008-09-14
---
Several users reported on [the mailing list](http://www.formilux.org/archives/haproxy/0809/date.html) that they were experiencing abnormal concurrent connection counts higher than the maxconn they configured.

They were very prompt to send me configurations and screenshots of the stats report [showing the problem](http://skitch.com/signalmark/i5j1/haproxy-maxconn-bug).

It was indeed a bug triggered every time a connection attempt to a server failed.

I've fixed it along with another minor one, and released **[1.3.15.4 and 1.3.14.8](download/1.3/src/)**.

Mongrel users are particularly exposed because they run with **maxconn=1** and the server cannot accept more connections, so users may experience occasional errors when a server starts to reject connections.

It would also be interesting to find why some connections fail to the servers.

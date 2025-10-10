---
title: "haproxy versions 1.3.15.2 and 1.3.14.6 have been released to fix a major bug in request queue handling."
date: 2008-06-21
---
**[haproxy versions 1.3.15.2 and 1.3.14.6](download/1.3/src/)** have been released to fix a major bug in request queue handling.

The problem was that due to a design problem, it was possible for new requests to be immediately served by a server before a request in queue would be served.

That caused some requests to remain in queue until they reached the queue timeout, after which either they would eventually be served, or return a 503 error code to the client.

Since it was a design problem, it took a lot of time analyzing the root cause and finding a solution.

However, as a positive side effect, the fix now makes the redispatch option work for requests which overflow a queue.

That way, clients do not get a 503 error anymore but can be served by another server (which was the purpose of the redispatch option.

Note that it is possible that 1.2 is also affected by the issue since some parts of the faulty code have not changed since.

But it is very hard to determine if it is faulty or not, and backporting the fix would take even more time.

Maybe I will eventually take a look at it if people complain about the issue.

Update (2008/06/28): Alexander Staubo, who first [noticed the problem](http://affectioncode.wordpress.com/2008/06/11/comparing-nginx-and-haproxy-for-web-applications/), has run [a new series of tests](http://affectioncode.wordpress.com/2008/06/28/another-comparison-of-haproxy-and-nginx/) showing that the problem is definitely fixed.

It also demonstrates the very nice positive effect of running with **maxconn 1** with Rails servers.

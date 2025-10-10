---
title: "HTTP/1.1 reloaded"
date: 2014-06-07
---
Six years ago, Daniel Stenberg [notified](http://curl.haxx.se/mail/lib-2008-07/0245.html) on the libcurl mailing list that [Mark Nottingham](https://www.mnot.net/blog/), chair of the [IETF HTTP Working Group](http://trac.tools.ietf.org/wg/httpbis/trac/wiki), initiated a review of existing HTTP implementations.

Since HAProxy was mentionned in this list, Aleks Lazic [relayed this mail](http://www.formilux.org/archives/haproxy/0808/1253.html) to the haproxy mailing list and I attempted to fill in the form with the information I could provide on HAProxy.

By then HAProxy 1.3.15 had just been released without keep-alive nor HTTP/1.1 support.

Being confronted to a lot of interoperability issues between clients and servers through HAProxy, I felt that it was a great opportunity to join the Working Group to try to improve the situation from my angle of view.

I was impressed to see that participants work professionally and calmly.

Noone really tries to defend his own implementation, what matters is interoperability, even if that sometimes needs changes in their code.

Of course, the concerns are different for various types of components (eg: security, performance, complexity, etc), often resulting in long debates.

And like many other products, HAProxy experienced quite a number of code changes consecutive to clarifications made to the spec.

The latest example of this [happened](http://lists.w3.org/Archives/Public/ietf-http-wg/2014AprJun/1050.html) after Google Chrome users were seeing HAProxy's 408 error page on a number of web sites.

And 7 years after this positive work started (OK, 6 years for me, I started late), the group's efforts have [finally resulted in 11 new RFCs](http://lists.w3.org/Archives/Public/ietf-http-wg/2014AprJun/1169.html)!

The 6 first (RFC 7230 to 7235) replace the aging RFC2616 :

1.  [RFC7230](http://tools.ietf.org/html/rfc7230) : Message Syntax and Routing
2.  [RFC7231](http://tools.ietf.org/html/rfc7231) : Semantics and Content
3.  [RFC7232](http://tools.ietf.org/html/rfc7232) : Conditional Requests
4.  [RFC7233](http://tools.ietf.org/html/rfc7233) : Range Requests
5.  [RFC7234](http://tools.ietf.org/html/rfc7234) : Caching
6.  [RFC7235](http://tools.ietf.org/html/rfc7235) : Authentication

The next ones are about authentication scheme and method registrations (7236 and 7237), and extensions whose discussion was initiated in the working group but which were not carried by the working group (status code 308, "Forwarded" and "Prefer" header).

If you're implementing an HTTP agent (client, server, proxy, gateway, or whatever), please read them.

They cover a lot of corner cases that are encountered in field and which are the result of the fact that the protocol evolved faster in field than in the docs.

The first two ones are already a very good start to demystify the protocol and get rid of your wrong beliefs.

What next ?

HTTP/2.0 is on the rails and has been for about 2 years now.

It's time to focus on it!

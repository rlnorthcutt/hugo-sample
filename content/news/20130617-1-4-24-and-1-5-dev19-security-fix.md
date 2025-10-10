---
title: "1.4.24 and 1.5-dev19 : security fix"
date: 2013-06-17
---
A new vulnerability was discovered in all versions from 1.4.4 and above.

It was fixed today with 1.4.24 and 1.5-dev19 ([CVE-2013-2175](http://seclists.org/oss-sec/2013/q2/581)).

This vulnerability can induce a crash when configs involving tail-relative header offset such as hdr\_ip(xff,-1) are used.

Please see the advisory for more details.

All 1.4 and 1.5 users must upgrade.

Additionally, a few other important bugs were fixed.

One of them was a regression introduced in 1.5-dev12, which could randomly crash haproxy on rare circumstances when using pipelined requests with a slow client.

Last, some endless loops were possible since 1.4 when using consistent hashing algorithms with flapping servers.

On the positive side, many small new features were finally merged, such as http-response rule sets, ability to change task priority, DSCP field, Netfilter mark and log-level based on L7 ACLs, ability to selectively accept the PROXY protocol header using ACLs, support for environment variables in ACLs and fetches, addition of a 3rd stick-counter, filtering on the stats page, transparent proxy for FreeBSD/OpenBSD, and a few other things.

Last but not least, the doc on ACLs/fetches got a major lift-up to deduplicate keywords.

A few important issues still need to be addressed, and server-side keep-alive is expected as well before final 1.5 can be released, hopefull by the end of this summer.

Please refer to the [1.4 changelog](/download/1.4/src/CHANGELOG) and [1.5 changelog](/download/1.5/src/CHANGELOG) for more information.

Source code is available [here for 1.4](/download/1.4/src/) and [here for 1.5](/download/1.5/src/).

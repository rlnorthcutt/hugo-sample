---
title: "HAProxy participates to IPv6 day"
date: 2011-05-31
---

About two weeks ago I registered to participate to the [World IPv6 day](http://worldipv6day.org/). The concept is very simple : on June 8th, many web sites will be available both in IPv4 and IPv6. Why only that day ? Because there exists some places where IPv6 can be resolved but not reached, causing the dual-stack sites to be unreachable from these places. By having many sites running IPv6 on the same day, network admins will notice the problem comes from their site and not from the outside since many sites will be unreachable at the same time.

HAProxy was running dual-stack a few years ago but I had to revert this due to many problem reports. Still some visitors might have noticed the little green image indicating to them if their browser can connect to IPv6. Since I noticed on the [participants list](http://www.worldipv6day.org/participant-websites/index.html) that some sites were already running with dual-stack enabled, I decided to enable it here again in advance, so that I'll be able to revert it in case some visitors report any issue. If no issue is reported until June 8th, I'll probably leave that enabled.

Unfortunately, the [Dedibox](http://www.dedibox.fr/) serving as a cache for the web site is in a network that is not yet IPv6-enabled. That's really a shame, considering that we upgraded it from an old box that was on an IPv6-capable network. I really don't understand what's happening at Free for taking that long a time to enable IPv6 on all their network segments, it does not seem to be on their top priority list. But since the site is running at home behind my [Nerim](http://www.nerim.net) internet access which has been IPv6-enabled for something like 10 years now, I could announce the ADSL endpoint address in the DNS.

Enabling IPv6 on your web site really is trivial with HAProxy. You just have to add "bind :::80" to your frontend and announce the IPv6 address as an AAAA record in your DNS zone, and that's all. No readdressing, no routing changes, nothing fancy. And you can even get IPv4/IPv6 statistics like [here](http://demo.haproxy.org/). BTW, I know for sure that some of the World IPv6 Day participants have done exactly that with their HAProxy config too :-)

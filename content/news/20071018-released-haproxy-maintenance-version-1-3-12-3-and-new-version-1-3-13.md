---
title: "Released haproxy maintenance version 1.3.12.3 and new version 1.3.13."
date: 2007-10-18
---
Released **[haproxy maintenance version 1.3.12.3](download/1.3/src/)** and **[new version 1.3.13](download/1.3/src/)**.

Thanks to quite a bunch of subscribers of the new [mailing list](https://www.mail-archive.com/haproxy@formilux.org/), several nasty bugs have been ironed out and a handful of smart features have been added.

The most visible add-ons are the UNIX socket to access the statistics page, and the support for [Doug Lea's dlmalloc](http://gee.cs.oswego.edu/pub/misc/malloc.c) which dramatically reduces memory usage during soft-reconfigurations.

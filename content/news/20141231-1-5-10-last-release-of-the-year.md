---
title: "1.5.10 : Last release of the year!"
date: 2014-12-31
---
Most of the fixes in this version are related to how we deal with out-of-memory situations.

This normally interests nobody except those who run many instances on memory-bound servers.

There was a very unlikely but possible case of crash when it was not possible to allocate a small chunk of memory (I managed to reproduce it after a long time during extremely aggressive tests).

There are a few fixes on tcp-checks, one for a bug causing some random contents to be analysed, another one where quick acks were disabled when there was no data to send, causing 200ms delays when "option tcp-check" was specified alone.

Another bug concerned proxies disabled in the configuration which could under some circumstances cause a segfault upon startup during the process mask propagation between frontends and backends.

The rest is mostly harmless, so keep cool, no rush if you're already running 1.5.9.

Code and changelog are available [here](/download/1.5/src/) as usual.

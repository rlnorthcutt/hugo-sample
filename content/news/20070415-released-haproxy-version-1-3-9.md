---
title: "Released haproxy version 1.3.9."
date: 2007-04-15
---

Released **[haproxy version 1.3.9](download/1.3/src/)**. This one adds modularization to the pollers, which made it possible for me to finally implement **support for FreeBSD kqueue()**. I'd like to thank Olivier Warin for providing me a FreeBSD account during this development.

A new concept was introduced too : **speculative I/O**. It is a new method consisting in reducing the number of calls to the expensive epoll\_ctl() and epoll\_wait() by attempting to access the file descriptors before being notified about their readiness. This provides an **overall speed boost of 10%**, which is quite much for just a poller.

---
title: "Released haproxy version 1.3.11.4."
date: 2007-06-03
---

Released **[haproxy version 1.3.11.4](download/1.3/src/)**. It fixes 2 long-standing bugs in timeout handling, which could sometimes cause 100% CPU usage during several seconds when a client had closed its write channel. Some small improvements to the I/O subsystem should save some CPU cycles on high bandwidth sites. It is now possible to finely tune the pollers for reduced latency.

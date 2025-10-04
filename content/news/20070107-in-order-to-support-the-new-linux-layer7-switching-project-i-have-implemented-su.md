---
title: "In order to support the new Linux Layer7 Switching project, I have implemented support for kernel TCP splicing using Alexandre Cassen's library."
date: 2007-01-07
---

In order to support the new **[Linux Layer7 Switching project](http://linux-l7sw.sf.net/)**, I have implemented support for **kernel TCP splicing** using Alexandre Cassen's library. This is still experimental but already works remarkably well. On my notebook at 400 Mbps, haproxy's usage goes down from 65% to 5-10%. I have written [some doc](/download/1.3/doc/tcp-splicing.txt) explaining how to setup up TCP splicing, with [an example](/download/1.3/test/tcp-splicing-sample.cfg). Since the original code was provided for Linux kernel 2.6.19 only, I have backported the patches to kernel [2.6.16](/download/patches/tcp_splice-0.1.1-linux-2.6.16.diff) and [2.4.33](/download/patches/tcp_splice-0.1.1-linux-2.4.33.diff).

The second great news is that Sin Yu has provided me with a useful patch for the second time : the **task scheduler** is now based on an **rbtree** and not on the dirty old dual-linked list anymore. It means that people who had performance problems and who had to set all their timeouts to the same value as a workaround will not have to do this anymore. I have tested, and the code works like a charm ! Thanks again Sin !

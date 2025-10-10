---
title: "Released haproxy version 1.3.10.1."
date: 2007-05-09
---
Released **[haproxy version 1.3.10.1](download/1.3/src/)**.

It fixes a serious bug affecting Linux users with speculative I/O processing, introduced in 1.3.9.

This bug was causing random timeouts on some traffic patterns, mostly noticeable in TCP mode but almost certainly in HTTP too.

All Linux users of 1.3.9 and 1.3.10 should either upgrade or disable speculative I/O as a workaround, by starting haproxy with the **\-ds** argument or by setting **nosepoll** in the **global** section.

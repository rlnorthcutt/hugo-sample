---
title: "Released haproxy version 1.3.11.3."
date: 2007-05-14
---
Released **[haproxy version 1.3.11.3](download/1.3/src/)**.

It fixes the (hopefully) last bug affecting Linux users with speculative I/O processing, introduced in 1.3.9.

This bug was also causing random timeouts.

Do not use versions 1.3.11 to 1.3.11.2 as they are all broken.

New in this release are a better timer management and a new memory manager which is able to self-manage its pools and free unused ones when memory is becoming scarce.

It is also easier to code with this new one since it's not necessary anymore to declare pool sizes.

Overall, yet another performance boost of 5% has been gained.

---
title: "Released haproxy version 1.2.17."
date: 2007-03-17
---
Released **[haproxy version 1.2.17](download/1.2/src/)**.

I have backported Sin Yu's **rbtree scheduler** from version 1.3 since it proved to be stable.

A few minor bugs were fixed, and two useful contributions were merged : support for user and group keywords as alternatives to numerical uid and gid from Marcus Rueckert, and the ability to prevent some source addresses from appearing in the X-Forwarded-For header, which is useful when combined with Stunnel for instance (patch from Bryan Germann).

Thanks to both of them, contribs are always welcome !

The [architecture manual](download/1.2/doc/) was updated to reflect new features in branch 1.2, with examples for stunnel and for load mitigation.

Users of 1.2.16 with high loads are encouraged to upgrade to 1.2.17 as it offers them the high performance of branch 1.3 with the reliability of the stable branch 1.2.

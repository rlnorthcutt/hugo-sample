---
title: "Released haproxy version 1.3.8.2 to fix a minor and a major bug."
date: 2007-04-03
---

Released **[haproxy version 1.3.8.2](download/1.3/src/)** to fix a minor and a major bug. The minor bug caused the response rewrite to fail on the status line. The major bug which was introduced in **1.3.6** could cause **the process to crash** in some circumstances when rewriting the request line (method and/or URI). **All users of 1.3.6 and later must upgrade**.

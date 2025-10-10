---
title: "Released haproxy version 1.3.7."
date: 2007-01-27
---
Released **[haproxy version 1.3.7](download/1.3/src/)**.

I found a **critical bug** in the new parser in development branch, causing crashes when an empty header is passed.

This was caused by a missing pointer assignment in the empty header processing path.

All 1.3.6 users MUST upgrade to 1.3.7.

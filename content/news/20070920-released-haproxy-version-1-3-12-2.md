---
title: "Released haproxy version 1.3.12.2."
date: 2007-09-20
---

Released **[haproxy version 1.3.12.2](download/1.3/src/)**. It fixes several bugs affecting timeouts and retry counts when configs are split between frontends and backends. Some sanity checks on the configuration file were never executed, causing some erroneous configurations to be accepted without being fixed. Last, the license has been clarified in a few files from O'Reilly. All in all, it seems like keeping a supported version is already starting to pay off, as people are looking for something **stable** and report bugs very quickly. **_All version 1.3 users are encouraged to upgrade to 1.3.12.2_**.

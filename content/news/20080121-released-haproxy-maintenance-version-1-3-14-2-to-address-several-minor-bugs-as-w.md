---
title: "Released haproxy maintenance version 1.3.14.2 to address several minor bugs as well as a major one affecting Linux 2.6 users with the sepoll poller, which can r"
date: 2008-01-21
---

Released **[haproxy maintenance version 1.3.14.2](download/1.3/src/)** to address several minor bugs as well as a major one affecting Linux 2.6 users with the sepoll poller, which can result in truncated responses if the client closes the connection before the server completes its response. Note that version 1.3.13.2 was released too with those bugs fixed. The GNU Makefile was crappy and caused trouble in some build environments. It has been rewritten in a more flexible manner, while still providing full variable compatibility with existing build systems. Distribution packagers are encouraged to migrate over to this one. The **[new configuration manual](download/1.3/doc/configuration.txt)** is almost finished. All keywords and all their options have been documented. Only the logs section remains to be completed. This version has been merged with 1.3.14.2. Some minor robustness and performance tuning parameters have been added, mostly timeouts and backlog.

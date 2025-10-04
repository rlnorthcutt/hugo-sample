---
title: "Kai Krueger reported a nasty problem he encountered and analyzed."
date: 2008-12-04
---

Kai Krueger reported a nasty problem he encountered and analyzed. When a server goes down, it requeues all of its connections waiting in the queue into the global queue. But when a session completes after that, haproxy checks if there are pending connections that this server can handle, without taking into account the fact that the server is dead. So the server can progressively suck all pending connections from the global queue just after it has been marked down. Yes, I know, this is stupid. A check has been added so that it does not dequeue global connections when it's marked down, and releases **[1.3.15.7 and 1.3.14.11](download/1.3/src/)** have been issued. There are very few setups which will trigger this problem, however it's quite annoying for those experiencing it.

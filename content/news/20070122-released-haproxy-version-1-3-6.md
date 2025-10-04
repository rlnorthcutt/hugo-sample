---
title: "Released haproxy version 1.3.6."
date: 2007-01-22
---

Released **haproxy version 1.3.6**. I spent a long time reworking the **HTTP message parser**. It now consists in a **carefully hand-optimized 28-states FSM**. The new code will look awful to _goto_ haters, and will please FSM lovers. It's blazingly fast : parsing and indexing all of the 660 bytes of an HTTP request from _Firefox_ on [Freshmeat](http://freshmeat.net/) only takes 1.94 **microsecond** on my 1.7 GHz Pentium-M notebook, which means it can do it more than **500000 times a second!**

The request code has been cleaned up a lot and adapted to this new FSM. Adding layer7 rules based on new criteria is now trivial. The response code will be ported next, but the code was so much cleaner and faster that it was worth releasing one version before breaking everything. Several bugs were fixed since 1.3.5. I really consider **1.3.6** as the **most likely reliable** 1.3 release to date.

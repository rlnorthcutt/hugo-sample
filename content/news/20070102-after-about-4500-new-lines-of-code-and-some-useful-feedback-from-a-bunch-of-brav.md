---
title: "After about 4500 new lines of code and some useful feedback from a bunch of brave beta-testers, I'm pleased to announce haproxy version 1.3.4 with the new Conte"
date: 2007-01-02
---

After about 4500 new lines of code and some useful feedback from a bunch of brave beta-testers, I'm pleased to announce **[haproxy version 1.3.4](download/1.3/src/)** with the new **Content-Switching features !!!**

It is now possible to select a **backend** (_server pool + load balancing algo_) depending on any parameter in the request, such as **any part of the URI**, the **host name**, etc.... As of now, I've merged Sin Yu's patch to permit switching based on a request regex, but the framework is ready to accept many other criteria. The HTTP request parser has been completely rewritten to support unlimited header inspection, and the statistics page has been rewritten, as can be seen [on the demo page](http://demo.haproxy.org/). It is far from being finished right now, but it seems pretty usable. The server state machine should be adapted though.

There is still no doc, so please note that old configurations do still work, and that in order to switch from an instance to another backend, you need to use "reqisetbe <regex> <new\_proxy>". Also, there's [a config example here](download/1.3/test/) that will be worth any doc.

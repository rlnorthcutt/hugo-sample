---
title: "1.3.16 is getting closer !"
date: 2009-03-10
---

Second release candidate of **[1.3.16](download/1.3/src/Beta/)** has been published. It brings a lot of new long-awaited features, among which TCP splicing support, conditional redirection, TCP content filtering, session rate reporting and limiting, invalid request/response capture, binding to specific network interfaces, per-process affinity for frontends and backends, a monotonic internal clock, and many other features.  
The internals have finally been reworked in layers so that forwarding can be processed without waking high levels up. HTTP is now on top of TCP and not a special case of it. A big advantage of these changes is that we can now touch the socket code without impacting HTTP and vice-versa, which had not yet been possible till there. This means that the risk of future regressions caused by feature additions will be significantly lowered. Thanks to these changes, a lot of complex tricks and specific cases are now handled more cleanly and in a more evolutive manner. New work on keep-alive, SSL integration and QoS will be easier.  
Once 1.3.16 is out, branch 1.3 will become the new stable branch, and support for 1.2 as well as 1.3.14 and 1.3.15 will slowly phase out.

---
title: "Released haproxy version 1.3.14."
date: 2007-12-06
---
Released **[haproxy version 1.3.14](download/1.3/src/)**.

A good part of the changes comes from nice contributors of the [mailing list](https://www.mail-archive.com/haproxy@formilux.org/).

Most sensible changes include support for dynamic server weights offering support for slow start and graceful shutdown.

The load balancer is now able to report its servers state to outer components, enabling the building of more complex multi-site architectures involving dynamic routing protocols such as BGP.

People who were complaining about the rough configuration, rough statistics, or lack of logging to UNIX sockets, should really give this one a try.

Rate of changes after this version should significantly drop in order to progressively switch the tree to a stable state.

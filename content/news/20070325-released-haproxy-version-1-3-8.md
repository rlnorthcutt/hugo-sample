---
title: "Released haproxy version 1.3.8."
date: 2007-03-25
---

Released **[haproxy version 1.3.8](download/1.3/src/)**. Several bugs which might have caused crashes on erroneous configurations have been fixed. The response processing is now completed, which means that real configurations can now be written ; HAProxy 1.3.8 now is at least equivalent to 1.2.17 in terms of features.

Just like with every release, several code optimization have led to small but noticeable performance increases, particularly on very high data bandwidth. The configuration errors are handled more gracefully now with indications about what failed and hints to resolve the issue. HAProxy now builds on MacOS 10.4 thanks to Dan Zinngrabe who provided a makefile. Also, it is now possible to send health checks to an alternate server address, thanks to a patch from Fabrice Dulaunoy.

Users of 1.3 are encouraged to upgrade to 1.3.8 as it both fixes known bugs and converges towards something less tricky than previous versions.

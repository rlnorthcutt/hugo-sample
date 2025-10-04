---
title: "HAProxy 2.8.0 release"
date: 2023-05-31
---

During the development cycle of this new LTS release, behind the curtains the focus was mostly set on all the stuff that can improve the reliability, observability and troubleshooting in field, in a quest to further reduce the number of problem reports. At the most visible layers, QUIC is now considered production ready after having been running on this site for more than a year and with no glitch since 2.7 was released; SSL got new improvements with a much better LetsEncrypt integration, wolfSSL support and OCSP automatic updates; RFC7239 ("forwarded") is supported both in processing and generation; listeners can now span multiple thread groups, setting a new limit of 4096 threads (let's hope we won't have to raise that one in the next two decades). For more details, please have a look at the full article on [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-2-8) and the [more synthetic mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg43600.html).

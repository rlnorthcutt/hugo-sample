---
title: "HAProxy 2.9.0 release"
date: 2023-12-05
---
This release has received a lot of small changes that are difficult to summarize.

Most of them were aimed at improving performance and resource usage in general (zero-copy forwarding, QUIC's smaller footprint for closed connections, improved scalability), others focusing on better integration with other components (support for the AWS-LC crypto library, QUIC OpenSSL compatitility layer, PROXY protocol manipulation), ease of configuration (most log-format tags now have an equivalent sample fetch, some converters support variables in addition to integers, warnings about bad cpu-map or thread settings), more reliability (log backends with checked servers, better debugging), and a really cool new feature to play with, reverse-http.

A lot more details are explained on the [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-2-9), and the [mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg43600.html) summarizes most of these at a higher level.

---
title: "HAProxy 3.2.0 release"
date: 2025-06-24
---
This LTS release improves in a lot of areas.

First, many improvements were made to scale much better on large CPUs with many cores.

The load balancing algorithms, the queues, the stick-tables, the peers are now thread-group aware and will reduce their sharing between CPUs of different groups, and these groups can now be formed automatically to match the hardware topology thanks to the new CPU binding policies.

Outgoing connections may now pick an idle connection from another thread group instead of creating a new connection, resulting in a higher TCP reuse ratio and a lower resource usage.

Memory pools are merged more intelligently and contribute to memory usage reduction.

The latency induced by heavy configs has been further reduced.

Various HTTP improvements such as checking idle connections using PING frames, rules to drop trailers, health checks over idle connections, and improved convergence of H2 and H3 processing.

SSL is easier to configure thanks to the ssl-f-use rules that are common to multiple "bind" lines, and the early support of the ACME protocol for certificates renewal.

QUIC pacing is now really performant and enabled by default, QUIC rx buffers are automatically sized to support much faster (30x) uploads, and Tx memory size can now be capped while being adjusted to match the maximum link speed.

OpenSSL 3.5's QUIC API is supported.

Lua supports receive timeout and queued events, permitting to implement interactive applications (a game is provided as an example).

And many improvements were made to help with live troubleshooting (CLI, glitch counters descriptions, various new "show" commands).

It's better to read the details on the [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-3-2), and the [mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg45917.html).

---
title: "HAProxy 3.0.0 release"
date: 2024-05-29
---

Once again, 3.0 has been a release focusing on polishing a lot of the existing things and sprinkling lots of small new features all around, including crt-stores to ease cert management, GUIDs to config objects for more reliable state manipulation, stats preservation across reloads, syslog load balancing, JSON & CBOR logging, virtual maps/acls, improved performance all over the board (Lua, stick-tables, rings), improved H2/H3 protection against protocol-level attacks. A lot more details are explained on the [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-3-0), and the [mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg44993.html) summarizes most of these at a higher level.

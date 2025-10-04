---
title: "1.4.23 and 1.5-dev18 : security fix"
date: 2013-04-03
---

A vulnerability in all 1.4 and 1.5 releases was fixed in 1.4.23 and 1.5-dev18 ([CVE-2013-1912](http://seclists.org/oss-sec/2013/q2/3)), affecting HTTP fetches in TCP request inspection rules. All 1.4 and 1.5 users must upgrade.

In addition to this, 1.5-dev18 brings a significant number of improvements, among which use of environment variables in all addresses (bind, log, source, server, ...), agent-based health check system, support for systemd, TLS ALPN, and a few other nice features.

Please refer to the [1.4 changelog](/download/1.4/src/CHANGELOG) and [1.5 changelog](/download/1.5/src/CHANGELOG) for more information. Source code is available [here for 1.4](/download/1.4/src/) and [here for 1.5](/download/1.5/src/).

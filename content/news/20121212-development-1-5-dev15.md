---
title: "Development 1.5-dev15"
date: 2012-12-12
---

This is an incremental fixup on top of dev14 to address [the few remaining bugs](/download/1.5/src/CHANGELOG) that were reported since its release, and particularly the high CPU usage that a few users have reported. Some SSL issues were also fixed and its cache was improved to use 4 times less memory. The conditions to enable compression were tightened. The strange server errors that were logged and counted for years were in fact client errors, and that was fixed. SSL handshake errors are now logged. Tracking layer 7 information is now possible ; it was limited to "src" till now. It will allow people behind proxies to benefit from some scraping or DoS protection.

All 1.5-dev users are then encouraged to upgrade to [dev15](/download/1.5/src/).

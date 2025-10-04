---
title: "Worked all the day both in kernel and haproxy to get full transparent proxy to work on Linux."
date: 2008-01-13
---

Worked all the day both in kernel and haproxy to get full transparent proxy to work on Linux. Now, with a small kernel patch, it's possible for haproxy to become completely transparent and just appear as a router, without touching either source nor destination addresses and ports. And all this without NAT, at the same performance level as in normal proxy mode. This will be great for people looking for SMTP/HTTPS/FTP relaying and load balancing. I'm even planning on installing it on my firewall ;-) Stay tuned for the updates, I will soon post the patches once cleaned up.

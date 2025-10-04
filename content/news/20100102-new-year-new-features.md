---
title: "New year, new features"
date: 2010-01-02
---

After several weeks of work, I have [committed](/git?p=haproxy.git;a=commitdiff;h=b608feb82ae08270fa97f435f065942188e7d177) the patch which introduces client-side **HTTP keep-alive and pipelining** support. The code is quite ugly and I'm not proud of it. This is because I got quite a bunch of last-minute surprises that I will have to workaround in a cleaner way. But since the code worked, I would have found it wasted to make you wait for it.  
In order to enable pipelining on the client side, just comment out any "option httpclose" statement in the defaults, frontend and backend sections and set "option http-server-close" in any of them. As the name implies it, the connection is still closed on the server side. This way we can still have low ressource usage on servers and correctly enforce maxconn while retaining keep-alive with the client.  
This code will be in **1.4-dev5** by the end of the week-end, but the impatient will be able to download a [snapshot](/download/1.4/src/snapshot/) for their tests.  
The new code has been put in test on the [Formilux](http://formilux.org/) server and already shows [decent load time savings](http://tools.pingdom.com/?url=http://www.ant-computing.com/album.html&treeview=0&column=objectID&order=1&type=0&save=false) on [this page](http://www.ant-computing.com/album.html). _Stay tuned..._

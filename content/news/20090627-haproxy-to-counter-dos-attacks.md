---
title: "HAProxy to counter DoS attacks"
date: 2009-06-27
---

Since the [announcement of the Slowloris](http://ha.ckers.org/slowloris/) tool, people seem to be discovering how fragile a default Apache setup can be ! Well, this is not news, as people who install Apache on high-traffic sites have been aware of this weakness for ages, and have been setting very low timeouts and disabling keep-alive in order to mitigate risks. Now that a tool is publicly advertised, I'm beginning to hear questions from worried site admins about what to do if their site is attacked. Also, we're seeing several sites and forums suggesting installing HAProxy in front of Apache servers to protect them (note that Nginx would probably do equally well).

Indeed, HAProxy does not need a new thread nor process to accept a new connection, it only needs some RAM (16-32 kB per connection). Some people are already using it past 70000 concurrent connections, which cannot be achieved on Apache which needs an expensive thread or process per connection. More specifically, HAProxy will only forward complete and valid requests. This means that it will not bother Apache while the attacker is playing with its few thousands connections, and all valid requests will immediately pass through. And the _icing on the cake_ is that HAProxy can kill requests which take too much time to complete, using timeout http-request (more than a few seconds is not to be considered normal).

Once again, we observe a derivate use of a load-balancer, which is a bit expected : when a tool is designed to accept 10 times more load than the servers it feeds, there is nothing surprizing that it can be used to protect them ! Let's see if Apache evolves towards providing more tunables to mitigate such attacks... In the mean time, a drop-in anti-DoS configuration is [available here](/download/1.3/examples/antidos.cfg).

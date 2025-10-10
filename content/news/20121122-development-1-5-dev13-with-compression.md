---
title: "Development 1.5-dev13 with Compression!"
date: 2012-11-22
---
This is the largest development version ever issued, 295 patches in 2 months!

We managed to keep the [Exceliance](http://www.exceliance.fr/en/) team busy all the time, which means that the code is becoming more modular with less cross-dependences, I really like this !

First, we got an amazing amount of feedback from early adopters of dev12.

It seems like SSL was expected for too long a time.

We really want to thank all those who contributed patches, feedback, configs, cores (yes there were) and even live gdb access, you know who you are and you deserve a big thanks for this!

Git log says there were 55 bugs fixed since dev12 (a few of them might have been introduced in between).

Still, this means that dev12 should be avoided as much as possible, which is why I redirected many of you to more recent snapshots.

These bugs aside, I'm proud to say that the whole team did a really great job which could be summarized like this :

1.  SSL:
    *   many more features ; client and server certificates supported on both sides with CA and CRL checks. Most of the information available in SSL can be used in ACLs for access control. Some information such as protocol and ciphers can be reported in the logs. These information are still not added to HTTP logs though, a lot of config work is still needed.
    *   cache life time and maximum concurrent SSL connections can be set. Unfortunately OpenSSL happily dereferences NULL malloc returns and causes the process to die if memory becomes scarce. So we can only limit its maximum amount of connections if we want to limit the memory it uses.
    *   TLS NPN was implemented with the help from Simone Bordet from Jetty, and can be used to offload SSL/TLS for SPDY and to direct to a different server depending on the protocol chosen by the client.
    *   Ivan Ristic from [ssllabs](https://www.ssllabs.com/) and Andy Humphreys from Robinson-way provided very valuable help in diagnosing and fixing some nasty issues with aborts on failed handshakes and improve [from an E-grade to an A-grade](https://www.ssllabs.com/ssltest/analyze.html?d=demo.haproxy.org).
2.  HTTP Compression
    *   HTTP payload compression was implemented at Exceliance to achieve bandwidth usage reduction and reduce page load time on congested or small links. Compression is extremely CPU and memory intensive, so we spent most of the time developing dynamic adaptations. It is possible to limit the maximum RAM dedicated to compression, the CPU usage threshold and bandwidth thresholds above which compression is disabled. It is even possible to adjust some of these settings from the stats socket and to monitor bandwidth savings in real time. Proceeding like this ensures a high reliability at low cost and with little added latency. I've put it on the haproxy web site with nice bandwidth savings (72% avg on compressible objects, 50% on average, considering that most downloads are compressed sources). I must say I'm very happy of this new feature which will reduce bandwidth costs in hosted infrastructures ! And it goes back to the origins of haproxy in zprox 14 years ago :-)
3.  Health checks
    *   SSL is now usable with health checks. By default it is enabled if the server has the "ssl" keyword and no "port" nor "addr" setting. It can be forced using "check-ssl" otherwise. So now running an HTTPS health check simply consists in using "option httpchk" with "ssl" on the server.
    *   send-proxy is also usable with health checks, with the same rules as above, and the "check-send-proxy" directive to force it. The checks also respect the updated spec which suggests sending real addresses with health checks instead of sending unknown addresses. This makes it compatible with some products such as postfix 2.10 for example.
4.  Polling
    *   speculative polling was generalized to all pollers, and sepoll disappeared as it was superseded by epoll. The main reason for this important change is the way OpenSSL works and the fact that it can easily get stuck with some data in buffers with no I/O event to unblock them. So we needed to engage into this difficult change. I'd have preferred to delay it to 1.6 if I was offered the choice ! But in the end this is good because it's done and it improves both performance and reliability. Even select() and poll() are now fast.
    *   the maxaccept setting was too low on some platforms to achieve the highest possible performance, so it was doubled to 64 and is now per listener so that it automatically adjusts to the number of processes the listener is bound to. This ensures both best performance in single process mode, and quite good fairness in multi-process mode.
5.  Platform improvements
    *   Linux 3.6 TCP Fast Open is supported on listeners ("tfo" bind keyword). This is used to allow compatible clients to re-establish a TCP connection in a single packet and save one round-trip. The kernel code for this is still young, I'd be interested in any feedback.
    *   use of accept4() on Linux >= 2.6.28 saves one system call.
6.  Process management
    *   stats socket can now be bound to specific processes. This is useful to monitor a specific process only.
    *   "bind-process" now supports ranges instead of silently ignoring them.
    *   "cpu-map" establishes a mapping between process numbers and CPU cores. This is important when running SSL offloaders on dedicated processes because you don't want them to pollute the low-latency L7 core.
7.  Misc : "redirect scheme" makes it easier to redirect between http and https, config error reporting was improved for "bind" and "server" lines by enumerating the list of supported options dynamically.

I must say I'm much more confident in dev13 than I was with dev12 and I have already upgraded the main web site which has been upgraded every few days with recent snapshots.

I've build and run it on Linux i586/x86\_64/armv5/v7, OpenBSD/amd64 and Solaris/sparc without any issue anymore.

To all those running SSL tests on dev12, please drop it for dev13.

I don't think we introduced regressions (but that's still possible), but I know for sure that we fixed a lot!

The usual [changelog](/download/1.5/src/CHANGELOG) and [source](/download/1.5/src/) are available at the usual place.

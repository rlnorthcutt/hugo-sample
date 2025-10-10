---
title: "Released haproxy versions 1.3.15.1 and 1.3.14.5 with minor fixes : build fix for GCC 4.3, fix for early truncate of stats output in certain circumstances, and b"
date: 2008-05-25
---
Released **[haproxy versions 1.3.15.1 and 1.3.14.5](download/1.3/src/)** with minor fixes : build fix for GCC 4.3, fix for early truncate of stats output in certain circumstances, and better handling of large amounts of highly active sockets.

I indeed discovered during testing that the **sepoll** poller was so much efficient that when running at gigabit speed with 80000 active sockets fighting for their CPU share, almost all of them were running in speculative mode, causing starvation of the remaining ones, which in turn caused the accept() call to be very rarely called.

Delays of about 40 seconds have been observed on a 3.4 GHz Pentium 4 to get the stats page under such a load.

The other pollers were not better BTW.

The fix consisted in ensuring that polled events are checked at much often as the speculative ones.

With this fix, the stats page responds in less than one second on such a saturated machine.

There is still room for improvement relying on events prioritization though.

Version 1.3.15 has been promoted as the recommended one since there has been no regression report.

Version 1.2.18 was also released for users of 1.2 which experienced trouble building on BSD.

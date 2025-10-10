---
title: "Stable 1.3.26 and status updates"
date: 2011-08-06
---
Previous 1.3 version was released 14 months ago, the same day as 1.4.8.

Since then, a number of fixes went into 1.4 and [a part of them were queued for 1.3](/download/1.3/src/CHANGELOG).

These fixes are not \*that much\* important but are still worth a release.

Thus, both 1.3.26 and 1.3.15.13 were released and are available as [source](/download/1.3/src/) and [precompiled binaries](/download/1.3/bin/) for Linux/x86 and Solaris/sparc.

I realized that I don't use 1.3 anymore myself, and for this reason I'm afraid of the risk of introducing regressions with future backports.

So I decided that it was time to turn 1.3 into a "**critical fixes only**" status after 2.5 years of stable releases and 5 years of existence, meaning that minor fixes will probably never get there anymore, and that future releases, if any, will be focused on important bugs.

That does not mean it's not supported anymore, but that fixes will come at a very slow pace and that new deployments are encouraged to use 1.4 if they expect a responsive support.

I'm also switching the 1.3.14 and 1.2 branches to the "**unmaintained**" status since nobody appears to be using them anymore (last fixes were more than 2 and 3 years ago respectively).

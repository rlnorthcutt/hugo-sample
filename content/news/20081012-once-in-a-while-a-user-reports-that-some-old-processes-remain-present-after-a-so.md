---
title: "Once in a while, a user reports that some old processes remain present after a soft-restart."
date: 2008-10-12
---
Once in a while, a user reports that some old processes remain present after a soft-restart.

I could never reproduce the issue until Manuel Soto sent me a truss output of a configuration with which the problem reproduces frequently.

The cause is finally that haproxy still binds listening addresses to disabled instances, but does not try to stop them and refuses to exit as long as they remain present.

I took the opportunity to fix a related problem causing warnings to be emitted when haproxy tried to stop backends, and a segfault in the configuration parser if ACLs were declared in a defaults section.

That was enough to release **[1.3.15.5 and 1.3.14.9](download/1.3/src/)**.

I recommend that any user of 1.3.14 or 1.3.15 upgrades, as these fixes present very minor risk and fix really annoying problems.

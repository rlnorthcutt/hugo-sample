---
title: "Released haproxy version 1.3.15 with many new features."
date: 2008-04-19
---
Released **[haproxy version 1.3.15](download/1.3/src/)** with many new features.

The most important changes are stats updates (HTTP and UNIX), enhancements of server checks such as tracking and dynamic intervals, addition of the leastconn load-balancing algorithm, a fully transparent mode on Linux, better handling of connection failures (dead server avoidance and turn-around state), support for inter-site off-loading through redirects, updates to the build process, and large documentation updates.

For more information, please check the [ChangeLog](download/1.3/src/CHANGELOG).

Due to the important number of changes, upgrade from earlier versions should be performed with a bit of care.

Once again, a lot of code comes from contributions.

I'd like to specially thank _Krzysztof Oledzki_ for a lot of useful contributions, including the **SNMP agent**, and the guys at _Nokia_ for the good work they have done on **POST parameter hashing**.

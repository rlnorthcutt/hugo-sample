---
title: "Released haproxy version 1.3.12.1."
date: 2007-09-05
---

Released **[haproxy version 1.3.12.1](download/1.3/src/)**. It fixes a few bugs discovered in 1.3.12, notably one which could lead to crashes under Linux with speculative I/O when clients disconnect before the connection has been established to the server. As a workaround, it is possible to specify "**nosepoll**" in the "**global**" section. A "**stats refresh <interval>**" option has also been added because some people like to have the stats page automatically refresh. It's also possible to hide all failed servers on the stats page now. This version also contains the **[new configuration manual](download/1.3/doc/configuration.txt)** which has just been started but which helps understand how to use ACL.

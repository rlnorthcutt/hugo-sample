---
title: "Several minor bug fixes were pending since 1.3.15.7, so it was time to release 1.3.15.8 and 1.3.14.12."
date: 2009-03-09
---

Several minor bug fixes were pending since 1.3.15.7, so it was time to release **[1.3.15.8 and 1.3.14.12](download/1.3/src/)**. Those bugs are not stability bugs, rather load-time bugs (config parsing, etc...). Only one of them really justifies updating : if your configuration uses the **"track"** keyword in order to synchronize multiple servers states, the time taken to synchronize them grows with the number of servers. Among the changes, a backport of the doc updates was merged, covering the log format, so that the old docs should normally not be needed anymore.

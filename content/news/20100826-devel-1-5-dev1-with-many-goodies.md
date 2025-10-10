---
title: "devel 1.5-dev1 with many goodies"
date: 2010-08-26
---
Three months ago I was approached by the [Stack Overflow Team](http://blog.serverfault.com/) team who needed to get some improvements in HAProxy.

Overall, their needs would have been addressed by the final release of version 1.5 scheduled around the end of the year, but having to wait that long was not practical due to some architectural constraints imposed by an intermediate solution.

They proposed that we find an agreement on which we could work together.

Since we were already having productive exchanges for some time, and I knew they were good guys (after all they already [donated](http://blog.stackoverflow.com/2009/12/) to the project last year), I accepted the deal.

Also, I must say that as a software engineer, it's always a lot better to have someone explain their needs with high expectations than having to guess how a feature will be used.

[Geoff Dalgas](http://stackoverflow.com/users/2/geoff-dalgas) and [Jeff Atwood](http://stackoverflow.com/users/1/jeff-atwood) described to me in great details what they needed to do : perform request throttling per IP address, possibly based on various criteria, in order to limit risks of service abuse.

That was very interesting, because that feature was being thought about for about 4 years without enough time to completely develop it, and also the new stickiness framework that was contributed by [Exceliance](http://www.exceliance.fr/) and [Loadbalancer.org](http://loadbalancer.org/) was making that really possible, although an important design rework had to be operated first within the code.

During the tests with Geoff and [Kyle Brandt](http://serverfault.com/users/2561/kyle-brandt), it appeared that some more changes had to be operated to be able to store any criteria in the tables (eg: bandwidth per IP address), and to be able to consult and change the table contents at runtime, leading to a more and more generic code.

Kyle has been very patient and comprehensive, I think I have changed the mechanisms and configuration syntax at least 5 or 6 times during the tests, but he always took the time to understand the changes and adapt his configurations.

If I had been at his place, I would have got bored earlier, so I owe him a big thanks for his patience !

Now the code has been running fine in production overthere, so it's time to release it and merge it into the master branch.

I won't extend further on how it works, since Kyle has put an [excellent explanation](http://blog.serverfault.com/post/1016491873/better-rate-limiting-for-all-with-haproxy) on his blog that is a lot more clear than the doc (that reminds me that the architecture guide really needs some lifting).

I'll add quick status on the current code.

Some core changes that I wanted to do earlier will now start.

But that means that 1.5-dev1 should be as stable as 1.4.8.

I'm not saying that I would suggest to anyone to push it into production, but it can clearly be used to mitigate DDoS attacks as well as stop service abuses.

I could get it to stop connection floods slightly above 200000 connections per second (yes, two hundreds thousands) and let the good traffic pass through.

So for this reason, I think that people who are regularly exposed to such trouble may find it useful to keep it handy.

Now what's next ?

Right now the data in the tables is local to one process, so it is not shared if you start multiple processes, nor it is across reloads.

The second step of the stickiness extensions developped by Exceliance and Loadbalancer.org will include stickiness table synchronization between multiple hosts.

Some work will still be needed to be able to share counters, but since this development is done in a flexible way, it should not be too hard to adapt it later.

BTW, I also owe a big kudos to the [Git versionning system](http://git-scm.com/), which has made it very easy to rework my patches after every change and bugfix until they were looking good, through massive abuse of branching and rebasing.

Too much talk.

The code is available [here](/download/1.5/src/devel/), the ChangeLog [is here](/download/1.5/src/CHANGELOG) and the doc is [here](/download/1.5/doc/).

Since this is a development version, no binary is provided.

The last words naturally go to the really cool guys at [Stack Overflow](http://blog.serverfault.com/).

It's very nice to see some sites and companies involve time and money and take risks to make Open Source products better.

Of course they benefit from this work, but at no point during the whole development did they try to reduce the focus to their specific needs, quite the opposite.

From the very first exchanges, their goal clearly was to make the product better, and that must be outlined.

That's now achieved and I really appreciate their involvement.

Thank you guys !

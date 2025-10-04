---
title: "Released haproxy version 1.3.10."
date: 2007-05-09
---

Released **[haproxy version 1.3.10](download/1.3/src/)**. This one adds ACL, SMTP health checks (thanks to Peter van Dijk), and URI hashing (thanks to Guillaume Dallaire). Also, the rbtree was replaced with a much faster tree, leading to an overall performance boost around 5%.

The speculative I/O processing in 1.3.9 has introduced some bugs which have been fixed in this version. I feel confident that latest changes have brought their pile of bugs too. I will probably spend some time soon to do cleanup and stabilization work, eventhough both are not really compatible.

I also want to **thank all the people who contribute** code and testing. You are more and more at each release. I'm impatient to clean up the remains of the old code, so that even more people can contribute code. Interestingly, all contributions till now were of high quality. This is probably induced by some sort of selection caused by the technical aspect of the product, and the skills required to use the development version. _Thanks again to you all !_

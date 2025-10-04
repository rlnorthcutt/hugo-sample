---
title: "Broke new performance record: 2 million req/s & 100 Gbps"
date: 2021-04-08
---

There was no performance report published since the 100k req/s milestone 12 years ago... So here is a great one: [2 million HTTPS requests forwarded per second, and 100 Gbps of bandwidth](https://www.haproxy.com/blog/haproxy-forwards-over-2-million-http-requests-per-second-on-a-single-aws-arm-instance/) achieved on AWS's c6gn instances running the 64-core ARM Graviton2 CPUs. This shows that our thread scalability has massively improved since threads made their entry in 1.8, it's immensely rewarding for all those who spent countless hours chasing nanosecond and scratching their heads to eliminate lock after lock! And it confirms if it was still needed that the old multi-process model can now rest in peace, being completely obsolete by 2021's standards.

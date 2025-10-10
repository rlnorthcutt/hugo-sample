---
title: "HAProxy 1.6.0 now released!"
date: 2015-10-13
---
HAProxy 1.6.0 has been released.

It includes a lot of new features gathered from many contributors during 16 months of development and stabilization.

There are too many features to list here.

More than 1150 commits were merged from 59 people, and 2/3 came from HAProxy Technologies, meaning that the remaining 1/3 came from the rest of the community, explaining the faster development rate.

Among the most user-visible changes, we can cite the simpler handling of multiple configuration files, the support for quotes and environment variables in the configuration, a significant reduction of the memory usage thanks to a new dynamic buffer allocator, notifications over e-mail, server state keeping across reloads, dynamic DNS-based server address resolution, new scripting capabilities thanks to the embedded Lua interpreter, use of variables in the configuration to manipulate samples, request body buffering and analysis, support for two third-party device identification products (DeviceAtlas and 51Degrees), a lot of new sample converters including arithmetic operators and table lookups, TLS ticket secret sharing between nodes, TLS SNI to the server, full tables replication between peers, ability to instruct the kernel to quickly kill dead connections, support for Linux namespaces, and a number of other less visible goodies.

The performance has also been improved a lot with support for server connection multiplexing, much faster and cheaper HTTP compression via libslz, and the addition of a pattern cache to speed up certain expensive ACLs.

The great flexibility offered by this version will allow many users to significantly simplify their configurations.

Some users will notice a huge performance boost after they enable the features designed for them.

This release also marks the opening of the 1.6-stable branch and the 1.7-dev branch which is where new development will be done.

The next release date for 1.7.0 is set to end of September 2016, or approximately one year.

This time, in order to satisfy more contributors, we'll have a 3-phase development cycle.

The first phase ending in March 2016 will merge the most sensitive changes, possibly causing a lot of breakage.

It is only for developers.

A second phase, ending in June, will be dedicated to fixing the breakage and will still allow small improvements to be made as long as they are not expected to cause regressions.

It is possibly where we will decide to revert some of the early breakage if some features are too broken.

Enthousiasts may start to test during this phase and report issues.

The last phase ending in September will be dedicated to the final polishing, portability issues and doc updates, and should be acceptable for most early adopters.

So let's get back to the whiteboards now.

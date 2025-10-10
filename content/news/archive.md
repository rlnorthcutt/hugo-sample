**Jun, 24th, 2025** : **HAProxy 3.2.0 release**

This LTS release improves in a lot of areas.

First, many improvements were made to scale much better on large CPUs with many cores.

The load balancing algorithms, the queues, the stick-tables, the peers are now thread-group aware and will reduce their sharing between CPUs of different groups, and these groups can now be formed automatically to match the hardware topology thanks to the new CPU binding policies.

Outgoing connections may now pick an idle connection from another thread group instead of creating a new connection, resulting in a higher TCP reuse ratio and a lower resource usage.

Memory pools are merged more intelligently and contribute to memory usage reduction.

The latency induced by heavy configs has been further reduced.

Various HTTP improvements such as checking idle connections using PING frames, rules to drop trailers, health checks over idle connections, and improved convergence of H2 and H3 processing.

SSL is easier to configure thanks to the ssl-f-use rules that are common to multiple "bind" lines, and the early support of the ACME protocol for certificates renewal.

QUIC pacing is now really performant and enabled by default, QUIC rx buffers are automatically sized to support much faster (30x) uploads, and Tx memory size can now be capped while being adjusted to match the maximum link speed.

OpenSSL 3.5's QUIC API is supported.

Lua supports receive timeout and queued events, permitting to implement interactive applications (a game is provided as an example).

And many improvements were made to help with live troubleshooting (CLI, glitch counters descriptions, various new "show" commands).

It's better to read the details on the [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-3-2), and the [mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg45917.html).

**Feb, 26th, 2025** : **HAProxyConf 2025 Early birds registration**

Early birds registration for [HAProxy Conf 2025](https://www.haproxyconf.com/) is now available!

Please check the link to book your tickets.

**Nov, 26th, 2024** : **HAProxy 3.1.0 release**

This release brings a number of troubleshooting improvements.

For example it offers new sample fetch methods to report information about last rule, termination states and syscall statuses in logs, it allows to filter only on anomalies, and exposes more info to the CLI ("show dev", "show sess show-uri"), it now officializes the "traces" section allowing to capture traffic and debugging info permanently, as well as to correlate traces between back and front, and even counts the number of passes on certain key points in the code.

On the terrain of configuration stability, the watchdog will now warn early before killing so as to more easily spot dangerous configs, suspiciously low timeouts will now raise a warning suggesting to specify the units, a new hard-limit to file descriptors allows to better adapt to some unbound container environments and duplicate config object names will produce warnings.

Architectural improvements were not put at rest, with a new master-worker model that saves a re-exec and is more reliable, the rewrite of the SPOE engine to rely on a much more efficient mux that opens it to all LB algorithms, queuing etc, further improved clock accuracy, the arrival of pacing in QUIC for much higher performance by a massive reduction of losses, the BBR congestion control algorithm, and a 24x performance boost on POST uploads over H2 thanks to adaptive Rx window.

There are many other things that would take too long to enumerate here, so please read the details on the [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-3-1), and the [mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg45435.html).

**Sep, 18th, 2024** : **HAProxyConf 2025 Call for Papers**

The next edition of the HAProxyConf will be held on June 4-5 2025, with some workshops on June 3.

The [Call for Papers is open](https://www.haproxyconf.com/call-for-papers/).

If you feel like you're doing awesome things with HAProxy, that it eases your job, reduces your costs, if you think you've figured smart ways to use it and want to share your findings, if you've written useful companion tools that your friends constantly tell you you should advertise more, and even if you want to express some criticism, please consider submitting a paper to the link above.

If you just want to attend, see where it's held, how to get there or register, you can also [visit the conference's site](https://www.haproxyconf.com/) (registrations are expected to open very soon).

**May, 29th, 2024** : **HAProxy 3.0.0 release**

Once again, 3.0 has been a release focusing on polishing a lot of the existing things and sprinkling lots of small new features all around, including crt-stores to ease cert management, GUIDs to config objects for more reliable state manipulation, stats preservation across reloads, syslog load balancing, JSON & CBOR logging, virtual maps/acls, improved performance all over the board (Lua, stick-tables, rings), improved H2/H3 protection against protocol-level attacks.

A lot more details are explained on the [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-3-0), and the [mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg44993.html) summarizes most of these at a higher level.

**Dec, 5th, 2023** : **HAProxy 2.9.0 release**

This release has received a lot of small changes that are difficult to summarize.

Most of them were aimed at improving performance and resource usage in general (zero-copy forwarding, QUIC's smaller footprint for closed connections, improved scalability), others focusing on better integration with other components (support for the AWS-LC crypto library, QUIC OpenSSL compatitility layer, PROXY protocol manipulation), ease of configuration (most log-format tags now have an equivalent sample fetch, some converters support variables in addition to integers, warnings about bad cpu-map or thread settings), more reliability (log backends with checked servers, better debugging), and a really cool new feature to play with, reverse-http.

A lot more details are explained on the [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-2-9), and the [mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg43600.html) summarizes most of these at a higher level.

**May, 31th, 2023** : **HAProxy 2.8.0 release**

During the development cycle of this new LTS release, behind the curtains the focus was mostly set on all the stuff that can improve the reliability, observability and troubleshooting in field, in a quest to further reduce the number of problem reports.

At the most visible layers, QUIC is now considered production ready after having been running on this site for more than a year and with no glitch since 2.7 was released; SSL got new improvements with a much better LetsEncrypt integration, wolfSSL support and OCSP automatic updates; RFC7239 ("forwarded") is supported both in processing and generation; listeners can now span multiple thread groups, setting a new limit of 4096 threads (let's hope we won't have to raise that one in the next two decades).

For more details, please have a look at the full article on [HAProxyTech's blog](https://www.haproxy.com/blog/announcing-haproxy-2-8) and the [more synthetic mailing-list announcement](https://www.mail-archive.com/haproxy@formilux.org/msg43600.html).

**February, 14th, 2023** : **CVE-2023-25725 fixed!**

We've been notified of a vulnerability in HAProxy that can be exploited to build some request smuggling attacks.

It affects all currently supported branches, all the details are [here on the mailing list announce](https://www.mail-archive.com/haproxy@formilux.org/msg43229.html).

Please make sure to update either to your latest distro package or to latest version if you build from the sources (2.0.31, 2.2.29, 2.4.22, 2.5.12, 2.6.9, 2.7.3 or 2.8-dev4).

**December, 1st, 2022** : **HAProxy 2.7.0 release**

HAProxy 2.7.0 is now released and available for download, opening the way to 2.8-dev.

2.7 provides traffic shaping, many QUIC improvements, eases the switch to alternate SSL libraries, and improves user experience with everything related to troubleshooting and issue reporting.

Please see the [announnce](https://www.mail-archive.com/haproxy@formilux.org/msg42914.html) for more details and/or consult the [HAProxyTech blog article](https://www.haproxy.com/blog/announcing-haproxy-2-7/) for more details.

**June, 16th, 2022** : **HAProxyConf: Call for Papers**

This year, [HAProxyConf 2022](https://www.haproxyconf.com/) will be held physically so that we can meet in person, just as we did in 2019!

It will be held in Paris from November 8th to 9th.

The Call for Papers is now open and ends on September 5th.

Better not wait too much if you already have an idea in mind.

There's a [simplified form](https://www.haproxyconf.com/call-for-papers/#submission-form) to fill to propose a talk.

It doesn't ask much, just your contact and a quick abstract.

If you have no idea yet, think about some great things or tricks you've achieved using HAProxy, or all the stuff tha made your friends tell you "you should really blog about it".

Remember, you have one month and it's counting...

**May, 31st, 2022** : **HAProxy 2.6.0 release**

HAProxy 2.6 is now the latest long-term supported release.

It further improves reliability, and focused on making future contributions easier by simplifying some of the internals, and completing the native HTTP client, allowing easier interactions with external services.

And the star of this release is undoubtly the long-awaited support for the QUIC protocol!

The full details are [detailed here](https://www.mail-archive.com/haproxy@formilux.org/msg42371.html) in the announce.

**Mar, 26th, 2022** : **QUIC experimentation**

One front that made impressive progress over the last few months is QUIC.

While a few months ago we were counting the number of red boxes on the interop tests at [https://interop.seemann.io/](https://interop.seemann.io/) to figure what to work on as a top priority, now we're rather counting the number of tests that report a full-green state, and haproxy is now on par with other servers in these tests.

Thus the idea emerged, in order to continue to make progress on this front, to start to deploy QUIC on haproxy.org so that interoperability issues with browsers and real-world traffic can be spotted.

A few attempts were made and already revealed issues so for now it's disabled again.

Be prepared to possibly observe a few occasional hiccups when visiting the site (and if so, please do complain to us).

The range of possible issues would likely be frozen transfers and truncated responses, but these should not happen.

From a technical point, the way it's done is by having a separate haproxy process listening to QUIC on UDP port 1443, and forwarding HTTP requests to the existing process.

The main process constantly checks the QUIC one, and when it's seen as operational, it appends an Alt-Svc header that indicates the client that an HTTP/3 implementation is available on port 1443, and that this announce is valid for a short time (we'll leave it to one minute only so that issues can resolve quickly, but for now it's only 10s so that quick tests cause no harm):

    http-response add-header alt-svc 'h3=":1443"; ma=60' if { var(txn.host) -m end haproxy.org } { nbsrv(quic) gt 0 }

As such, compatible browsers are free to try to connect there or not.

Other tools (such as git clone) will not use it.

For those impatient to test it, the QUIC process' status is reported at the bottom of the stats page here: [http://stats.haproxy.org/](http://stats.haproxy.org/).

The "quic" socket in the frontend at the top reports the total traffic received from the QUIC process, so if you're seeing it increase while you reload the page it's likely that you're using QUIC to read it.

In Firefox I'm having this little plugin loaded: [https://addons.mozilla.org/en-US/firefox/addon/http2-indicator/](https://addons.mozilla.org/en-US/firefox/addon/http2-indicator/).

It displays a small flash on the URL bar with different colors depending on the protocol used to load the page (H1/SPDY/H2/H3).

When that works it's green (H3), otherwise it's blue (H2).

For Chrome there is [HTTP Indicator](https://chrome.google.com/webstore/detail/hgcomhbcacfkpffiphlmnlhpppcjgmbl) which does the same but displays an orange symbol when using H3.

Chrome only accepts H3 on port 443 (which we enabled as well for it).

Note that H2 and H3 are only served when the site is browsed in HTTPS at [https://haproxy.org/](https://haproxy.org/).

At this point I'd still say "do not reproduce these experiments at home".

Amaury and Fred are still watching the process' traces very closely to spot bugs and stop it as soon as a problem is detected.

But it's still too early for being operated by non-developers.

The hope is that by 2.6 we'll reach the point where enthousiasts can deploy a few instances on not-too-sensitive sites with sufficient confidence and a little dose of monitoring.

**Nov, 23th, 2021** : **HAProxy 2.5.0 release**

HAProxy 2.5 is now the latest stable release.

It further improves runtime updates, flexibility and performance.

The full story is [detailed here](https://www.mail-archive.com/haproxy@formilux.org/msg41508.html) in the announce.

**November 5th, 2021** : **Cool hardware donation from Zerodha**

Just after the HAProxy 2.4.0 release in May this year, Kailash Nadh, CTO of [Zerodha](https://zerodha.com) contacted me and offered to donate a pair of [SolidRun HoneyComb LX2 boards](https://www.solid-run.com/arm-servers-networking-platforms/honeycomb-workstation/) to help us continue to improve out threading scalability.

With 16 ARM cores, 32GB RAM, 64GB eMMC, 4x10GbE, and PCI-e in a tiny and quiet form factor, there definitely is plenty of potential to emphasize the cost of contention and to further improve our data model and our algorithms!

As usual with SolidRun, the hardware design is really awesome (it feels like you're installing a PC, and they're about the only ones featuring the console port).

However I must say I was really disappointed by their complete absence of communication during the 5 months it took to ship the board.

Vishnu of Zerodha and me probably asked them for status updates 8 times in total and each time we were told "we'll contact you when it ships, no need to ask all the time".

Last time we were told the parcel had been sent two weeks ago to DHL who had no way to contact me... no comment!

Emailing a tracking number doesn't cost much, especially when their own tracking site still shows the order as "processing" after I received it!

Hopefully SolidRun manages to address this deficiency in the future because right now they're among the very few who make affordable server-grade development boards and I hope to continue to be able to order their great products without trouble...

Anyway, more news later when the tests really begin!

For now the boards boot and are fast (hint: haproxy-2.5 builds in 6 sec).

Many big thanks to Kailash and Vishnu of Zerodha for this very kind contribution!

[![](/img/lx2-150.jpg)](/img/lx2-1k.jpg)

**November 3rd, 2021** : **HAProxyConf 2021 is in less than two weeks!**

The conference is still scheduled for November 16-17 and will be free to watch on [https://www.haproxyconf.com/](https://www.haproxyconf.com/), with live Q&A sessions after each talk.

The list of [speakers](https://www.haproxyconf.com/speakers/) and their [presentations](https://www.haproxyconf.com/presentations/) is already published.

The conference schedule is being finalized and is to be published in the forthcoming days, please check the site to stay up to date, or register to be notified about last-minute updates.

See you soon!

**May, 14th, 2021** : **HAProxy 2.4.0 release**

HAProxy 2.4 is now the latest LTS release.

It comes with lots of new stuff making it more dynamic, more user-friendly, more reliable, more flexible, and more scalable.

Please check the [announce here](https://www.mail-archive.com/haproxy@formilux.org/msg40499.html) for the details.

**April 8th, 2021** : **Broke new performance record: 2 million req/s & 100 Gbps**

There was no performance report published since the 100k req/s milestone 12 years ago...

So here is a great one: [2 million HTTPS requests forwarded per second, and 100 Gbps of bandwidth](https://www.haproxy.com/blog/haproxy-forwards-over-2-million-http-requests-per-second-on-a-single-aws-arm-instance/) achieved on AWS's c6gn instances running the 64-core ARM Graviton2 CPUs.

This shows that our thread scalability has massively improved since threads made their entry in 1.8, it's immensely rewarding for all those who spent countless hours chasing nanosecond and scratching their heads to eliminate lock after lock!

And it confirms if it was still needed that the old multi-process model can now rest in peace, being completely obsolete by 2021's standards.

**July 7th, 2020** : **HAProxy 2.2.0 is ready!**

HAProxy 2.2 is the latest LTS release, delivered few weeks late, but for good given that many early bugs were addressed during this time!

New features include runtime certificate addition and crtlist management, dynamic error pages and return statements, logging over TCP, refined idle connection pools saving server resources, extensible health checks, improved I/O processing and scheduling for even lower latency processing, even more debugging information.

Please check the [announce here](https://www.mail-archive.com/haproxy@formilux.org/msg37852.html) for more details.

**November 25th, 2019** : **HAProxy 2.1.0 is out!**

Delivered on time, for once, proving that our new development process works better.

In short this provides hot-update of certificates, FastCGI to backends, better performance, more debugging capabilities and some extra goodies.

Please check the [announce here](https://www.mail-archive.com/haproxy@formilux.org/msg35491.html) for more details.

**September 9th, 2019** : **HAProxyConf**

[HAProxyConf](http://haproxyconf.com/) full speaker list and agenda is announced.

Early Bird tickets will be on sale until September 30th, at a price of EUR175.

**June 21th, 2019** : **Call for papers slightly extended**

The call for papers for the [HAProxyConf 2019](http://haproxyconf.com/) was extended by one weak so that late proposals can still be considered.

Unsurprizingly most submissions started to arrive close to the deadline so it's definitely worth waiting a few more days.

**June 16th, 2019** : **HAProxy 2.0.0 is out!**

No that's not a typo, it's really **2.0.0**!

It comes with plenty of shiny new features and scalability improvements, too many to list here, better [read this announcement](https://www.mail-archive.com/haproxy@formilux.org/msg34215.html) instead!

By the way, it's the last week to [send your proposals for the HAProxyConf 2019](http://haproxyconf.com/), please don't forget!

**May 22th, 2019** : **HAProxyConf 2019 - Call for Papers**

We are very pleased to announce our first-ever user conference, HAProxyConf 2019 which will take place in Amsterdam on November 12 and 13.  
We are designing this conference with our community in mind. All sessions will be highly informative and technical in nature, without marketing fluff. There will be a heavy focus on presentations from end-users, who will share their use cases and real-world recommendations. We also expect the conference to be a fun time and a great opportunity to connect with several hundred of your peers from across Europe and beyond.  
We very much want our community members to play a big role in the conference. With that in mind, please consider submitting an abstract as part of our call-for-papers process, which is now open. You can submit your abstracts by visiting the [conference website](http://haproxyconf.com/). Please note that any submissions that are obviously vendor or product pitches will not be considered by the content selection committee. Abstracts much be submitted by June 21, 2019. All chosen presenters will receive a free, full conference pass.  
If you have any questions about the conference or the call-for-papers process, please contact us at [submission@haproxy.com](mailto:submission@haproxy.com).

**December 19th, 2018** : **HAProxy 1.9.0 released**

One year after 1.8.0 comes 1.9.0.

This one's primary target is a significant technical improvement over 1.8, bringing much higher multi-threaded performance, improvements on connection management, process management, caching, H2...

Please read [the announcement here](https://www.mail-archive.com/haproxy@formilux.org/msg32143.html) and [the detailed blog article](https://www.haproxy.com/blog/haproxy-1-9-has-arrived/) for more information.

An important point to note, this technical release is not suitable for inclusion in distros, as it will only be maintained for approximately one year (till 2.1 is out).

Version 2.0 coming in May will be long-lived and more suitable for distros.

**November 26th, 2017** : **HAProxy 1.8.0 released**

One year after 1.7.0, we're pleased to announce release 1.8.0, which is by far the most feature-rich version ever produced.

Read [the announcement here](https://www.mail-archive.com/haproxy@formilux.org/msg28004.html) for more information.

**June 23th, 2017**

The "Links" section in the [version table](http://www.haproxy.org/) now provides a link to the public announce of each version on the list.

This will ensure that all versions are always covered in details for everyone.

The News section will only be updated for breaking news, and not for every new minor release anymore.

**February 28th, 2017** : _1.7.3_

HAProxy 1.7.3 was released on 2017-02-28.

It fixes a few remaining bugs affecting 1.7, mostly related to DNS, Lua, header rewriting, and compression for the more serious ones.

A few other minor issues were addressed.

For the details, please check [the announcement here](https://www.mail-archive.com/haproxy@formilux.org/msg25066.html).

Code and changelog are available [here](/download/1.7/src/) as usual.

**December 25th, 2016** : _1.6.11 and 1.5.19_

There was nothing really critical on the 1.6 front but a number of fixes were pending among which some against painful bugs when hitting out of memory conditions.

1.5 had been lagging for quite longer and received fixes against a few risks of crashes when misusing sc\_trackers, another rare crash in zlib not happening with slz, some situations where random connections can be frozen during a redispatch, and an issue with gcc 6 where the listening address could be ignored.

For more info, you can check the [full 1.6.11 announcement here](https://www.mail-archive.com/haproxy@formilux.org/msg24440.html) and the [1.5.19 announcement here](https://www.mail-archive.com/haproxy@formilux.org/msg24441.html).

Code and changelogs are available [here for 1.6](/download/1.6/src/) and [here for 1.5](/download/1.5/src/) as usual.

**December 13th, 2016** : _1.7.1_

HAProxy 1.7.1 was released on 2016-12-13.

It fixes a few regressions introduced during 1.7 and some painful bugs pre-dating 1.6 related to behaviour under low memory condition (thus expect 1.6.11 soon).

The most notable 1.7 regressions that were fixed concern the CONNECT method which stopped working in 1.7, two typos on "show stat resolvers" and "show tls-keys" causing the output to be empty, a possible crash with "show stat" on a backend with no LB algorithm (dates back to 1.4 except that it would print "(nil)" by then), and support for LibreSSL was fixed.

There are a few other small things and doc fixes, for more info, it's recommended to [read the announcement here](https://www.mail-archive.com/haproxy@formilux.org/msg24339.html).

Code and changelog are available [here](/download/1.7/src/) as usual.

**November 25th, 2016** : **HAProxy 1.7.0 now released!**

HAProxy 1.7.0 was released on 2016-11-25.

It is considered by some of its contributors as the cleanest release ever produced.

The development cycle for this version was focused on making it more reliable, more modular and more evolutive.

And it pays, because most of the recent new features did not require any core change, resulting in a more reliable core engine and less bugs expected over time.

There are too many improvements to list them here ; for a detailed description of the changes since 1.6, please [consult the announcement here](https://www.mail-archive.com/haproxy@formilux.org/msg24244.html).

Consecutive to this update, the haproxy.org website was also [upgraded to version 1.7.0](http://demo.haproxy.org/) and a new SSL certificate was installed now that [StartSSL](https://www.startssl.com/) accepts up to 10 hostnames per domain on free certs.

Code and changelog are available [here](/download/1.7/src/).

**November 20th, 2016** : _1.6.10_

HAProxy 1.6.10 was released on 2016-11-20.

A few issues were fixed.

The first one is a final fix for the connection layer with the revert of the previous incorrect fix that went into 1.6.8 and 1.6.9, which could cause some unkillable tasks to happen.

Two bugs in the peers' task management were also fixed, putting an end to the few occasional reports of stale CLOSE\_WAIT connections.

Last, the systemd wrapper's signal delivery was fixed to ensure the signals are not lost and the wrapper always knows whether haproxy has finished starting or not.

This ensures reload signals are not lost while the config is being parsed.

The complete announcement is [available here](http://www.mail-archive.com/haproxy@formilux.org/msg24187.html).

Code and changelog are available [here](/download/1.6/src/) as usual.

**November 10th, 2016** : _1.7-dev6_

HAProxy 1.7-dev6 was released on 2016/11/10.

It completes a 13 months development cycle with some nice features that have been awaited for a long time, and managed to fix all the remaining bugs that were reported after the 1.6 release (1.6.10 will be issued soon with the fixes).

The main last features are the support for starting the process with a configuration containing servers which do not resolve and to let them resolve later, the ability for the DNS resolver to finally mark a server as temporarily down on resolution failure (and obviously up again on success), initial support for OpenSSL 1.1.0 (with temporary loss of support for the now obsolete OpenSSL 0.9.8), and the [Stream Processing Offload Engine](http://www.haproxy.org/download/1.7/doc/SPOE.txt) (SPOE for short) letting haproxy delegate some processing to external components for various reasons (CPU usage, high latencies, reliability, event-driven incompatible development model, etc).

We also merged a third device detection engine, WURFL (developed by [Scientiamobile](https://www.scientiamobile.com)).

It's a bit late in the development cycle for such stuff but the code is very well isolated and very clean so there's no reason not to take it.

A few minor performance improvements on large requests or responses were done as well (about 10% faster with 1kB cookie and 100-chars URIs).

It is supposed to be the last version before the final release.

Code cleanups are more than welcome (and needed in some areas).

A few of them area already ongoing.

The complete announcement is [available here](http://www.mail-archive.com/haproxy@formilux.org/msg24095.html).

Code and changelog are available [here](/download/1.7/src/) as usual.

**August, 14th, 2016** : _1.6.8 and 1.7-dev4_

HAProxy 1.6.8 was released on 2016/08/14.

It added 19 new commits after version 1.6.7, and fixes all the annoying issues that were still pending in 1.6.

So this is the first 1.6 version for which we're not aware of any strange problem.

Among the issues fixed, we can cite the occasional segfault hitting a few users of zlib (it was the result of a misunderstanding of the API apparently), a segfault when using sc\_trackers with a different table, a potential memory corruption when using "sni" on the server line, a few crashes in Lua's txn\_done() called by actions and fetchers, a risk to freeze some random file descriptors after an attempt to pass data to a file descriptor being experiencing a connection retry explaining some observed zombie connections, some peers protocol encoding issues explaining some abnormal values and synchro losses, a problem with incorrect sample duplication during processing which could lead certain fetchers to fail to work as a stick table key, and I think that's about all for this time.

Code and changelog are available [here](/download/1.6/src/) as usual.

For 1.7-dev4, we had quite some new stuff.

One change that may affect some users is that we removed the magic consisting in assigning a server's check port to the same port as the first port of the first "bind" directive in the listener if any.

It doesn't make sense at all, is not documented, doesn't work in many situations (eg: unix sockets) and makes it impossible to improve the configuration.

Normally nobody uses this anymore since 1.6 due to the fact that it is not allowed anymore to specify a port on the "listen" line.

Developers may notice that now everything is rebuilt when they modify a ".h" file.

Just do like me, append "DEP=" to your make command line and it will continue to work as before.

Non-developer users are protected against easy mistakes and we are not bothered by a dependency hell.

A number of build fixes for OpenBSD were merged.

In fact it would not build anymore since 1.6 due to various missing includes (or include order).

It's now OK.

I'm surprized that we didn't receive any complaint in one year, in the past people would report OpenBSD breakage.

Maybe these users are now on FreeBSD which seems to work very well.

There were other updates like "set-src-port", "set-dst", "set-dst-port" actions, to force the incoming src/dst address/port to be replaced by the one in argument (useful for logging and also to force a connection to go to a server configured as 0.0.0.0).

Another new action is the "track-sc" for http-response.

This is nice to for counting certain response events.

The "show tls-keys" CLI command can now display the current secrets.

There were some filter changes.

The SNI filters now support multicerts (rsa/ecdsa).

We can also decode the Netscaler's CIP protocol which is an alternative to haproxy's PROXY protocol.

We now have a few new sample fetch functions reporting various TCP-level information on Linux, FreeBSD and NetBSD such as RTT, number of retransmits, etc.

It can make logs more usable during troubleshooting.

And finally the command-line "-f" argument now supports directories in addition to file names.

Files are loaded in alphabetical order.

It is convenient for certain users, but beware of the orderning, use at your own risk!

Code and changelog are available [here](/download/1.7/src/) as usual.

**April, 13th, 2016** : _1.5.17_

I've just released HAProxy 1.5.17 which fixes the CPU usage regression introduced in 1.5.16 after improperly fixing the buffer space calculation code.

It also fixes another bug impacting header captures when there are exactly MAX\_HDR\_HISTORY headers captured (10 by default), in which case the process may crash by dereferencing a pointer at a negative position in the pointers history.

The remaining patches are minor bugs and documentation.

All users of 1.5 should upgrade to 1.5.17, there are too many bugs impacting older versions.

Code and changelog are available [here](/download/1.5/src/) as usual.

**March, 14th, 2016** : _1.7-dev2, 1.6.4, 1.5.16, 1.4.27, 1.3.28 (**EOL**)_

After 3 months for the most recent versions and one year for the oldest ones, a new version was released in each supported branch.

This also marks the last 1.3 release as this branch has now reached end-of-life almost 10 years after it was created.

A number of important bugs were fixed since last releases.

Some of them impact 1.6 when using http-reuse (orphaned connections).

A few Lua bugs were fixed as well, one of them causing a segfault and another one dead connections.

Sample fetch functions were protected against misuse of layer 7 in tcp connection rules causing a segfault.

And session variables could also be improperly used in connection rules with the same effect.

For the less important fixes, some race conditions were addressed in the systemd wrapper possibly causing the orphaned processes some people were experiencing.

In 1.5 there were two issues with idle keep-alive timeout handling on the server side, sometimes causing some short-time busy polling loops and sometimes causing a new incoming request to be aborted on a persistent connection (that browsers had to resend).

In 1.7-dev we've got the filters which introduce a number of hooks to plug some code in a more flexible way than analysers.

The compression code was already adapted to use them.

More to come later, possibly traffic shaping.

The stats have been improved : now everything available in HTML is also available in the CSV output, and there is a new "typed" output format that is more friendly to aggregators.

It is now possible to manipulate environment variables from within the config files, this will solve the problem people are facing when migrating to systemd since it doesn't allow reloaded processes to see changes in environment variables.

As it's been a long time for all versions, users are encouraged to upgrade.

Code and changelogs are available [here](/download/) as usual.

**November, 1st, 2015** : _1.5.15_

With all the recent activity on 1.6, 1.5 was a little bit left behind.

For the last 4 months, a few fixes have accumulated there, including the annoying one striking again on http-send-name-header.

Another one may cause the old process to die during a soft reload when a proxy references a disabled peers section.

The next annoying one affects those who set memory limits to their processes, as the memory size computation was accidently performed on 32-bits which is limited by todays standards (4GB max) so a typical 5 GB allocation would result in 1 GB only due to integer overflow.

The remaining patches are for minor bugs, cleanups and doc updates.

For the vast majority of users there's no emergency to update.

However if you're deploying now, please consider using this version in order to avoid these bugs later.

Code and changelog are available [here](/download/1.5/src/) as usual.

**October, 20th, 2015** : _1.6.1_

HAProxy 1.6.1 has been released with the fixes for the pending bugs introduced in 1.6.0, including the SSL crash when two certs were present on a line, the issue with impossibility to bind frontends when namespaces were enabled but not used, the incorrect use of ANY type DNS queries, and a few doc and build issues.

The small number of bugs (3) in one week is much smaller than what we had in 1.5 (7) in less time, which is encouraging, and matches the quality we were reaching in the last -dev versions.

As usual, code and changelog are available [here](/download/1.6/src/).

**October, 13th, 2015** : **HAProxy 1.6.0 now released!**

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

**September, 28th, 2015** : _1.6-dev6_

HAProxy 1.6-dev6 has just been issued with 35 bugfixes and 22 doc updates.

A few extra features were merged, among which server state conservation across reload, Lua applet registration, RFC5424-compliant log header and structured data extension, cpu-map support on FreeBSD, TCP silent-drop action, and support for any address family in Lua co-socket.

Please check for the details in [the mailing list's announce](http://marc.info/?l=haproxy&m=144347978408109&w=2).

Please test it this week so that we can group last fixes and doc updates next week for a release in less than 2 weeks.

As usual, code and changelog are available [here](/download/1.6/src/devel/).

**August, 30th, 2015** : _1.6-dev4_

HAProxy 1.6-dev4 has just been issued, please check for the details in [the mailing list's announce](http://marc.info/?l=haproxy&m=144096658314447&w=2).

The short version : it's getting better, cleaner and more robust.

Still some work to be done before final 1.6 expected in one month, but we're heading straight in the right direction.

Code and changelog are available [here](/download/1.6/src/devel/) as usual.

Please test it if you haven't yet tested 1.6, especially if you feel like you're using some advanced features or a complex setup, and report issues or successes on the mailing list.

**July, 3rd, 2015** : _1.5.14_ : fixes an information leak vulnerability (CVE-2015-3281)

A vulnerability was found when HTTP pipelining is used.

In some cases, a client might be able to cause a buffer alignment issue and retrieve uninitialized memory contents that exhibit data from a past request or session.

I want to address sincere congratulations to Charlie Smurthwaite of aTech Media for the really detailed traces he provided which made it possible to find the cause of this bug.

Every user of 1.5-dev, 1.5.x or 1.6-dev must upgrade to 1.5.14 or latest 1.6-dev snapshot to fix this issue, or use the backport of the fix provided by their operating system vendors.

CVE-2015-3281 was assigned to this bug.

Code and changelog are available [here](/download/1.5/src/) as usual.

**June, 26th, 2015** : _1.5.13_

There's nothing really critical this time.

The most important part is the replacement of the dh-param groups provided by default in order to avoid the issues brought with logjam.

Some bugs were found in the tcp-checks rules processing and were fixed.

If you use tcp-checks, you'd be safe with this update.

Another one is an issue that was reported in 1.5.12 with peers trying to immediately reconnect upon error and eating a lot of CPU.

An old issue was reported regarding TIME\_WAIT sockets on the server side caused by POST requests terminated with abort-on-close.

Now we apply NOLINGER to avoid this.

And there's this backport I announced but forgot about peers now being usable with nbproc > 1 provided that each section is referenced by tables from only one process.

Code and changelog are available [here](/download/1.5/src/) as usual.

**June, 17th, 2015** : _1.6-dev2_

This version marks the feature freeze for 1.6.

The number of changes is as huge as for dev1, in part due to many last-minute features being rushed into it.

Among the changes since dev1, we can enumerate DNS-based server name resolution, server address change from the CLI, peers protocol updated to v2 to replicate everything in stick-tables, improved support for peers and multi-process, removal of some deprecated keywords, pattern matching cache for faster regex match, stateless ZIP compression using [libslz](http://1wt.eu/projects/libslz/), support for variables to ease data manipulation, declared captures to allow captures on responses and in backends, SSL cert forgery on the fly, device identification with [DeviceAtlas](https://deviceatlas.com/deviceatlas-haproxy-module) and [51Degrees](https://github.com/51Degreesmobi/51Degrees-C), updated default DH params for improved protection against the [logjam attack](https://weakdh.org/), support of quotes and environment variables everywhere in the configuration language, automatic quoting in the stats CSV output, redirect on HTTP responses, stricter detection of duplicated backend or server names, support for multiple redispatches on failed retries, request body processing, TLS ticket keys loading from file and update from CLI, "option http-ignore-probes" to silently ignore 400/408 caused by browser preconnect, disabling of HTTP/0.9 by default, stricter memory allocator for Lua, and many internal changes.

The more detailed changelog can be read [here in the announce](http://marc.info/?l=haproxy&m=143455374508423&w=2).

Server state conservation across reloads is still being reviewed and will hopefully be merged before dev3.

Code and changelog are available [here](/download/1.6/src/devel/) as usual.

**May, 15th, 2015** : _HTTP/2 is out!_

Today, HTTP/2 officially exists as [RFC7540](https://www.rfc-editor.org/info/rfc7540) and [RFC7541](https://www.rfc-editor.org/info/rfc7541).

The first one describes the protocol itself while the second one is specific to the header compression mechanism called HPACK.

HTTP/2 is a major change to HTTP/1 as it introduces multiplexed concurrent streams over a single connection.

HAProxy has experienced a major internal architecture redesign during the 1.6 development cycle to address these new requirements.

Version 1.6 will not support HTTP/2 yet since the feature freeze is expected at the end of this month, however the architecture should be mostly ready for the future developments to start for real.

We expect to support it by the end of the year, during the 1.7 development cycle.

It was great to participate to this specification during these 3+ years, I'm already impatient to work on HTTP/3 :-)

**May, 2nd, 2015** : _1.5.12_

A number of annoying bugs were fixed during the last 3 months, it was time for an update.

Two of them may result in a crash with very specific configurations.

A number of fixes to comply with RFC7230 were made.

Till now we used to comply with 2616 but it was not strict enough and could cause interoperability issues in some corner cases.

A new feature was backported : "option http-ignore-probes".

It disables logging, responses 400/408 and error counters for empty connections that could result from pre-connect from some clients.

People are seeing up to 25% of them in their stats or logs, so it made sense to backport this from 1.6.

Another improvement consists in a relax of the restriction between peers and nbproc.

Now it is possible to use peers provided that the whole section is only used by tables belonging to the same process.

This makes it easier to run SSL offloading in multiple processes now.

Code and changelog are available [here](/download/1.5/src/) as usual.

**April, 1st, 2015** : _April Fool's: Complete rewrite of HAProxy in Lua_

As some might have noticed, HAProxy development is progressively slowing down over time.

I have analyzed the situation and came to the following conclusions :

*   the code base is increasing and is becoming slower to build day after day. Ten years ago, version 1.1.31 was only 6716 lines everything included. Today, mainline is 108395 lines, or 16 times larger.
*   gcc is getting slower over time. Since version 2.7.2 I used to rely on ten years ago, we've seen important slowdowns with v2.95, several v3.x then v4.x. I'm currently on 4.7 and afraid to upgrade.
*   while the whole code base used to build in less than a second ten years ago on an Athlon XP-1800, now it takes about 10 seconds on a core i5 at 3 GHz. Multiply this by about 200 builds a day and you see that half an hour is wasted every single day dedicated to development. That's about 1/4 of the available time if you count the small amount of time available after processing e-mails.
*   people don't learn C anymore at school and this makes it harder to get new contributors. In fact, most of those who are proficient in C already have a job and little spare time to dedicate to an opensource project.

In parallel, I'm seeing I'm getting old, I turned 40 last year and it's obvious that I'm not as much capable of optimizing code as I used to be.

I'm of the old school, still counting the CPU cycles it takes a function to execute, the nanoseconds required to append an X-Forwarded-For header or to parse a cookie.

And all of this is totally wasted when people run the software in virtual machines which only allocate portions of CPUs (ie they switch between multiple VMs at high rate), or install it in front of applications which saturate at 100 requests a second.

Recently with the Lua addition, we found it to be quite fast.

Maybe not as fast as C, but Lua is improving and C skills are diminishing, so I guess that in a few years the code written in Lua will be much faster than the code we'll be able to write in C.

Thus I found it wise to declare a complete rewrite of HAProxy in Lua.

It comes with many benefits.

First, Lua is easy to learn, we'll get many more developers and contributors.

One of the reason is that you don't need to care about resource allocation anymore.

What's the benefit of doing an strdup() to keep a copy of a string when you can simply do "a = b" without having to care about the memory used behind.

Machines are huge nowadays, much larger than the old Athlon XP I was using 10 years ago.

Second, Lua doesn't require a compiler, so we'll save 30 minutes a day per 200 builds, this will definitely speed up development for each developer.

And we won't depend on a given C compiler, won't be subject to its bugs, and more importantly we'll be able to get rid of the few lines of assembly that we currently have in some performance-critical parts.

Third, last version of HAProxy saw a lot of new sample fetch functions and converters.

This will not be needed anymore, because the code and the configuration will be mixed together, just as everyone does with Shell scripts.

This means that any config will just look like an include directive for the haproxy code, followed by some code to declare the configuration.

It will then be possible to create infinite combinations of new functions, and the configuration will have access to anything internal to HAProxy.

In the end, of the current HAProxy will only remain the Lua engine, and probably by then we'll find even better ones so that haproxy will be distributed as a Lua library to use anywhere, maybe even on IoT devices if that makes sense (anyone ever dreamed of having haproxy in their watches ?).

This step forward will save us from having to continue to do any code versionning, because everyone will have his own fork and the code will grow much faster this way.

That also means that Git will become useless for us.

In terms of security, it will be much better as it will not be possible to exploit a vulnerability common to all versions anymore since each version will be different.

HAProxy Technologies is going to assign a lot of resources to this task.

Obviously all the development team will work on this full time, but we also realize that since customers will not be interested in the C version anymore after this public announce, we'll train the sales people to write Lua as well in order to speed up development.

We'll continue to provide an enterprise version forked from HAPEE that we'll rename "Luapee".

It will still provide all the extras that make it a professional solution such as VRRP, SNMP etc and over the long term we expect to rewrite all of these components in Lua as well.

The ALOHA appliances will change a little bit, they'll mostly be a Lua engine to run all that code, so we'll probably rename them HALUA.

And given that the appliance's goal has always been to take profit of the hardware and kernel to further improve the capabilities, we'll have free hands to port other performance-critical parts in Lua, including maybe the currently aging Linux kernel which also happens to be written in C.

Once everything is ported, I intend to use my old skills in the domain of microarchitecture to design a native Lua processor that will run in our appliances so that all the code runs in silicon and ends up being much faster than what we currently have in C.

I'm quite aware that some parts will be tedious.

Rewriting OpenSSL in Lua will neither be easy nor fun.

But it's the price to pay to get fast and affordable security.

Due to the huge amount of work, we'll postpone the 1.6 release to 1st April 2016, which leaves us exactly 366 days to complete this task.

I hope everyone understands that we have no other choice.

**February, 1st, 2015** : _1.5.11, 1.4.26, 1.3.27, 1.3.15.14_

There was nothing really important for 1.5, mostly small annoyances caused by improper behaviours.

One of them was not exactly a bug since it used to work as documented, but as it was documented to work in a stupid and useless way I decided to backport it anyway.

It's the "http-request set-header" action which used to remove the target header prior to computing the format string, making it impossible to append a value to an existing header, or to have to pass via a dummy header, adding to the complexity.

Now the string is computed before removing the header so that there's no more insane tricks to go through.

One important fix targets users running on 1.5.10 : the addition of "log-tag" uncovered a bug by which we can run with a null logger if no logger is declared.

Since 1.5.10 (with log-tag), this could cause a crash upon startup, so this was fixed here.

On the 1.4 front, things had been stuck for several months due to the problems caused by "http-send-name-header" that managed to keep both Cyril and me busy for a while.

No less than 3 bugs in direct relation with this feature were fixed, two of them capable of crashing the process under certain conditions.

Another important bug in 1.4 was triggered when issuing "show sess" on the CLI.

Other fixes are not really important and were accumulated over 10 months.

Having 1.4 ready was a great opportunity to issue another 1.3, so 1.3.27 backports the relevant fixes from 1.4.

Considering that the last 1.3 was issued 3.5 years ago, I suspect that 1.3.27 will be the last 1.3 though it's still maintained 8 years the first 1.3 was issued.

1.3.15.14 was released with pending fixes as well and now **the 1.3.15 branch is closed and switches to the unmaintained state** after 7 years of fixes.

Note: when pushing 1.3.27, I was unfortunate to discover that git.haproxy.org and the public master Git repository went out of sync, both forking after 1.3.26, so **I had to perform a forced push** on git.haproxy.org to resync them.

Sorry for the inconvenience.

**January, 1st, 2015** : _Year of a changing Web_

I'm always surprized to see how very few people outside of the [IETF HTTP working group](https://tools.ietf.org/wg/httpbis/) are just aware of the fact that HTTP/2 is being worked on.

At the time of writing, the draft is in the "Last Call" state which basically means that unless something critical is discovered, it will soon be adopted in its [current form](https://datatracker.ietf.org/doc/draft-ietf-httpbis-http2/).

Here _"soon"_ means _"around a few weeks"_.

What will this change ?

Probably not much at the beginning, but a lot soon.

It will take some time before web site operators figure the performance benefits brought by HTTP/2, but the media will quickly boast its merits and the change can happen quickly, even if just to catch up with competiting early adopters.

A number of sites already support SPDY for the same reasons right now but SPDY is constantly evolving and requires more attention from users who have to update often.

By being a new standard, HTTP/2 will not require that level of care, and it will be perceived as the direct descendant of HTTP/1.1, which is why it will be more adopted than SPDY.

All major browsers already support HTTP/2, two of them (Firefox and Chrome) [will only support it for HTTPS](https://www.mnot.net/blog/2014/01/30/http2_expectations).

Internet Explorer [will drop SPDY support](http://blogs.msdn.com/b/ie/archive/2014/10/08/http-2-the-long-awaited-sequel.aspx) once HTTP/2 is adopted.

That logically means that a number of web sites will decide to enable HTTPS in order to support HTTP/2 for the users of the two aforementionned browsers.

HTTPS comes with an extra round trip at the beginning of the connection, but HTTP/2 saves a lot of them during the transfers so in the end if there are at least a few tens of objects to retrieve, it will still be an improvement.

But this will cause a new issue : migrating to HTTPS will mean that the caches that are operated in universities, enterprises, all mobile phone operators and many ISPs will not be used anymore.

This will immediately have two impacts : the first one is that the traffic on the internet will increase.

Alarmists [used to say](http://www.pcworld.idg.com.au/article/308437/trans-atlantic_internet_cables_may_filled_by_2014/) that the [40 Tbps trans-atlantic total capacity](http://www.itu.int/ITU-D/ict/newslog/TransAtlantic+Bandwidth+The+Hangover+Lingers.aspx) is almost saturated and hard to upgrade, we'll see if that's true.

The second effect is that origin servers will get a significant traffic increase, which is good for ADC vendors as well as for CDNs which will get many new customers and increase their revenue.

Sadly, in a number of poorly connected countries where client-side caches are critical to the survival of the Internet, CDNs will not be able to help and the situation will get even worse.

That's also the case for a number of mobile phone operators who can observe high cache hit ratios today.

What will very likely happen to address these situations is that ISPs and mobile phone operators will start to propose a faster Internet access to their customers in exchange for a root cert that they can happily install in their browser so that [the operator can decipher SSL traffic](https://gigaom.com/2013/01/10/nokia-yes-we-decrypt-your-https-data-but-dont-worry-about-it/) on the fly and cache again.

End users are already prepared to accept this because they don't care at all about their privacy when it comes to whatever they do with their smartphone, otherwise they would always close their apps and type a password to access their emails.

And the next logical step is that mobile phones sold by these operators will already have the root cert pre-installed in order to save a complex operation from the end user.

And that will lead to an interesting situation.

First, SSL offloading solution vendors will happily see their sales increase.

But the counter part is that the chain of trust of the SSL/TLS model will be definitely broken in that there will be no way for the end user to know [if his data were safe](http://lists.w3.org/Archives/Public/ietf-http-wg/2014OctDec/0643.html) or not.

This chain is extremely fragile already and is [regularly being abused](http://www.computerworld.com/article/2486614/security0/french-intermediate-certificate-authority-issues-rogue-certs-for-google-domains.html), but now it could become the norm not to trust SSL anymore when rogue CAs becomes mandatory to access the net.

Fortunately, a [few](http://tools.ietf.org/html/draft-rpeon-httpbis-exproxy) [solutions](https://tools.ietf.org/html/draft-loreto-httpbis-trusted-proxy20) [are](http://lists.w3.org/Archives/Public/ietf-http-wg/2013OctDec/1489.html) being worked on.

On the HTTP working group they're called _"Trusted Proxies"_ or "GET https://", as a reference to what an HTTPS request through an explicit proxy could look like.

They consist in letting the end user choose what can be deciphered and what cannot.

That allows proxy operators to let some trusted sites pass through and to decipher/inspect/cache contents for all other ones.

That's how we could get a better Internet for everyone, with better caching and better privacy at the same time.

Not sure it will happen by 2015 though, but we should do whatever we can for this to happen!

**December, 31th, 2014** : _1.5.10 : Last release of the year!_

Most of the fixes in this version are related to how we deal with out-of-memory situations.

This normally interests nobody except those who run many instances on memory-bound servers.

There was a very unlikely but possible case of crash when it was not possible to allocate a small chunk of memory (I managed to reproduce it after a long time during extremely aggressive tests).

There are a few fixes on tcp-checks, one for a bug causing some random contents to be analysed, another one where quick acks were disabled when there was no data to send, causing 200ms delays when "option tcp-check" was specified alone.

Another bug concerned proxies disabled in the configuration which could under some circumstances cause a segfault upon startup during the process mask propagation between frontends and backends.

The rest is mostly harmless, so keep cool, no rush if you're already running 1.5.9.

Code and changelog are available [here](/download/1.5/src/) as usual.

**November, 25th, 2014** : _1.5.9_

That's a release as I like them, with 6 different contributors providing direct fixes and a few other bringing detailed bug reports.

In short, some issues with out-of-memory conditions were fixed both in the SSL part and in the session management.

Now it should not be possible to crash haproxy even when running with artificially low memory limitations.

Cyril fixed a problem with the agent check accidently inheriting the SSL mode of regular checks.

Denys Fedoryshchenko found that TCP captures could cause random crashes when not using HTTP mode due to the capture pointers not yet being initialized.

Krisztian Kovacs fixed a Proxy Protocol parsing bug.

Thierry Fournier fixed a bug that appears when loading many time the same ACL from a file, causing it to grow and slow down for some linear matches (eg: regex).

A few minor fetches were backported as they make it easier to take action based on the process ID or the stopping status.

The rest are minor bug fixes and improvements.

Users must definitely upgrade, especially if using TCP captures or running under constrained memory conditions.

Code and changelog are available [here](/download/1.5/src/) as usual.

**October, 31th, 2014** : _1.5.8_

Dmitry Sivachenko reported that an occurrence of "-ldl" accidently slipped into the makefile in 1.5.7, complicating builds on systems like FreeBSD with no libdl.

Godbach fixed a bug which appears only when users force tune.maxrewrite to 0 (which is impractical in production), and which causes buffer insertions to write at the wrong location and to crash the process.

There's no security impact here given that such configurations cannot be used in production.

I preferred to issue a new version so that everyone can upgrade without trouble.

If you already run with 1.5.7, then you don't need to upgrade to 1.5.8.

Code and changelog are available [here](/download/1.5/src/) as usual.

**October, 30th, 2014** : _1.5.7_

A nasty bug reported by Dmitry Sivachenko can cause haproxy to die in some rare cases when a monitoring system issues a lot of "show sess" commands on the CLI and aborts them in the middle of a transfer.

The probability to hit it is so low that it has existed since v1.4 and was only noticed now.

Cyril Bonté fixed a bug causing wrong flags to be sometimes reported in the logs for keep-alive requests.

A bug where the PROXY protocol is used with a banner protocol causes an extra 200ms delay for the request to leave, slowing down connection establishment to SMTP or FTP servers.

Christian Ruppert found and fixed a bug in the way regex are compiled when HAProxy is built with support for PCRE\_JIT but the libpcre is built without.

The way original connection addresses are detected on a system where connections are NAT'd by Netfilter was fixed so that we wouldn't report IPv4 destination addresses for v6-mapped v4 addresses.

This used to cause the PROXY protocol to emit "UNKNOWN" as the address families differred for the source and destination!

John Leach reported an interesting bug in the way SSL certificates were loaded : if a certificate with an invalid subject (no parsable CN) is loaded as the first in the list, its context will not be updated with the bind line arguments, resulting in such a certificate to accept SSLv3 despite the "no-sslv3" keyword.

That was diagnosed and fixed by Emeric, who also implemented the global "ssl-default-bind-options" and "ssl-default-server-options" keywords, and implemented "ssl\_c\_der" and "ssl\_f\_der" to pass the full raw certificate to the server if needed.

That's all for this version.

Nothing critical again, but we're just trying to keep a fast pace to eliminate each and every bug.

Code and changelog are available [here](/download/1.5/src/) as usual.

**October, 18th, 2014** : _1.5.6_

Very few fixes this time, 1.5.6 fixes the annoying bug reported this week about disabled proxies, an issue in the URI hash (the question mark of a query string was accidently hashed when present), an off-by-one when checking the stick-counter number in "track-sc" rules, resulting in the "track-sc3" action being accepted and reported as valid but ignored, and slightly improves the systemd wrapper.

Code and changelog are available [here](/download/1.5/src/).

**October, 8th, 2014** : _1.5.5_

This time, nothing really important, just a few issues in the config parser (eg: stop trying to propagate process binding to dynamic backends, stop sending warnings for stats attached to multi-process frontends if it relies on single-process bind lines), a fix for an annoying issue causing the HTTP mode (close/keep-alive) to be ignored in backends, a fix for TCP checks not properly detecting connection failures is there was no tcp-check rule, and better support for supervisord in systemd-wrapper.

Since there was no rush here, it can be the good timing to upgrade to a reasonably stable version after testing it calmly :-) As usual code and changelog are available [here](/download/1.5/src/).

**September, 2nd, 2014** : _1.5.4_

A **critical bug** was fixed in 1.5.4.

This bug was introduced in 1.5-dev23, so all users of any version between 1.5-dev23 and 1.5.3 must upgrade.

This bug can cause haproxy to crash if a number of conditions are met together.

Basically, we need a client which can upload multiples of 2GB of POST data much faster than the server can read, and the server must accept all these data slowly enough.

If all of this happens, it is possible during the roll-over at every 2GB that the chunk parser tries to parse a chunk length out of the input buffer, causing haproxy to crash.

In practice, it can essentially be exploited when the attacker controls both the client, the server, and the timing.

This cannot be used to modify data nor execute code though, it's only a denial of service.

**CVE-2014-6269** was assigned to this bug.

Another bug was a possible busy loop in tcp-request content track-sc rules.

Other bugs are less important and can be found in the changelog available with the code [here](/download/1.5/src/).

**July 25th, 2014** : _1.5.3_

Version 1.5.3 fixes a few issues on top of 1.5.2.

Essentialy, a possible memory leak un SSL DHE exchanges, and a possible memory corruption when building the proxy protocol v2 header.

For sure few people will feel impacted, but better release a new version while everything else is calm.

The source code and changelog are available [here](/download/1.5/src/).

**July 12th, 2014** : _1.5.2_

Two extra important issues were discovered since 1.5.1 which were fixed in 1.5.2.

The first one can cause some sample fetch combinations to fail together in a same expression, and one artificial case (but totally useless) may even crash the process.

The second one is an incomplete fix in 1.5-dev23 for the request body forwarding.

Hash-based balancing algorithms and http-send-name-header may fail if a request contains a body which starts to be forwarded before the contents are used.

A few other bugs were fixed, and the max syslog line length is now configurable per logger.

As usual, the source code and changelog are available [here](/download/1.5/src/).

**June 24th, 2014** : _1.5.1_

Version 1.5.1 fixes a few bugs from 1.5.0 among which a really annoying one which can cause some file descriptor leak when dealing with clients which disappear from the net, resulting in the impossibility to accept new connections after some time.

This bug was introduced in 1.5-dev25, so affected users are strongly encouraged to upgrade.

For more information, please consult the source code and changelog [here](/download/1.5/src/).

Also today I was pleased to receive a bottle of Champagne sent by our friends at Loadbalancer.org!

Thank you guys!

[![](/img/bottle-lb_s.jpg)](/img/bottle-lb.jpg)

**June 19th, 2014** : **HAProxy 1.5.0 released!**

After 4 years of hard work, **HAProxy 1.5.0 is finally released!**

For people who don't follow the development versions, 1.5 expands 1.4 with many new features and performance improvements, including **native SSL** support on both sides with SNI/NPN/ALPN and OCSP stapling, **IPv6** and UNIX sockets are supported everywhere, **full HTTP keep-alive** for better support of NTLM and improved efficiency in static farms, **HTTP/1.1 compression** (deflate, gzip) to save bandwidth, **PROXY protocol** versions 1 and 2 on both sides, **data sampling** on everything in request or response, including payload, **ACLs** can use any matching method with any input sample **maps** and dynamic ACLs **updatable** from the CLI **stick-tables** support counters to track activity on any input sample **custom format** for logs, unique-id, header rewriting, and redirects, **improved health** checks (SSL, scripted TCP, check agent, ...), **much more scalable** configuration supports hundreds of thousands of backends and certificates without sweating.

Since dev26, a few bugs were fixed, and some low-importance things were integrated.

Basic OCSP stapling support from Dirkjan and Emeric was finally merged.

Sasha's header replace actions were merged as well.

I've added a few more info in the stats page (avg response times) and CSV output (health check status), added support for PROXY v2 on the accept side, and added the "capture" action on tcp-request in order to log contents such as SNI or payload.

Rémi's dh-param was finally integrated.

People love numbers, so here are a few.

From 1.4.0 to 1.5.0, we had :

*   **1574** calendar days (4 yr 3 mon)
*   **26** development versions (one every 2 months on average)
*   **540** bugs fixed (**387** added during 1.5, **153** affecting 1.4 as well)
*   **2549** commits
*   **683** unique commit dates (at least this many days worked)
*   up to **24** commits per day
*   **69712** lines removed, **122279** lines added
*   many extremely useful bug reports (too many to list)
*   **73** code/doc contributors : Adrian Bridgett, Alex Davies, Aman Gupta, Andreas Kohn, Apollon Oikonomopoulos, Arnaud Cornet, Baptiste Assmann, Bertrand Jacquin, Bhaskar Maddala, Conrad Hoffmann, Cyril Bonté, Daniel Schultze, David BERARD, David Cournapeau, Dave McCowan, David du Colombier, Delta Yeh, Dirkjan Bussink, Dmitry Sivachenko, Emeric Brun, Emmanuel Hocdet, Evan Broder, Finn Arne Gangstad, Gabor Lekeny, Geoff Bucar, Wei Zhao, Guillaume Castagnino, Guillaume de Lafond, Hervé COMMOWICK, Hiroaki Nakamura, James Voth, Jamie Gloudon, Jarno Huuskonen, Joe Williams, Joshua M. Clulow, Julien Vehent, Justin Karneges, Kevin Hester, Kevin Musker, Kristoffer Grönlund, Krzysztof Piotr Oledzki, Lukas Tribus, Marc-Antoine Perennou, Mark Lamourine, Mathieu Trudel, Michael Scherer, Neil Prockter, Nenad Merdanovic, Nick Chalk, Olivier Burgard, Oskar Stolc, Patrick Mézard, Pieter Baauw, Prach Pongpanich, Rauf Kuliyev, Remi Gacogne, Sagi Bashari, Sasha Pachev, Sean Carey, Sergiy Prykhodko, Simon Horman, Simone Gotti, Stathis Voukelatos, Tait Clarridge, Thierry Fournier, Todd Lyons, Vincent Bernat, William Lallemand, William Turner, Willy Tarreau, Yuxans Yao, Yves Lafon.

Additionally, we are very thankful to a few organisations who have **sponsored** the development of certain advanced features which required to dedicate a person or a team for a significant amount of time (I hope I have not missed any) :

*   [HAProxy Technologies](https://www.haproxy.com/) _(formerly Exceliance)_
*   [Loadbalancer.org](http://loadbalancer.org/)
*   [StackOverflow](http://stackoverflow.com/)
*   [SmartFile](https://www.smartfile.com/)
*   [SmugMug](http://www.smugmug.com/)
*   [ImageShack](https://imageshack.com/)

Don't forget to offer a beer to your **distro packagers** who make your life easier.

It's hard to list them all, but if you don't build from sources, you're likely running a package made and maintained by one of these people :

*   debian: Vincent Bernat, Apollon Oikonomopoulos, Prach Pongpanich
*   Fedora: Ryan O'hara
*   OpenSuSE: Marcus Rückert
*   Other?: contact me to mention you

And last, I'd like to assign a special mention to our **most active mailing list supporters** during that period who make the project a reality by off- loading the support task from developers and kindly help our 800 permanent subscribers on a daily basis, **BIG THANKS** to you guys :

*   Baptiste Assmann
*   Lukas Tribus
*   Cyril Bonté
*   Jonathan Matthews
*   Thomas Heil

For the HAProxy development team here in France, it will be time to do some errands and buy some Champagne to celebrate the event :-)

**June 7th, 2014** : _HTTP/1.1 reloaded_

Six years ago, Daniel Stenberg [notified](http://curl.haxx.se/mail/lib-2008-07/0245.html) on the libcurl mailing list that [Mark Nottingham](https://www.mnot.net/blog/), chair of the [IETF HTTP Working Group](http://trac.tools.ietf.org/wg/httpbis/trac/wiki), initiated a review of existing HTTP implementations.

Since HAProxy was mentionned in this list, Aleks Lazic [relayed this mail](http://www.formilux.org/archives/haproxy/0808/1253.html) to the haproxy mailing list and I attempted to fill in the form with the information I could provide on HAProxy.

By then HAProxy 1.3.15 had just been released without keep-alive nor HTTP/1.1 support.

Being confronted to a lot of interoperability issues between clients and servers through HAProxy, I felt that it was a great opportunity to join the Working Group to try to improve the situation from my angle of view.

I was impressed to see that participants work professionally and calmly.

Noone really tries to defend his own implementation, what matters is interoperability, even if that sometimes needs changes in their code.

Of course, the concerns are different for various types of components (eg: security, performance, complexity, etc), often resulting in long debates.

And like many other products, HAProxy experienced quite a number of code changes consecutive to clarifications made to the spec.

The latest example of this [happened](http://lists.w3.org/Archives/Public/ietf-http-wg/2014AprJun/1050.html) after Google Chrome users were seeing HAProxy's 408 error page on a number of web sites.

And 7 years after this positive work started (OK, 6 years for me, I started late), the group's efforts have [finally resulted in 11 new RFCs](http://lists.w3.org/Archives/Public/ietf-http-wg/2014AprJun/1169.html)!

The 6 first (RFC 7230 to 7235) replace the aging RFC2616 :

1.  [RFC7230](http://tools.ietf.org/html/rfc7230) : Message Syntax and Routing
2.  [RFC7231](http://tools.ietf.org/html/rfc7231) : Semantics and Content
3.  [RFC7232](http://tools.ietf.org/html/rfc7232) : Conditional Requests
4.  [RFC7233](http://tools.ietf.org/html/rfc7233) : Range Requests
5.  [RFC7234](http://tools.ietf.org/html/rfc7234) : Caching
6.  [RFC7235](http://tools.ietf.org/html/rfc7235) : Authentication

The next ones are about authentication scheme and method registrations (7236 and 7237), and extensions whose discussion was initiated in the working group but which were not carried by the working group (status code 308, "Forwarded" and "Prefer" header).

If you're implementing an HTTP agent (client, server, proxy, gateway, or whatever), please read them.

They cover a lot of corner cases that are encountered in field and which are the result of the fact that the protocol evolved faster in field than in the docs.

The first two ones are already a very good start to demystify the protocol and get rid of your wrong beliefs.

What next ?

HTTP/2.0 is on the rails and has been for about 2 years now.

It's time to focus on it!

**May 28th, 2014** : _1.5-dev26 : hopefully last!_

This version tries to be the last one in the development cycle.

There were very few changes.

The agent-check was completed.

A potential CPU busy loop when reloading with the systemd wrapper was fixed.

A possible buffer overflow with regex in inlikely configs was fixed.

The "str" match is now used by default for string samples.

No major new feature is considered missing for the final release, so only fixes and minor updates may be merged now.

Source code and changelog are available as usual [here](/download/1.5/src/).

**May 10th, 2014** : _1.5-dev25_

Four important issues were fixed since dev24.

One could cause crashes on out-of-memory.

Another one concerns FreeBSD where the shared session cache could have been used without locking, causing random crashes as well.

The recent fixes for HTTP request body forwarding randomly caused pauses when using balance url\_param.

Last, arguments "-i" and "-n" were ignored on ACLs since dev23.

Some pending changes were completed as well.

Half-closed timeouts are now supported.

Unix sockets are supported on the server side, as well as abstract namespace sockets on Linux.

This allows backends and frontend to connect together without consuming TCP ports.

The old unmaintained BSD and OSX Makefiles were removed.

Per-listener process binding is finally possible using the "process" keyword on "bind" lines, which makes it possible to have one stats socket per process.

Version 2 of the PROXY protocol was implemented on the server side.

A few other minor improvements were made.

Source code and changelog are available [here](/download/1.5/src/).

**Apr 26th, 2014** : _1.5-dev24_

This version fixes 3 major regressions from dev23, one causing transfers to be interrupted after the configured timeout, another one where redirects could sometimes cause a crash, and one slowing down SSL.

Other minor issues were fixed.

The stats page now supports chunked mode, keep-alive and compression, and may be declared in any section with no warning.

Health checks can be started within a smaller delay. http-request/response now support set-map/del-map/add-acl/del-acl to add/remove pattern entries to maps and ACLs on the fly based on data extracted from the traffic.

Heartbleed attacks (CVE-2014-0160) are detected and blocked even on vulnerable OpenSSL implementations.

Source code and changelog are available [here](/download/1.5/src/).

**Apr 23th, 2014** : _1.5-dev23 : Broken_

This new version addresses half of the remaining changes before -final : use\_backend supports _log-format_ expressions.

Maps and ACLs now share the same pattern lists which are dynamically updatable from the CLI.

SSL web sites now load faster thanks to dynamic record size adjustments.

Compression of chunked HTTP responses was fixed and enabled again.

About 35 bugs were fixed.

We're getting close to 1.5-final.

Source code and changelog are available [here](/download/1.5/src/).

**Feb 3rd, 2014** : _1.5-dev22_

The whole polling system was finally reworked to replace the speculative I/O model designed 7 years ago with a fresh new event cache.

This was needed because the OpenSSL API is not totally compatible with a polled I/O model since it stores data into its internal buffers.

One of the benefits is that despite the complexity of the operation, the code is now less tricky and much safer.

HTTP keep-alive is now enabled by default when no other option is mentionned, as it is what users expect by default when they don't specify anything and end up with tunnel mode.

A new option "tunnel" was thus added for users who would find a benefit in using tunnel mode.

After an HTTP 401 or 407 response, we automatically stick to the same server so there's normally no need for "option prefer-last-server" anymore.

SSL buffer size are automatically adjusted to save round trips as suggested by Ilya Grigorik, reducing the handshake time by up to 3.

The CLI reports more info in "show info" and now supports "show pools" to check memory usage.

SSL supports "maxsslrate" to protect the SSL stack against connection rushes.

The "tcp-check" directive now supports a "connect" action, enabling multi-port checking.

Very few changes are pending before 1.5-final : ACL/map merge (being reviewed), HTTP body analyzer fixes (in progress), agent check update (started), per-listener process binding (experimentations completed).

Source code is available [here](/download/1.5/src/).

**Dec 17th, 2013** : _1.5-dev21_

Several early testers reported a few annoying bugs yesterday, so I preferred to fix them quickly and issue another release than wasting everyone's time on these bugs.

Use this version instead of 1.5-dev20 to be safe.

Please refer to the [changelog](/download/1.5/src/CHANGELOG) for more information.

Source code is available [here](/download/1.5/src/).

**Dec 16th, 2013** : _1.5-dev20 : keep-alive, finally!_

This version took 6 months to be released given the difficulty of some changes, and it collected a number of new features.

The most awaited of them is **server-side keep-alive**.

The first commit for this feature was initially attempted almost 4 years ago.

There are still some limitations, idle server connections are not accounted for maxconn and not reported in the stats for example.

And option http-keep-alive still needs to be specified to benefit from the feature.

The memory usage has significantly dropped, 640 bytes saved per idle connection on 64-bit systems.

All sample fetch expressions (including ACLs) now support a list of converters applied to the sample.

The new **map** feature allows input samples to be converted to other ones.

The most common usage of this is geolocation, but it may also be used for massive redirect tables.

Maps are updatable live from the CLI.

Redirects support the log-format syntax and can embed some elements collected from the request.

Hash algorithms can now be selected per backend.

Health checks have been improved with the **agent-check** and **tcp-check** to build send/expect rules.

Please refer to the [changelog](/download/1.5/src/CHANGELOG) for more information.

Source code is available [here](/download/1.5/src/).

**Jun 17th, 2013** : _1.4.24 and 1.5-dev19 : security fix_

A new vulnerability was discovered in all versions from 1.4.4 and above.

It was fixed today with 1.4.24 and 1.5-dev19 ([CVE-2013-2175](http://seclists.org/oss-sec/2013/q2/581)).

This vulnerability can induce a crash when configs involving tail-relative header offset such as hdr\_ip(xff,-1) are used.

Please see the advisory for more details.

All 1.4 and 1.5 users must upgrade.

Additionally, a few other important bugs were fixed.

One of them was a regression introduced in 1.5-dev12, which could randomly crash haproxy on rare circumstances when using pipelined requests with a slow client.

Last, some endless loops were possible since 1.4 when using consistent hashing algorithms with flapping servers.

On the positive side, many small new features were finally merged, such as http-response rule sets, ability to change task priority, DSCP field, Netfilter mark and log-level based on L7 ACLs, ability to selectively accept the PROXY protocol header using ACLs, support for environment variables in ACLs and fetches, addition of a 3rd stick-counter, filtering on the stats page, transparent proxy for FreeBSD/OpenBSD, and a few other things.

Last but not least, the doc on ACLs/fetches got a major lift-up to deduplicate keywords.

A few important issues still need to be addressed, and server-side keep-alive is expected as well before final 1.5 can be released, hopefull by the end of this summer.

Please refer to the [1.4 changelog](/download/1.4/src/CHANGELOG) and [1.5 changelog](/download/1.5/src/CHANGELOG) for more information.

Source code is available [here for 1.4](/download/1.4/src/) and [here for 1.5](/download/1.5/src/).

**Apr 3rd, 2013** : _1.4.23 and 1.5-dev18 : security fix_

A vulnerability in all 1.4 and 1.5 releases was fixed in 1.4.23 and 1.5-dev18 ([CVE-2013-1912](http://seclists.org/oss-sec/2013/q2/3)), affecting HTTP fetches in TCP request inspection rules.

All 1.4 and 1.5 users must upgrade.

In addition to this, 1.5-dev18 brings a significant number of improvements, among which use of environment variables in all addresses (bind, log, source, server, ...), agent-based health check system, support for systemd, TLS ALPN, and a few other nice features.

Please refer to the [1.4 changelog](/download/1.4/src/CHANGELOG) and [1.5 changelog](/download/1.5/src/CHANGELOG) for more information.

Source code is available [here for 1.4](/download/1.4/src/) and [here for 1.5](/download/1.5/src/).

**Apr 1st, 2013** : _April Fool's_

I decided to [launch HAProxy in a weather ballon](/hap-in-the-sky.html) to get direct connectivity over WiFi to a few nearby datacenters.

[**_Recent news..._**](/news.html)

**Dec 28th, 2012** : _Development 1.5-dev17_

I broke a few things in dev16 which have been repaired in **1.5-dev17**.

This is a very small version with few changes.

All 1.5-dev users are then encouraged to upgrade to [dev17](/download/1.5/src/).

**Dec 24th, 2012** : _Development 1.5-dev16_

Here comes **1.5-dev16**.

Thanks to the amazing work Sander Klein and John Rood have done at [Picturae ICT](http://picturae.com/) we could finally spot the freeze bug after one week of restless digging !

This bug was amazingly hard to reproduce in general and would only affect POST requests under certain circumstances that I never could reproduce despite many efforts.

It is likely that other users were affected too but did not notice it because end users did not complain (I'm thinking about webmail and file sharing environments for example).

During this week of code review and testing, around 10 other minor to medium bugs related to the polling changes could be fixed.

Another nasty bug was fixed on SSL.

It happens that OpenSSL maintains a global error stack that must constantly be flushed (surely they never heard how errno works).

The result is that some SSL errors could cause another SSL session to break as a side effect of this error.

This issue was reported by J.

Maurice (wiz technologies) who first encountered it when playing with the tests on [ssllabs.com](http://www.ssllabs.com/).

Another bug present since 1.4 concerns the premature close of the response when the server responds before the end of a POST upload.

This happens when the server responds with a redirect or with a 401, sometimes the client would not get the response.

This has been fixed.

Krzysztof Rutecki reported some issues on client certificate checks, because the check for the presence of the certificate applies to the connection and not just to the session.

So this does not match upon session resumption.

Thus another ssl\_c\_used ACL was added to check for such sessions.

Among the other nice additions, it is now possible to log the result of any sample fetch method using "%\[\]".

This allows to log SSL certificates for example.

And similarly, passing such information to HTTP headers was implemented too, as "http-request add-header" and "http-request set-header", using the same format as the logs.

This also becomes useful for combining headers !

Some people have been asking for logging the amount of uploaded data from the client to the server, so this is now available as the "%U" log-format tag.

Some other log-format tags were deprecated and replaced with easier to remind ones.

The old ones still work but emit a warning suggesting the replacement.

And last, the stats HTML version was improved to present detailed information using hover tips instead of title attributes, allowing multi-line details on the page.

The result is nicer, more readable and more complete, as can be seen on the [demo page](http://demo.haproxy.org/).

All 1.5-dev users are then encouraged to upgrade to [dev16](/download/1.5/src/).

**Update:** minor last-minute regression on the stats page, please use the [latest snapshot](/download/1.5/src/snapshot/) instead.

**Dec 12th, 2012** : _Development 1.5-dev15_

This is an incremental fixup on top of dev14 to address [the few remaining bugs](/download/1.5/src/CHANGELOG) that were reported since its release, and particularly the high CPU usage that a few users have reported.

Some SSL issues were also fixed and its cache was improved to use 4 times less memory.

The conditions to enable compression were tightened.

The strange server errors that were logged and counted for years were in fact client errors, and that was fixed.

SSL handshake errors are now logged.

Tracking layer 7 information is now possible ; it was limited to "src" till now.

It will allow people behind proxies to benefit from some scraping or DoS protection.

All 1.5-dev users are then encouraged to upgrade to [dev15](/download/1.5/src/).

**Nov 26th, 2012** : _Development 1.5-dev14_

This is a quick fixup for [all the bugs](/download/1.5/src/CHANGELOG) that were reported in dev13.

All users are encouraged to upgrade to [dev14](/download/1.5/src/) and to drop both dev12 and dev13 !

**Nov 22th, 2012** : _Development 1.5-dev13 with Compression!_

This is the largest development version ever issued, 295 patches in 2 months!

We managed to keep the [Exceliance](http://www.exceliance.fr/en/) team busy all the time, which means that the code is becoming more modular with less cross-dependences, I really like this !

First, we got an amazing amount of feedback from early adopters of dev12.

It seems like SSL was expected for too long a time.

We really want to thank all those who contributed patches, feedback, configs, cores (yes there were) and even live gdb access, you know who you are and you deserve a big thanks for this!

Git log says there were 55 bugs fixed since dev12 (a few of them might have been introduced in between).

Still, this means that dev12 should be avoided as much as possible, which is why I redirected many of you to more recent snapshots.

These bugs aside, I'm proud to say that the whole team did a really great job which could be summarized like this :

1.  SSL:
    *   many more features ; client and server certificates supported on both sides with CA and CRL checks. Most of the information available in SSL can be used in ACLs for access control. Some information such as protocol and ciphers can be reported in the logs. These information are still not added to HTTP logs though, a lot of config work is still needed.
    *   cache life time and maximum concurrent SSL connections can be set. Unfortunately OpenSSL happily dereferences NULL malloc returns and causes the process to die if memory becomes scarce. So we can only limit its maximum amount of connections if we want to limit the memory it uses.
    *   TLS NPN was implemented with the help from Simone Bordet from Jetty, and can be used to offload SSL/TLS for SPDY and to direct to a different server depending on the protocol chosen by the client.
    *   Ivan Ristic from [ssllabs](https://www.ssllabs.com/) and Andy Humphreys from Robinson-way provided very valuable help in diagnosing and fixing some nasty issues with aborts on failed handshakes and improve [from an E-grade to an A-grade](https://www.ssllabs.com/ssltest/analyze.html?d=demo.haproxy.org).
2.  HTTP Compression
    *   HTTP payload compression was implemented at Exceliance to achieve bandwidth usage reduction and reduce page load time on congested or small links. Compression is extremely CPU and memory intensive, so we spent most of the time developing dynamic adaptations. It is possible to limit the maximum RAM dedicated to compression, the CPU usage threshold and bandwidth thresholds above which compression is disabled. It is even possible to adjust some of these settings from the stats socket and to monitor bandwidth savings in real time. Proceeding like this ensures a high reliability at low cost and with little added latency. I've put it on the haproxy web site with nice bandwidth savings (72% avg on compressible objects, 50% on average, considering that most downloads are compressed sources). I must say I'm very happy of this new feature which will reduce bandwidth costs in hosted infrastructures ! And it goes back to the origins of haproxy in zprox 14 years ago :-)
3.  Health checks
    *   SSL is now usable with health checks. By default it is enabled if the server has the "ssl" keyword and no "port" nor "addr" setting. It can be forced using "check-ssl" otherwise. So now running an HTTPS health check simply consists in using "option httpchk" with "ssl" on the server.
    *   send-proxy is also usable with health checks, with the same rules as above, and the "check-send-proxy" directive to force it. The checks also respect the updated spec which suggests sending real addresses with health checks instead of sending unknown addresses. This makes it compatible with some products such as postfix 2.10 for example.
4.  Polling
    *   speculative polling was generalized to all pollers, and sepoll disappeared as it was superseded by epoll. The main reason for this important change is the way OpenSSL works and the fact that it can easily get stuck with some data in buffers with no I/O event to unblock them. So we needed to engage into this difficult change. I'd have preferred to delay it to 1.6 if I was offered the choice ! But in the end this is good because it's done and it improves both performance and reliability. Even select() and poll() are now fast.
    *   the maxaccept setting was too low on some platforms to achieve the highest possible performance, so it was doubled to 64 and is now per listener so that it automatically adjusts to the number of processes the listener is bound to. This ensures both best performance in single process mode, and quite good fairness in multi-process mode.
5.  Platform improvements
    *   Linux 3.6 TCP Fast Open is supported on listeners ("tfo" bind keyword). This is used to allow compatible clients to re-establish a TCP connection in a single packet and save one round-trip. The kernel code for this is still young, I'd be interested in any feedback.
    *   use of accept4() on Linux >= 2.6.28 saves one system call.
6.  Process management
    *   stats socket can now be bound to specific processes. This is useful to monitor a specific process only.
    *   "bind-process" now supports ranges instead of silently ignoring them.
    *   "cpu-map" establishes a mapping between process numbers and CPU cores. This is important when running SSL offloaders on dedicated processes because you don't want them to pollute the low-latency L7 core.
7.  Misc : "redirect scheme" makes it easier to redirect between http and https, config error reporting was improved for "bind" and "server" lines by enumerating the list of supported options dynamically.

I must say I'm much more confident in dev13 than I was with dev12 and I have already upgraded the main web site which has been upgraded every few days with recent snapshots.

I've build and run it on Linux i586/x86\_64/armv5/v7, OpenBSD/amd64 and Solaris/sparc without any issue anymore.

To all those running SSL tests on dev12, please drop it for dev13.

I don't think we introduced regressions (but that's still possible), but I know for sure that we fixed a lot!

The usual [changelog](/download/1.5/src/CHANGELOG) and [source](/download/1.5/src/) are available at the usual place.

**Sept 10th, 2012** : _Development 1.5-dev12 with SSL!!!_

The main, long-awaited, feature this time is **native SSL** support on both sides, with **SNI** and **multi-process session sharing**.

The work took several months to be done at [Exceliance](http://www.exceliance.fr/en/) because it required a major rewrite of the lower connection layers in order to support multiple data layers.

This was a very painful task, but doing so allowed us to shrink the SSL patch from several thousands of lines of hardly maintainable code to a few hundreds of SSL-specific code.

The code supports the Server Name Indication TLS extension (SNI), which consists in presenting the certificate which matches the host name requested by the client.

This also works with wildcard certificates, of course.

The certificates can be loaded from a directory, which makes it more convenient to load hundreds or thousands at a time.

And since they are loaded into a binary tree, there is no lookup overhead even if there are hundreds of thousands, which is very convenient for massive hosting providers.

In current state, the code does not yet support checking certificates, which also means that connecting to an SSL server is only useful if the LAN is safe (in short, it's only useful if the server absolutely wants to get the connection to port 443).

But the Exceliance team is actively working on this.

We took care of correctly arranging connection and data layers.

Right now it's perfectly possible to chain multiple layers of haproxy servers to offload more SSL, using SSL-ID affinity and the PROXY protocol in order not to lose the client's source address.

Doing this with off-the shelf hardware can result in quite a cheap SSL offloader even for huge loads.

We measured 4000 TPS on SSLv3 on an Atom D510 and have not yet run the tests on larger hardware.

Among the other features in this version, we can list IPv6 transparent mode, "base" pattern/acl to match a concatenation of the Host header and the URI, "urlp\_val" ACL to match a URL parameter's value, support for the "nice" keyword on "bind" lines to change the priority of sessions using this bind line (useful to limit SSL CPU impact), the ability to clear/feed stick-table entries on the stats CLI (which got lost forgotten in a dead branch), and the usual set of halog features and optims.

The [changelog](/download/1.5/src/CHANGELOG) is available for more information, though there are a lot of commits to transform the connection layers.

Users who need SSL should really [give it a try](/download/1.5/src/).

While we got a number of useful reports on the mailing list and could fix some issues, it is very likely that some bugs remain, so if you observe abnormal behaviours, please report your experiences there.

On the stable branch side, [1.4.22](/download/1.4/src/) was silently released one month ago with a number of small fixes and a number of minor feature improvements, such as the ability for putting a server in soft-stop mode from the stats web page in admin mode, and support for the "httponly" and "secure" flags on cookies.

**June 4th, 2012** : _Development 1.5-dev11_

A large number of bugs were fixed again since 1.5-dev10, some of them being regressions from 1.5-dev8 and later versions.

See the [changelog](/download/1.5/src/CHANGELOG) for more information, but nobody should be running on dev9 nor dev10.

Minor harmless features were added in dev11, such as new actions on the stats page, a few new cookie options, and some minor improvements on URI hashing and server recovery mode.

Users should really [upgrade](/download/1.5/src/), as I don't want to waste time trying to spot stupid bugs in configs that are notoriously broken.

**May 21st, 2012** : _Stable 1.4.21_

A number of old bugs were reported recently.

Some of them are quite problematic because they can lead to crashes while parsing configuration or when starting up, which is even worse considering that startup scripts will generally not notice it.

Among the bugs that [1.4.21 fixes](/download/1.4/src/), we can list : risk of crash if using reqrep/rsprep and having tune.bufsize manually configured larger than what was compiled in, risk of crash when using header captures on a TCP frontend (uncaught invalid configuration), risk of crash when some servers are declared with checks in a farm which does not use an LB algorithm (eg: "option transparent" or "dispatch"), "balance source" did not correctly hash IPv6 addresses resulting in IPv4 connections to IPv6 listeners always having the same hash.

Some other minor fixes and improvements were merged.

While it's very likely that almost nobody is affected by the bugs above, troubleshooting them is annoying enough to justify an upgrade.

**May 8th, 2012** : _Development 1.5-dev9_

Many new features [were added](/download/1.5/src/CHANGELOG) since 1.5-dev7 (I forgot to announce dev8 here).

Let's summarize this shortly : new logging subsystem with customizable log formats, a unique-ID generator, full rework of the buffers and HTTP message storage, merge of the ACL and pattern fetch code, ACL support for IPv6 addresses, cookies, URL parameters and arbitrary payload, support for specifying a precise occurrence in fetch functions, much better error reporting for ACL parsing errors, the long-awaited "use-server" directive, minor improvements to the error capture reports, and a significant number of bugfixes.

Please [give it a test](/download/1.5/src/).

**March 10th, 2012** : _Stable 1.4.20_

A few bugs were reported since 1.4.19 was released, and some were found in 1.5 during development.

Servers tracking disabled servers would still be used while disabled.

Zero-weight servers could still dequeue requests pending in the backend's queue.

The build was broken on FreeBSD since 1.4.19.

Since the introduction of client keep-alive, a server would not pick a pending requests after releasing a connection if it keeps exactly maxconn-1 connections, which is problematic with low maxconn values.

POST requests smaller than the buffer would experience an undesirable additional delay of 200ms due to a flag being left unconditionally enabled on the buffer.

Sometimes when sending data wrapping across the buffer, haproxy would fail to merge TCP segments into a single one, which results in a few PUSH packets that can sometimes be observed during chunked-encoded transfers (this was just a missed optimization). [1.4.20 was released](/download/1.4/src/) with all these changes.

Some of them are important enough to justify an upgrade, eventhough they've been here for a very long time.

**January 8th, 2012** : _Stable 1.4.19_

A few bugs were fixed since 1.4.18, and they impacted users so I wanted to release something now eventhough none of them is critical.

First, Sagi Bashari fixed the usage of alternative header name for the "forwardfor" option.

An incompatibility between server tracking and slowstart, was diagnosed by Ludovic Levesque : the weight would remain at the lowest level forever.

Daniel Rankov reported that option nolinger did not work in backends.

It looks like it has been the case for a very long time now.

An issue in the string indexing in ebtrees was diagnosed by Julien Thomas.

It is used in ACLs could theorically affect the ACL code though it has no visible effect since all patterns in the same ACL are interchangeable.

Timothy Garnett reported an issue where Ruby clients were experiencing an extra delay in response time.

After analyzing some network traces, it appeared that Ruby likes to send POST requests in multiple incomplete packets, waiting for the first one to be ACKed before pushing the rest, which is incompatible with the delayed ACK.

Since we get the incomplete request, we can notice that it's missing data and re-enable quick ACKs to make the client send the rest ASAP.

Obvously the client should be fixed as its behaviour makes it very sensible to network latency.

Brian Lagoni reported that TProxy broke after Linux 2.6.34 kernel, because the address family was previously assumed to be AF\_INET and was not set in HAProxy.

Last bug, I was fed up with HAProxy blocking invalid server responses which were sent without headers.

I finally understood that it was because some requests were sent with a "\\0" in the URI which HAProxy did not block, and Apache considered the request line truncated and ignored the HTTP version, resulting in HTTP/0.9.

So the request parser was modified to reject control characters in the URI (the standard forbids other characters but we can't change too much in a stable version without risking breaking some setups).

One minor feature was merged.

Mark Lamourine worked on a solution to send a server's name in a header when connections are established to a server.

I know this can be useful in some silo-like setups and the code does not present any risk of regression so I accepted to include it in 1.4.

So [1.4.19 was released](/download/1.4/src/) with all these changes.

If you have no problem with current version, there is no need to upgrade.

**September 16th, 2011** : _Stable 1.4.18_

The fix for the space parsing in the headers that I made of 1.4.17 was not complete, because it results in negative header lengths being returned for headers that are exclusively composed of spaces.

I have checked the whole code to see if this can have any nasty effect, and I couldn't find one, since everytime, we check the length before the contents (we're saved by an optimization).

Still, I don't like having dangerous code lie around, especially in stable versions.

I know for instance that some people apply custom patches on top of it and may get trapped.

So [i have issued 1.4.18](/download/1.4/src/) with that fix.

I also included the recent patch from Finn Arne Gangstad to split domain names on ':' too, as I agree that whenever a port is specified, the host name cannot easily be checked.

And I added a match for header length so that it's now a lot easier to check for an empty header.

The rest are just usual doc and halog updates.

I don't think there is any specific reason to rush on this new version, but if you're in the process of upgrading an older one, please avoid 1.4.17 and use 1.4.18 instead.

**September 10th, 2011** : _Development 1.5-dev7_

Five months have elapsed since 1.5-dev6.

A [massive amount of changes](/download/1.5/src/CHANGELOG) was merged since then.

Most of them were cleanups and optimizations.

A number of changes were dedicated to making listeners more autonomous.

The immediate effect is a more robust handling of resource saturation, and the second effect is the removal of the 10-years old maintain\_proxies() function which was harming performance and hard to get over.

Halog was improved too (faster with more filters).

A significant number of external contributions were merged, among them the stats socket updates to clear session-table keys by values.

There are too many changes to list, but nothing too dangerous, so I'd say it's the 1.5-dev version I trust the most today.

Please [give it a test](/download/1.5/src/).

**September 5th, 2011** : _Stable 1.4.17_

Last week an issue was discovered with an application emitting spaces after the content-length value, which caused haproxy to report an error when parsing it.

After some checks, it appeared that haproxy ought to ignore these spaces, so this was addressed.

It was an opportunity to improve invalid request and responses captures, so that any message rejected for its malformation can be captured.

A new minor feature making the X-Forwarded-For header addition conditional was added because users had to resort to complex tricks to do that.

Last, halog was updated to latest version.

Due to the issue with the header above, I [released 1.4.17](/download/1.4/src/).

Quite frankly most users don't need to upgrade.

However it's better to use this one for new deployments.

**August 6th, 2011** : _Stable 1.3.26 and status updates_

Previous 1.3 version was released 14 months ago, the same day as 1.4.8.

Since then, a number of fixes went into 1.4 and [a part of them were queued for 1.3](/download/1.3/src/CHANGELOG).

These fixes are not \*that much\* important but are still worth a release.

Thus, both 1.3.26 and 1.3.15.13 were released and are available as [source](/download/1.3/src/) and [precompiled binaries](/download/1.3/bin/) for Linux/x86 and Solaris/sparc.

I realized that I don't use 1.3 anymore myself, and for this reason I'm afraid of the risk of introducing regressions with future backports.

So I decided that it was time to turn 1.3 into a "**critical fixes only**" status after 2.5 years of stable releases and 5 years of existence, meaning that minor fixes will probably never get there anymore, and that future releases, if any, will be focused on important bugs.

That does not mean it's not supported anymore, but that fixes will come at a very slow pace and that new deployments are encouraged to use 1.4 if they expect a responsive support.

I'm also switching the 1.3.14 and 1.2 branches to the "**unmaintained**" status since nobody appears to be using them anymore (last fixes were more than 2 and 3 years ago respectively).

**August 5th, 2011** : _Stable 1.4.16_

Since 1.4.15 was released 2 months ago, very few minor bugs were detected.

They were so minor that it was worth waiting for other ones to be found, but after some time, there wasn't any point making users wait any more, so I [released 1.4.16](/download/1.4/src/).

A few minor improvements were also made based on feedback from users.

Among the changes, MySQL checks now support Mysqld versions after 5.5, health checks support for multi-packet response has been fixed, the HTTP 200 status can be configured for monitor responses, a new http-no-delay option has been added to work around buggy HTTP implementations that assume packet-based transfers, chunked-encoded transfers have been optimised a bit, the stats interface now support URL-encoded forms, and halog correctly handles truncated files.

There is no real emergency to upgrade.

**June 7th, 2011** : _Country IP Blocks needs help_

Quite a few HAProxy users rely on geolocation lists freely provided by [Country IP blocks](http://www.countryipblocks.net/), either to add a request header indicating the origin country, or to select the datacenter closest to the client.

Now this nice service needs some money to continue operations otherwise they're forced to close.

They're asking for donations.

Their service has been offered for free with a high quality to many HAProxy users for some time now, I think it would really be fair that these users in turn help their nice provider.

They need **$2000 before next week**, this certainly is achievable if all big site using their lists donate $100 each to keep them alive.

**Never forget that for any free software or service on the Net, there are always people working hard to keep the service alive and who have to pay bills at the end of the month**.

**May 31st, 2011** : _HAProxy participates to IPv6 day_

About two weeks ago I registered to participate to the [World IPv6 day](http://worldipv6day.org/).

The concept is very simple : on June 8th, many web sites will be available both in IPv4 and IPv6.

Why only that day ?

Because there exists some places where IPv6 can be resolved but not reached, causing the dual-stack sites to be unreachable from these places.

By having many sites running IPv6 on the same day, network admins will notice the problem comes from their site and not from the outside since many sites will be unreachable at the same time.

HAProxy was running dual-stack a few years ago but I had to revert this due to many problem reports.

Still some visitors might have noticed the little green image indicating to them if their browser can connect to IPv6.

Since I noticed on the [participants list](http://www.worldipv6day.org/participant-websites/index.html) that some sites were already running with dual-stack enabled, I decided to enable it here again in advance, so that I'll be able to revert it in case some visitors report any issue.

If no issue is reported until June 8th, I'll probably leave that enabled.

Unfortunately, the [Dedibox](http://www.dedibox.fr/) serving as a cache for the web site is in a network that is not yet IPv6-enabled.

That's really a shame, considering that we upgraded it from an old box that was on an IPv6-capable network.

I really don't understand what's happening at Free for taking that long a time to enable IPv6 on all their network segments, it does not seem to be on their top priority list.

But since the site is running at home behind my [Nerim](http://www.nerim.net) internet access which has been IPv6-enabled for something like 10 years now, I could announce the ADSL endpoint address in the DNS.

Enabling IPv6 on your web site really is trivial with HAProxy.

You just have to add "bind :::80" to your frontend and announce the IPv6 address as an AAAA record in your DNS zone, and that's all.

No readdressing, no routing changes, nothing fancy.

And you can even get IPv4/IPv6 statistics like [here](http://demo.haproxy.org/).

BTW, I know for sure that some of the World IPv6 Day participants have done exactly that with their HAProxy config too :-)

**Apr 8th, 2011** : _stable 1.4.15 & 1.5-dev6_

Two annoying bugs were detected on 1.4 at Exosec, one week apart.

The first one limits the usable content-length to 32-bit on 32-bit platforms, despite the efforts made in the code to support 64-bit quantities everywhere.

It was then fixed in 1.4.14.

Yesterday, while working on the backport of 1.4 fixes to 1.3, I spotted that the patch to fix the issues with spaces in cookies that was merged in 1.4.9 introduced a regression due to a typo.

In some circumstances, a malformed header sent by the server can crash haproxy when cookie-based persistence is enabled.

Thus 1.4.15 was released as an emergency update to address this.

The bug has never been reported because it's extremely unlikely to appear, unless a server tries to provoke it on purpose.

In the mean time, 1.5-dev4 was released with a huge amount of fixes and architectural reorganizations (too many to list here), which were needed to continue the work towards server-side keep-alive.

1.5-dev5 enabled server-side IPv6 support and fixed a number of remaining bugs.

1.5-dev6 was finally released to address the last regressions reported on the list yesterday as well as the important bug above.

Now, everyone should have understood that all users of 1.4 >= 1.4.9 or 1.5 > 1.5-dev3 must upgrade.

Please consult the [1.4](/download/1.4/src/) [CHANGELOG](/download/1.4/src/CHANGELOG) and the [1.5](/download/1.5/src/) [CHANGELOG](/download/1.5/src/CHANGELOG) for more information.

**Mar 9th, 2011** : _stable 1.4.13_

Many annoying bugs were discovered both when working on 1.5-dev and by users.

Some headers were not correctly processed after removal of the last header (issue reported to the list by Stefan Behte), disabling a disabled proxy from the CLI could result in a segfault (reported by Bryan Talbot, fixed by Cyril Bonté), "balance url\_param" was completely broken on POST requests (reported by Bryan Talbot too), it is theorically possible to get HTTP chunk size wrong if only the CR is sent as the last byte of the buffer, waiting for the LF to wrap around in a subsequent packet, ACLs loaded from a file did not correctly close the file descriptor upon success (reported by Bertrand Jacquin), the recently added srv\_id ACL could segfault if the server is not known (reported by Hervé Commowick), rlimits were not correctly updated for listening sockets (reported by the loadbalancer.org team), the stats page in admin mode did not support multi-packet requests (fixed by Cyril).

1.4.12 was released with all those fixes, and Hank A.

Paulson reported a crash with pattern files with empty lines caused by a regression introduced into 1.4.11 by a fix for correctly handling empty lines.

So [1.4.13 was released](/download/1.4/src/CHANGELOG) a few hours later to avoid any issue.

I'd like to thank all of these contributors, because well-detailed bug reports are equally important as code contributions.

Once again, all users of 1.4 are encouraged to upgrade in order to avoid boring troubleshooting of stupid bugs.

This time I have added Sparc builds too, as there are still requests for those.

As usual, please check [Changelog](/download/1.4/src/CHANGELOG), with [sources](/download/1.4/src/) and Linux [binaries](/download/1.4/bin/) at the usual places.

**Feb 10th, 2011** : _stable 1.4.11_

While working on keep-alive on 1.5, several issues were discovered, some of which were found to also affect 1.4.

For this reason, I preferred to delay the next 1.4 release to until 1.5-dev4 was complete but development has recently stalled, so I preferred to release [1.4.11](/download/1.4/src/CHANGELOG) anyway.

One bug is tagged as **critical** because it can cause a session to remain indefinitely upon certain conditions that are hard but not impossible to trigger when a server dies.

A bug in the ebtree code could cause stick tables to not always match arbitrary length keys.

Cyril Bonté has definitely fixed the http-pretend-keepalive option to correctly handle the situations where it was combined with httpclose or in tunnel mode.

Until now, it was common to see the client wait for the server to close the connection before returning, causing very bad performance.

Since all combinations were extensively tested, I think we should be OK now.

Some error conditions were fixed to report correct flags in the logs (eg: client aborts in the middle of HTTP trunking used to report chunking errors).

There was an issue with server connection error processing which prevented pending connections from being processed when maxconn was set to 1, because the current connection was counted in them.

The error capture from the stats socket is now also able to report incorrectly chunked data.

This helps troubleshooting faulty applications.

Also the error captures now include an error counter to ease processing with external monitoring scripts.

Joe Williams added a global "log-send-hostname" statement which makes it possible to pass the hostname field in the emitted syslog messages.

Other various minor improvements on the config parser were merged too.

With all that, all users of 1.4 are strongly encouraged to upgrade.

As usual, please check [Changelog](/download/1.4/src/CHANGELOG), with [sources](/download/1.4/src/) and Linux [binaries](/download/1.4/bin/) at the usual places.

**Nov 11th, 2010** : _devel 1.5-dev3_

Haproxy [1.5-dev3](/download/1.5/src/CHANGELOG) was released with everything that went into 1.4.9, plus some added bonus that were mainly developped at Exceliance, among which support for binding to UNIX socket on the accept side so that Haproxy can now receive connections over a UNIX socket.

This is particularly useful when combined with stunnel, for which [a patch](/download/patches/stunnel-4.34-exceliance-aloha-unix-sockets.diff) is also available.

The new [PROXY protocol](/download/1.5/doc/proxy-protocol.txt) was implemented in order to permit stunnel to forward transport-level information to haproxy, such as the protocol, source and destinations of an incoming connection, so that haproxy can make use of that everywhere internally (acls, logs, transparent, ...) instead of stunnel's address.

The main advantage over the x-forwarded-for patch is that it now supports keep-alive and is not limited to HTTP anymore.

When combined with the UNIX socket, it can make haproxy and stunnel integrate seamlessly and reliably, provided that [this patch](/download/patches/stunnel-4.33-exceliance-aloha-sendproxy.diff) is applied to stunnel.

Stick tables can now learn from responses, which enables SSL-ID stickiness.

And more importantly, stick-tables can now be synchronized in a multi-master fashion between multiple haproxy instances.

Also, during soft-restarts, the new process learns the table from the old one so that restarts do not lose that precious information anymore.

This tough task was the second half of the large work co-sponsored by [Exceliance](http://www.exceliance.fr/) and [LoadBalancer.org](http://www.loadbalancer.org/).

**Oct 29th, 2010** : _stable 1.4.9_

Four months after 1.4.8 was released, some minor issues have accumulated and a new release was necessary.

It was also an opportunity to add some long-awaited minor feature improvements.

Among the issues that were fixed, a listener could be left in an unrecoverable state in case of memory shortage during an accept().

POST requests that were followed by a CRLF (forbidden) in a late packet could cause some TCP resets to be emitted on Linux due to those two unread bytes (diagnosed with Dietrich Hasselhorn).

Servers that were disabled while processing requests could still drain new requests from the global queue.

HTTP header handling for ACLs did not correctly consider quotes and used to consider commas within quotes as a list delimitor.

A server with address 0.0.0.0 used to rely on the system to connect to this address (which is always itself).

Now it forwards the connection the same way as in the transparent mode.

Various error reports and logs were fixed or improved, and many doc typos were fixed.

Now concerning the improvements, Krzysztof Oledzki improved his netsnmp-perl plugin to support listening sockets, and Mathieu Trudel's Cacti templates were merged.

Judd Montgomery and Cyril Bonté's work to support setting servers up/down from the stats interface has been merged too.

Gabor Lekeny added LDAPv3 health checks.

Hervé Commowick improved the MySQL check to support a complete login sequence with a real username.

When option "abortonclose" is set and a client disconnects while waiting for the server, now we forward the close notification to the server.

That way the server can decide whether to continue or close.

This is important for servers dealing with long polling requests.

The Explicit Content Validation (ECV) check code was finally merged after 18 months of reviewd and fixes by various people.

That was one major cause for delaying this release.

Health checks can now rely on a string that is looked up in server responses.

Persistence cookies now support inactivity timeouts and time to live.

This is needed with some new terminals such as iPhones where the browser is never closed and the terminal sticks to the same server forever (which is particularly undesired during a partial outage).

Also, we now have a new "preserve" option for cookies in "insert" mode, which indicate that if the server sets the cookie, then we let it pass unaffected.

This allows servers to terminate persistence upon logout.

Last, the "halog" utility was improved to support per-url and per-termination code statistics.

This means that it's now trivial to know what URLs take the most processing time.

Version [1.4.9](/download/1.4/src/CHANGELOG) was released with all that, with [sources](/download/1.4/src/) and Linux [binaries](/download/1.4/bin/) at the usual places.

Some of these fixes will slip into 1.3 too.

**Oct 23th, 2010** : _new httperf results : 572000 reqs/s_

This morning I came across [this interesting post](http://kristianlyng.wordpress.com/2010/10/23/275k-req/) from Kristian Lyngstol about the performance tests he ran on the [Varnish](http://www.varnish-cache.org/) cache.

What struck me was the number of requests per second Kristian managed to reach : 275000, not less.

I'm not surprized at all that Varnish can withstand such high rates, it's known for being very fast.

My surprize came from the fact that Kristian managed to find fast enough tools to run this test.

My old injector is limited to around 100k requests per second on my machines, as it does not support keep-alive, and Apache's ab to around 150k with keep-alive enabled.

And when I managed to reach 2 millions requests per second, I was feeding a constant stream of pipelined requests with netcat, which is particularly inconvenient to use.

Kristian said he used [httperf](http://www.hpl.hp.com/research/linux/httperf/).

I tried it in the past but did not manage to get good numbers out of it.

He said he found some "httperf secrets", so that made me want to try again.

First tests were limited to approximately 50000 requests per second with httperf at 100% CPU.

Something close to my memories.

But reading the man, I found that httperf can work in a session-based mode with the "--wsess" parameter, where it also support HTTP pipelining.

Hmmm nice, we'll be less sensible to packet round-trips :-) So I tried again with haproxy simply doing redirects.

Performance was still limited to 50000 requests per second.

In fact, there appears to be a default limit of 50000 requests per second when "--rate" is not specified.

I set it to 1 million and ran the test again.

Result: about 158000 requests per second at 100% CPU and with haproxy at 44%.

Since my machine is a Core2 Quad at 3 GHz, I fired 3 httperf against one haproxy process.

The load reached a max of 572000 requests/s with an average around 450000 requests per second.

This time, haproxy and all 3 httperf were using 100% CPU.

What an improvement!

[![](img/haproxy-572krps-sm.gif)](img/haproxy-572krps.gif)  

These tests mean nothing at all for real world uses of course, because when you have many clients, they won't send you massive amounts of pipelined requests.

However it's very nice to be able to stress-test the HTTP engine for regression testing.

And this will be an invaluable measurement tool to test the end-to-end keep-alive when it's finished.

I still have to figure out the meaning of some options and how to make the process less verbose.

Right now it fills a screen with many zeroes, making it hard to extract the useful numbers.

I'm grateful to Kristian to have made me revisit httperf !

**Aug 26th, 2010** : _devel 1.5-dev1 with many goodies_

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

**June 16th, 2010** : _stable 1.4.8 and 1.3.25_

Today, Ben Congleton, Morten Gade Sørensen and Hervé Commowick reported and diagnosed two bugs in 1.4.7.

One was a regression introduced in 1.4.7, breaking the stick-table feature due to a side effect of the fix for a memory leak in it.

The second one is quite old, it dates 1.3.16 (2 years old) !

It causes crashes soon after a connection has matched a monitor-net in a tcp-only instance.

I wanted to quickly fix both issues so that users who have not yet upgraded to 1.4.7 don't waste their time, and I'm very grateful to the 3 guys above who were extremely reactive and allowed the bugs to be fixed in a few hours.

Finally, Patrick Mézard's doc updates were merged too.

Version [1.4.8](/download/1.4/src/CHANGELOG) was released, with [sources](/download/1.4/src/), Linux and Solaris [binaries](/download/1.4/bin/) at the usual places.

Version [1.3.25](/download/1.3/src/CHANGELOG) was released too with a few other pending fixes, and [sources](/download/1.3/src/) and Linux/Solaris [binaries](/download/1.3/bin/) at the usual places too.

Users of 1.3 after 1.3.16, or 1.4 with TCP only frontends will likely want to upgrade, eventhough if they have not been hit yet, they will probably never be.

Users of stick-tables will have to upgrade too.

The fact that we're now spotting bugs that have been there for two years is an encouraging sign of stability.

**June 10th, 2010** : _stable 1.4.7_

Jeff Persch debugged the trouble affecting consistent hashing about two weeks ago.

I wanted to issue 1.4.7 right after that fix got merged but I was lucky enough to spot a few minor bugs in the following days, so that finally got delayed.

Most of these issues are really minor and were found while reviewing the code in preparation of 1.5-dev.

Some stats were not accounted properly (_failed req_ instead of _denied req_), some termination flags in the logs could be wrong, which is a shame because we use them for debugging, a TCP to HTTP transition was not properly handled, and the dispatch and http\_proxy modes were broken since 1.4-dev, but apparently nobody uses them anymore.

Some people will like the new halog, as it is able to report per-server stats on status codes, error ratios, average connection times and response times, which is very handy for quick checking of your prod's health.

The complete ChangeLog for **version 1.4.7** is [here](/download/1.4/src/CHANGELOG) and the sources are [here](/download/1.4/src/).

On a side note, someone asked on the list how haproxy would perform on a [Guruplug Server Plus](http://1wt.eu/articles/guruplug-slow-heater/).

I ordered one a few months ago and finally received it.

Well, it's a disaster, not only it is slower than the Geode, but it heats so much that metal parts hurt to the touch and power supplies fry after a few months.

Definitely not something to buy.

Check the full review on previous link if you're interested.

**May 16th, 2010** : _stable 1.4.6_

Version 1.4.5 triggered a conflict in a macro name with some Linux distros shipping glibc >= 2.10.

Since this affects most recent distros, it was better to upgrade now.

A few points about RDP cookies were clarified in the doc.

Last, a new ACL match **srv\_is\_up()** has been added, to consider a specific server's state in ACLs.

Those who had no problem building 1.4.5 don't really need to upgrade. mixing them with fixes.

**May 13th, 2010** : _stable 1.4.5_

No reliability issue was reported since 1.4.4 was released.

This is a very good thing, because some people were asking for a few minor features, so it was a good opportunity to get them merged without mixing them with fixes.

The ChangeLog for **version 1.4.5** is [here](/download/1.4/src/CHANGELOG) and the updates are [here](/download/1.4/src/).

First, Cyril Bonté provided the new **ignore-persist** directive. it allows haproxy to ignore the persistence cookie on some requests which validate an ACL-based condition.

It is particularly suited to optimise the load balancing of static or stateless objects in the middle of a stateful farm.

Second, it was planned 3 years ago to be able to feed ACLs with large data sets loaded from files, but it was still not implemented due to the lack of precise needs.

Now, 3 years later, more and more people are reporting difficulties writing large configurations, and the last config I saw which was 104000 lines long convinced me that it was urgent to support this feature.

But matching requests against very large datasets can be CPU intensive, so I have extended my Elastic Binary Trees to support new lookup methods and now it is possible to lookup a string or an IP address among tens of thousands in a few tens of nanoseconds.

This means that **it is now possible to use haproxy to perform geolocation**.

For instance, checking that a source address belongs to one of the 38400 european networks only consumes 2% CPU at 40000 requests per second.

The rest are just minor improvements.

Tt's now possible to stick on an IP address extracted from an HTTP header, and I improved a bit more the halog analyser, which is now possible to report request counts by status codes.

It also gained some nice performance boost as it can now parse about 1.3 Gigabytes of logs per second on a 3 GHz Core2.

I expect that this version will take some time to spread because it only contains new features and will likely not be backported to various distros.

Still, some power users will probably interested in giving it a try.

**April 7th, 2010** : _stable 1.4.4_

Some people were experiencing optimisation issues with Tomcat and Jetty, with which it was not possible to perform client side keep-alive when the server received a "Connection: close" header.

This is due to a strange design choice by which they decide the client is not interested in the response length if it intends to close after the transfer!

Well technically that works... most often...

Sometimes users may get truncated objects without being aware of that.

Anyway, Cyril Bonté had a very smart idea for a workaround : pretend to the server we'll maintain its session alive while it's false.

This fixed the problem, and is now available by adding **option http-pretend-keepalive** to option http-server-close.

Jetty's HTTP implementation seems to be the flakiest though.

It even manages to send "HTTP/1.1 100 Continue" intermediate responses when the client sends "Expect: 100-continue", but it closes the connection just after that message, resulting in a 502 error for the client.

Cyril also fixed an issue with appsession where a cookie whose name begins like the appsession cookie could be mistaken for it.

Those issues were enough to justify a new release.

Very few other minor fixes [were brought there](/download/1.4/src/CHANGELOG), and a minor feature was added.

It consists in being able to bind to a source address found in a header when connecting to a server.

Normally this will be the X-Forwarded-For header.

This requires use of the Linux kernel TPROXY patches, and makes it possible for backend servers to see the initial client's IP even when several layers of proxies have been passed through.

**March 30th, 2010** : _stable 1.4.3 and 1.3.24_

A few remaining issues and one regression [were fixed](/download/1.4/src/CHANGELOG) in 1.4. In 1.3, I have [backported](/download/1.4/src/CHANGELOG) all pending fixes since 1.3.23, most of which were discovered in 1.4. The most interested people will probably be users of FreeBSD where they could randomly get a SIGPIPE if the program was compiled on a very recent version (8, maybe 7.2 too). Anyway, due to other minor to medium fixes, 1.3 users should upgrade.  
It's worth noting that very few issues were reported on 1.4.2. The code has stabilized very quickly, and people in sensible environments will be able to start to think about evaluating it to plan an upgrade (from most reports, the new features such as client keep-alive and improved stats are very much demanded). If I could send them an advice, I'd say that we're going to release 1.4.4 soon with a few minor improvements and that if some people don't know what version they will start with, then let's start with 1.4.4 when it's available.

**March 17th, 2010** : _stable 1.4.2_

A new batch of annoying issues got fixed.

Among [these issues](/download/1.4/src/CHANGELOG), we can find a risk of crash (broken pipe) on very recent versions of FreeBSD, a segfault when using CLF logs and capturing a non existant header, a very rare case of stuck client session when using keep-alive, some garbage which appeared on the stats page after 1000 client resets, or when the host name was too long, a url\_param hash bug which could result in a dead server to be used in very rare situations, a risk of getting an empty result on the stats socket if the input closes before haproxy responds, and endless loop at config parsing time on the error-limit keyword, status codes 501 and 505 which could cause a server to be marked down if on-error was used, and a risk of getting truncated HTTP responses when chunk-encoding was used with chunk sizes that are exact divisors of the buffer size, and an issue with anonymous ACLs which were merged together into a single one.

A few improvements were made to the health checks which now support multi-packet responses, and the stats socket can now display more debug information about a specific connection.

The list is quite huge, it was important to [**release 1.4.2**](/download/1.4/src/) without waiting for any possible new issue to come, eventhough things seem to calm down.

**March 5th, 2010** : _stable 1.4.1_

Some build issues on non-Linux platforms were preventing new 1.4 adopters from trying it.

These issues are now fixed. [Other issues](/download/1.4/src/CHANGELOG) concerned the appearance of more 502 errors in the logs than with 1.3.

This was a bug that caused the status code to be changed to 502 even in case of connection abort during the data transfer.

A few new error counters were added to the stats, and other minor issues were fixed.

This new version now builds and works on FreeBSD, OpenBSD, OSX, Solaris, AIX and Linux, so let's not wait and [**release 1.4.1**](/download/1.4/src/).

Also, Solaris users will now be happy, I unpacked and replugged my Ultra5 so the Sparc binary is available again.

On a side note, I have removed the link to the haproxy.org mirror because it has been outdated for the last 6 months and even remained 1 week on an expired DNS zone.

I failed several times to contact Kevin Kuang there, so I don't even know who manages it now if any.

If someone gets in touch with him, please ask him to contact me.

**February 26th, 2010** : _**New stable branch 1.4 !**_

After 11 months of active development and a lot of external contributions, [**version 1.4 is now released**](/download/1.4/src/).

It has been tested for the last 3 weeks by many people, and only very minor bugs were reported (and fixed), so it's now time to officially stamp it as stable.

Version 1.4 brings a lot of new features, among which the long-awaited support for client-side HTTP keep-alive, the RDP protocol, and stickiness on anything, as well as many other nice usability improvements on the stats interface, checks and the CLI.

It is also much more powerful than version 1.3 and will support addition of new protocols faster than before due to a better structured internal architecture.

1.3 will still be supported for some time, and the old 1.3.15.X branch is now entering a deep freeze where only critical bugs will be fixed.

Please consult [the ChangeLog](/download/1.4/src/CHANGELOG) for more information about all the changes.

I particularly want to thank all the persons and companies who contributed to this version by code, testing or development funding ; without their efforts and participation, we would still be far away from a release !

**January 28th, 2010** : _stable 1.3.23_

Several minor bugs were fixed since **1.3.22**, and the **request-learn**, **force-persist** and **http-check send-state** were backported because people need them for more transparent and reliable application updates.

Since no new bug was in sight, and 3.5 months had elapsed since 1.3.22, it was the moment to release [1.3.23](/download/1.3/src/) with all that.

As 1.4 approaches, 1.3.23 will probably be the last 1.3 which accepts new [minor features](/download/1.3/src/CHANGELOG).

Future 1.3 versions will very likely be dedicated to bug fixes only.

**January 25th, 2010** : _1.4-dev7 & 1.4-dev8_

While trying to work on end-to-end keep-alive, I encountered issues that needed to be fixed, so this has delayed dev7 quite a lot, and it does still not have this end-to-end keepalive.

Think of it as a much cleaner dev6 instead since many bugs were fixed.

The stickiness code sponsored by [Exceliance](http://www.exceliance.fr/) and [Loadbalancer.org](http://www.loadbalancer.org/) got merged.

Currently, it can almost only learn IP addresses, but it has been designed with an amazing flexibility so that it will be very easy to add stickiness on any request or response criteria.

MySQL checks have been introduced and this code will evolve for slightly deeper and more reliable checks.

A new "force-persist" statement allows admins to test their servers without opening them to the world, which is very convenient to ensure they're correctly installed and that their customers will not face a lot of crap.

And as always, a bunch of bugs in many areas were fixed.

**Update:** 1.4-dev5 to 1.4-dev7 had a nasty bug with keep-alive enabled, so please update to 1.4-dev8.

**January 16th, 2010** : _4-hour network outage_

Some of you have noticed that the site was down from 11:45 to 15:45 local time, and it can be seen [here](http://whos.amung.us/stats/62nl1k3va5id/).

It was the longest outage I ever experienced in 8 years with my ISP ([Nerim](http://www.nerim.net/)).

The support told me the outage was at their ADSL provider, [SFR](http://www.sfr.fr/).

Well, 4 hours in 8 years is still 99.995% availability, I have nothing to complain about :-)

**January 8th, 2010** : _1.4-dev6_

As could be expected, 1.4-dev5 did not work very well.

The rule is pretty clear : if you don't like your code, it **will** fail.

Just reread the last post and you'll see that it was destined to fail.

With the nice help of Cyril Bonté and Hank A.

Paulson, we could spot a lot of bugs and I finally got rid of those parts I found ugly.

Now curiously, it works a lot better :-) Also, Krzysztof Oledzki contributed a nice feature he talked about some time ago : the **default-server** setting.

This makes it possible to specify some common settings globally and not have to repeat them for all servers.

This is useful for check intervals, maxconn, etc..

So it was time to release [1.4-dev6](/download/1.4/src/) so that all those who had a bad experience with 1.4-dev5 can try again.

This is the version currently running on the site, so it looks fine :-)

**January 2nd, 2010** : _New year, new features_

After several weeks of work, I have [committed](/git?p=haproxy.git;a=commitdiff;h=b608feb82ae08270fa97f435f065942188e7d177) the patch which introduces client-side **HTTP keep-alive and pipelining** support. The code is quite ugly and I'm not proud of it. This is because I got quite a bunch of last-minute surprises that I will have to workaround in a cleaner way. But since the code worked, I would have found it wasted to make you wait for it.  
In order to enable pipelining on the client side, just comment out any "option httpclose" statement in the defaults, frontend and backend sections and set "option http-server-close" in any of them. As the name implies it, the connection is still closed on the server side. This way we can still have low ressource usage on servers and correctly enforce maxconn while retaining keep-alive with the client.  
This code will be in **1.4-dev5** by the end of the week-end, but the impatient will be able to download a [snapshot](/download/1.4/src/snapshot/) for their tests.  
The new code has been put in test on the [Formilux](http://formilux.org/) server and already shows [decent load time savings](http://tools.pingdom.com/?url=http://www.ant-computing.com/album.html&treeview=0&column=objectID&order=1&type=0&save=false) on [this page](http://www.ant-computing.com/album.html). _Stay tuned..._

**October 18th, 2009**

I have put online a [matrix of all known bugs](/bugs/index.html) which affect stable versions 1.3 starting with 1.3.14.

It took about 4 hours of work to put that in shape but I think it was worth it.

Let's put it short : those of you running **1.3.15.2**, **1.3.16** or **1.3.17** are **doomed**.

Those running **1.3.15.X before 1.3.15.7**, **1.3.19** or **1.3.21** are at **risk**.

**1.3.14.14**, **1.3.15.10** and **1.3.20** are pretty **good**, and **1.3.22** is the only one with **no known bug** yet.

**October 14th, 2009** : _1.3.22_

A few hours after 1.3.21 was issued, John Lauro reported an important regression causing a crash when connecting to the stats socket.

This was caused by a minor backport which should have been modified for 1.3 and that I didn't detect during the tests because I did not use this socket.

**1.3.22** was released to fix this issue.

Please don't use 1.3.21 and update to 1.3.22!

**October 12th, 2009** : _1.4-dev4, 1.3.21_

A lot of changes have occured in only 3 weeks, so it was the right moment to release a new development version.

It's worth noting that Krzysztof Oledzki has been very active, contributing no less than 1/3 of all the changes.

This is nice because being two to work on the project, we progress faster.

Concerning the changes, the stats interface (socket and page) certainly is the most affected area.

It is now possible to **reset counters** and to **change a server's weight** without restarting... two features that many of you have been asking for years!

The [stats page](http://demo.haproxy.org/) now can also display a node name and description, as well as the **exact status** of a health check.

The LB algorithms have now been moved to separate files, and a [**consistent hashing**](http://www.spiteful.com/2008/03/17/programmers-toolbox-part-3-consistent-hashing/) algorithm has been added.

It allows hot addition or removal of servers without disturbing the load-balancing, which is desirable for caches.

Also, the LB rework brought the opportunity to re-enable the old **static round-robin** algorithm, which can make sense for people who run more than 4000 servers in a single backend (practical limit of the dynamic RR algorithm).

Last, some new ACLs have been added, to check for IP addresses in headers, and to check frontend's and backend's connections, queues and per-server average queue size.

A few minor bugs were fixed, and those fixes as well as some minor riskless features have been backported into 1.3 to release **1.3.21**.

**September 26th, 2009**

I found it was important to acknowledge some people and companies' efforts for the project.

So I added [a new page](/contrib.html) listing significant contributions, most often features but sometimes fixes, in the form of patches, code, time or even money.

A minor bug on the stats page which remained in 1.4-dev3 has also been fixed and is available [in the latest snapshot](/download/1.4/src/snapshot/).

**September 24th, 2009** : _1.4-dev3 + sponsors_

Most of the internal changes planned for version 1.4 have been completed, so it was time to release [a new clean snapshot](download/1.4/src/).

The architecture is now ready to permit keep-alive, SSL or FastCGI developments.

Some more changes are planned but the remaining ones should be a lot easier to perform without breaking everything.

Compared to latest stable 1.3.20 version, 1.4-dev3 provides new features, among which support for the CLF log format, RDP protocol load-balancing and persistence, a new interactive CLI, an improved HTML stats page, support for inspecting HTTP contents in TCP frontends and switching to HTTP backends (allowing HTTP+SSL to coexist on the same port), support for forcing of the TCP MSS on frontends, smart network optimizations to reduce the number of TCP packets in a session, runtime-configurable buffer sizes, support for more than 64k concurrent connections, config parser support for "no option xxx" to disable options that were enabled by default, and correct 1xx status code processing.

Developments to support keep-alive have already started, and if time permits, SSL integration will be attempted.

The code looks amazingly stable for the amount of changes, and will probably not change much anymore, so any bug found in this version must be reported and fixed.

Also, new feature submissions should be based on this version.

It will be easier to implement for submitters and for me to merge.

Several large sites are already running on 1.4-dev2 with great success.

This one should be even better, but given the number of changes, it should be monitored more closely at the beginning.

Last, I have a very good news that I hope will give ideas to others : [Exceliance](http://www.exceliance.fr/) and [Loadbalancer.org](http://www.loadbalancer.org/) have both agreed to contribute some manpower and money to implement the complete persistence framework that everyone is dreaming about into haproxy.

That's a tough work and I'm not certain it will be ready for 1.4 (though it might, depending if I'm as late on my releases as usual).

I would personally like to thank them both for their contributions.

When you have to put your money in commercial solutions, please never forget to consult first the guys who involve time and money in opensource projects, because they are the ones who help the projects evolve and live !

**August 9th, 2009** : _1.3.20_

Cristian Ditoiu from [transfer.ro](http://www.transfer.ro/) reported a major regression when testing 1.3.19.

It would crash within a few minutes while 1.3.15.10 was OK.

He offered to help so we could run gdb and debug the crash live.

We finally found that the crash was the result of a regression introduced by a recent in 1.3.19.

I really want to thank him because he spontaneously provided a lot of help and trust to debug this issue which at first glance looked impossible after reading the code and traces, but took less than an hour to spot and fix when caught live in gdb !

It's always pleasant when users show that level of involvement to chase bugs.

Another bug was reported by Romuald du Song, who found that option tcplog would log using global parameters if no logger was defined.

It can be either helpful or annoying.

This is now fixed and a warning is emitted when such a configuration is encountered, so that people running off erroneous configs can easily fix them.

This time I expect **[1.3.20](download/1.3/src/)** to be _the good one_.

It's always a good sign when we fix minor bugs or recent regressions introduced by bug fixes.

**[1.4-dev2](download/1.4/src/)** has also been released to help people track changes in the two versions in parallel.

**July 27th, 2009** : _1.3.19_

Since 1.3.18 was released two months ago, it has been widely deployed, in part thanks to the _slowloris_ tool which has caused HAProxy downloads to jump by 20-30%.

This results in more exposure and [new kinds of bugs](download/1.3/src/CHANGELOG) to be discovered.

The most annoying ones concern too short sessions which may sometimes be reported as server errors, random delays under low traffic conditions due to a scheduler bug, and the last one reported today by an [Exceliance](http://www.exceliance.fr/ahproxy.htm) customer who was kind enough to provide lots of traces, some occasional pauses on interactive TCP traffic which might also happen on the last chunk of an HTTP response, although extremely rarely.

Each one alone would have been enough to issue a new maintenance release, so here it is, **[1.3.19](download/1.3/src/)**.

It also brings a small bunch of nice new features backported from the dev tree, among which the support for multiple configuration files, the support for more than 64k concurrent connections (tested at 190k by the heavy user), and a highly better reporting of config warnings and errors.

So, as usual with maintenance releases... everyone is highly encouraged to upgrade.

Since some of the bugs above were present in earlier versions, a new release was emitted for 1.3.15 and 1.3.14 too for the late users who have not upgraded yet.

I really think it's the last one for 1.3.14.

1.3.15 might still see another one till the end of the year, and that will probably be all for this one after 20 months of free support :-)

The first development version should be released too, but I need to update my release scripts first, they are inadequate and take me too much time to use, so stay tuned !

**June 27th, 2009** : _HAProxy to counter DoS attacks_

Since the [announcement of the Slowloris](http://ha.ckers.org/slowloris/) tool, people seem to be discovering how fragile a default Apache setup can be !

Well, this is not news, as people who install Apache on high-traffic sites have been aware of this weakness for ages, and have been setting very low timeouts and disabling keep-alive in order to mitigate risks.

Now that a tool is publicly advertised, I'm beginning to hear questions from worried site admins about what to do if their site is attacked.

Also, we're seeing several sites and forums suggesting installing HAProxy in front of Apache servers to protect them (note that Nginx would probably do equally well).

Indeed, HAProxy does not need a new thread nor process to accept a new connection, it only needs some RAM (16-32 kB per connection).

Some people are already using it past 70000 concurrent connections, which cannot be achieved on Apache which needs an expensive thread or process per connection.

More specifically, HAProxy will only forward complete and valid requests.

This means that it will not bother Apache while the attacker is playing with its few thousands connections, and all valid requests will immediately pass through.

And the _icing on the cake_ is that HAProxy can kill requests which take too much time to complete, using timeout http-request (more than a few seconds is not to be considered normal).

Once again, we observe a derivate use of a load-balancer, which is a bit expected : when a tool is designed to accept 10 times more load than the servers it feeds, there is nothing surprizing that it can be used to protect them !

Let's see if Apache evolves towards providing more tunables to mitigate such attacks...

In the mean time, a drop-in anti-DoS configuration is [available here](/download/1.3/examples/antidos.cfg).

**May 10th, 2009** : _1.3.18_

Yan Qiao of [Rocket Fuel Inc](http://www.rocketfuelinc.com/) reported a crash on x86\_64, which was pretty much unexpected !

He nicely offered to help troubleshooting by rebuilding with debugging on and leaving the process running in production to catch the error, then sent me an interesting core 1 week later, which revealed that a field in the struct session which was never touched had been changed due to the sharing of two pools of the same size.

This field should have been initialized but was unfortunately not.

The issue can only happen on x86\_64 with HTTP logging enabled, due to the exact 1024 bytes of the struct session which allows its pool to be shared with the struct requri's.

Thank you guys for your huge help and the risks you have taken leaving that process running!

During a troubleshooting session with the [T20](http://www.iplt20.com/) guys ([Maxim Fedchishin](http://www.cloudadmin.info/), Jason Coward and Viktor Brilon from modX team, Hans from RightScale team), I came across an old leftover process doing nothing after a soft-reload.

That issue is brought once in a while by various people, but it happens too rarely for anyone to get an opportunity to debug it.

The guys accepted that I installed a debugger on their machine to see what the process was doing.

It was deadlocked in free() during the reload.

And that made sense : during a reload, the old process releases as much memory as possible to leave room for the new one.

If the two signals sent by the second one are too close to each other, the second signal is sent while the first one has not completed releasing memory and we can have a recursion in the libc's free(), causing a deadlock.

That has been fixed by implementing asynchronous signal delivery.

Thank you guys for giving me the opportunity to catch that rare event!

Problems aside, a few minor features were merged.

The stats are now more readable, report max session rates and provide full 64-bit counters everywhere.

It is now possible to forward invalid requests or responses without blocking them, but they will still be captured.

The config parser now warns about possibly unwanted ordering of ACLs or reqxxx/rspxxx.

Several wrong printf() format strings have been fixed.

The build process now supports an alternative architecture, and the RPM spec file has been cleaned.

A new balance hdr(header) algorithm has been added to balance depending on a header hash.

A new option enables addition of the destination IP address in the X-Original-To header.

And last but not least, the doc has been massively cleaned up and reorganised.

With [all these fixes](/download/1.3/src/CHANGELOG-1.3.18), I released **[1.3.18](download/1.3/src/)**, as well as 1.3.15.9 and 1.3.14.13 which are probably among the last ones of their respective branches after 12 and 18 months of maintenance.

**April 19th, 2009** : _new performance record broken !_

It was a long time since my last 10 Gigabit tests, exactly one year.

The Linux kernel has evolved a lot, so did HAProxy and even the Myri10GE driver.

I knew we could get much throughput since we fixed the kernel splice() syscall.

It was a good opportunity to start a [new series of benchmarks again](10g.html).

In short, new records were broken.

Full **10Gig** line rate with **20% CPU**, and the **100000** sessions/s barrier was crossed !

**March 29th, 2009** : _1.3.17_

Bart Bobrowski of [who's.amung.us](http://whos.amung.us/) reported abnormal CPU usage with the new version 1.3.16. After a full day of tests and code analysis, I failed to reproduce the issue here, and the bug appeared impossible to me. Bart then offered a lot of help with testing many patches, providing hundreds of megs of traces, so that I could finally fix the issue caused by a nasty race condition. I really appreciate it when users with extreme loads accept to take traces in production, with all the risks that this practise implies. Sometimes it's the only way to get a bug fixed._Thanks Bart!_.  
Since [other minor fixes and enhancements](download/1.3/src/CHANGELOG-1.3.17) were pending, I released **[1.3.17](download/1.3/src/)**, which users of 1.3.16 are invited to upgrade to.

**March 22th, 2009** : _1.3.16 !_

Minor fixes and enhancements have been added since the second release candidate.

So, that's it, **[1.3.16](download/1.3/src/)** is out and marks the new official stable release.

As it has already received long testing from major users, I'm not worried about its stability, eventhough I expect that a few bugs will surface.

Further development will continue in a new branch, and 1.3 will only receive fixes and minor enhancements.

**March 10th, 2009** : _1.3.16 is getting closer !_

Second release candidate of **[1.3.16](download/1.3/src/Beta/)** has been published. It brings a lot of new long-awaited features, among which TCP splicing support, conditional redirection, TCP content filtering, session rate reporting and limiting, invalid request/response capture, binding to specific network interfaces, per-process affinity for frontends and backends, a monotonic internal clock, and many other features.  
The internals have finally been reworked in layers so that forwarding can be processed without waking high levels up. HTTP is now on top of TCP and not a special case of it. A big advantage of these changes is that we can now touch the socket code without impacting HTTP and vice-versa, which had not yet been possible till there. This means that the risk of future regressions caused by feature additions will be significantly lowered. Thanks to these changes, a lot of complex tricks and specific cases are now handled more cleanly and in a more evolutive manner. New work on keep-alive, SSL integration and QoS will be easier.  
Once 1.3.16 is out, branch 1.3 will become the new stable branch, and support for 1.2 as well as 1.3.14 and 1.3.15 will slowly phase out.

**March 9th, 2009**

Several minor bug fixes were pending since 1.3.15.7, so it was time to release **[1.3.15.8 and 1.3.14.12](download/1.3/src/)**.

Those bugs are not stability bugs, rather load-time bugs (config parsing, etc...).

Only one of them really justifies updating : if your configuration uses the **"track"** keyword in order to synchronize multiple servers states, the time taken to synchronize them grows with the number of servers.

Among the changes, a backport of the doc updates was merged, covering the log format, so that the old docs should normally not be needed anymore.

**December 4th, 2008**

Kai Krueger reported a nasty problem he encountered and analyzed.

When a server goes down, it requeues all of its connections waiting in the queue into the global queue.

But when a session completes after that, haproxy checks if there are pending connections that this server can handle, without taking into account the fact that the server is dead.

So the server can progressively suck all pending connections from the global queue just after it has been marked down.

Yes, I know, this is stupid.

A check has been added so that it does not dequeue global connections when it's marked down, and releases **[1.3.15.7 and 1.3.14.11](download/1.3/src/)** have been issued.

There are very few setups which will trigger this problem, however it's quite annoying for those experiencing it.

**October 12th, 2008**

Once in a while, a user reports that some old processes remain present after a soft-restart.

I could never reproduce the issue until Manuel Soto sent me a truss output of a configuration with which the problem reproduces frequently.

The cause is finally that haproxy still binds listening addresses to disabled instances, but does not try to stop them and refuses to exit as long as they remain present.

I took the opportunity to fix a related problem causing warnings to be emitted when haproxy tried to stop backends, and a segfault in the configuration parser if ACLs were declared in a defaults section.

That was enough to release **[1.3.15.5 and 1.3.14.9](download/1.3/src/)**.

I recommend that any user of 1.3.14 or 1.3.15 upgrades, as these fixes present very minor risk and fix really annoying problems.

**September 14th, 2008**

Several users reported on [the mailing list](http://www.formilux.org/archives/haproxy/0809/date.html) that they were experiencing abnormal concurrent connection counts higher than the maxconn they configured.

They were very prompt to send me configurations and screenshots of the stats report [showing the problem](http://skitch.com/signalmark/i5j1/haproxy-maxconn-bug).

It was indeed a bug triggered every time a connection attempt to a server failed.

I've fixed it along with another minor one, and released **[1.3.15.4 and 1.3.14.8](download/1.3/src/)**.

Mongrel users are particularly exposed because they run with **maxconn=1** and the server cannot accept more connections, so users may experience occasional errors when a server starts to reject connections.

It would also be interesting to find why some connections fail to the servers.

**September 3rd, 2008**

A cool video demonstration of the **connection regulation mechanism** (maxconn) [has been posted on 37signals](http://www.37signals.com/svn/posts/1073-nuts-bolts-haproxy).

It's clearly explained and explicit enough for people not much aware of the mechanism to understand it.

Check it there, it's not too long and really worth seeing.

**September 2nd, 2008**

While working on haproxy 1.3.16, I came across a few bugs in the code, so I issued **[1.3.15.3 and 1.3.14.7](download/1.3/src/)**.

The only one annoying concerns 1.3.15 for people who use the "balance url\_param ... check\_post" construct to hash on parameters present in POST requests.

There is a risk of crashing (but no server compromission though) with some invalid requests.

Fortunately, this feature is very new and ver limited to niche users, but it needed a quick fix anyway.

Other bugs are pretty minor and most of them concern small issues with how timeouts are handled.

**July 20th, 2008** : _two lines..._

Two lines...

That's all what is needed with the new TCP content inspection system to stop half of the spams I got home.

One of my major customers who uses HAProxy a lot has sponsored the development of some preliminary content inspection which is used to decide whether to forward a connection or not.

The very first usage of this feature consists in checking that only SSL is spoken on a connection.

But most likely more protocols will come soon.

As a nice side effect, I could now add a delay before the HELO message of my SMTP server, and reject all robots which talk first (forbidden).

And since many spam bots have small timeout values, many of them abort before the timeout is reached, resulting in my incoming spam rate dropping from about 300/hour to "only" 150/hour.

Those who keep up with the time out slow down due to limited resources.

The small addition simply consists in adding those two lines in the frontend :

		tcp-request inspect-delay  35s
		tcp-request content reject if REQ\_CONTENT

**June 21th, 2008**

**[haproxy versions 1.3.15.2 and 1.3.14.6](download/1.3/src/)** have been released to fix a major bug in request queue handling.

The problem was that due to a design problem, it was possible for new requests to be immediately served by a server before a request in queue would be served.

That caused some requests to remain in queue until they reached the queue timeout, after which either they would eventually be served, or return a 503 error code to the client.

Since it was a design problem, it took a lot of time analyzing the root cause and finding a solution.

However, as a positive side effect, the fix now makes the redispatch option work for requests which overflow a queue.

That way, clients do not get a 503 error anymore but can be served by another server (which was the purpose of the redispatch option.

Note that it is possible that 1.2 is also affected by the issue since some parts of the faulty code have not changed since.

But it is very hard to determine if it is faulty or not, and backporting the fix would take even more time.

Maybe I will eventually take a look at it if people complain about the issue.

Update (2008/06/28): Alexander Staubo, who first [noticed the problem](http://affectioncode.wordpress.com/2008/06/11/comparing-nginx-and-haproxy-for-web-applications/), has run [a new series of tests](http://affectioncode.wordpress.com/2008/06/28/another-comparison-of-haproxy-and-nginx/) showing that the problem is definitely fixed.

It also demonstrates the very nice positive effect of running with **maxconn 1** with Rails servers.

**May 25th, 2008**

Released **[haproxy versions 1.3.15.1 and 1.3.14.5](download/1.3/src/)** with minor fixes : build fix for GCC 4.3, fix for early truncate of stats output in certain circumstances, and better handling of large amounts of highly active sockets.

I indeed discovered during testing that the **sepoll** poller was so much efficient that when running at gigabit speed with 80000 active sockets fighting for their CPU share, almost all of them were running in speculative mode, causing starvation of the remaining ones, which in turn caused the accept() call to be very rarely called.

Delays of about 40 seconds have been observed on a 3.4 GHz Pentium 4 to get the stats page under such a load.

The other pollers were not better BTW.

The fix consisted in ensuring that polled events are checked at much often as the speculative ones.

With this fix, the stats page responds in less than one second on such a saturated machine.

There is still room for improvement relying on events prioritization though.

Version 1.3.15 has been promoted as the recommended one since there has been no regression report.

Version 1.2.18 was also released for users of 1.2 which experienced trouble building on BSD.

**April 19th, 2008**

Released **[haproxy version 1.3.15](download/1.3/src/)** with many new features.

The most important changes are stats updates (HTTP and UNIX), enhancements of server checks such as tracking and dynamic intervals, addition of the leastconn load-balancing algorithm, a fully transparent mode on Linux, better handling of connection failures (dead server avoidance and turn-around state), support for inter-site off-loading through redirects, updates to the build process, and large documentation updates.

For more information, please check the [ChangeLog](download/1.3/src/CHANGELOG).

Due to the important number of changes, upgrade from earlier versions should be performed with a bit of care.

Once again, a lot of code comes from contributions.

I'd like to specially thank _Krzysztof Oledzki_ for a lot of useful contributions, including the **SNMP agent**, and the guys at _Nokia_ for the good work they have done on **POST parameter hashing**.

**March 30th, 2008**

I finally assembled my new machines and installed the donated 10-Gig Myricom NICs.

I ran a few benchmarks.

Result: **[new bandwidth records set for HAPoxy: 9.897 Gbps and 35128 hits/s!](/10g.html)** It's possibly the highest bitrate achieved to date with an opensource load-balancer!

BTW, even most commercial ones are commonly limited to 4 Gbps by hardware design.

What's a bit frustrating for a precision-tweaker like me is that those NICs work out-of-the box on dirt cheap hardware, there's almost no joy passing beyond the first 4 Gbps :-)

[![](img/10gesm.jpg)](img/10ge.jpg)  

**March 8th, 2008**

Released **[haproxy maintenance version 1.3.14.3](download/1.3/src/)** to address several minor bugs and clean up the configuration manual a little bit.

One annoying issue with backup servers in round robin mode was fixed.

Nothing really important was changed in this version, this makes it a good candidate for distro updates.

**February 23rd, 2008**

I finally decided to buy an expensive motherboard to upgrade my PC in order to begin testing with the 10Gig NICs.

I selected an Asus P5E3-WS Pro because I needed PCI-X slots for my older cards.

I've put a Core2 Duo E8200 (45nm) because I wanted a lot of silence.

The mobo has 2 PCI-E 16x slots, which made it possible for me to run a back-to-back test between two 10Gig NICs.

Since the board does not support PCI graphics cards, I had to boot on serial port (the only VGA card I've got running on this mobo was a cheap crappy GeForce 8400 GS which does not work under X).

Well, my first test is quite encouraging : I can achieve 10 Gbps of HTTP traffic between the two NICs with the server and client on the same machine, which means that the hardware will be able to support haproxy under the same conditions.

I tried with client + haproxy + server but the bit rate diminished to about 6-7 Gbps.

I'm impatient to buy the 3 other mobos to build a full lab.

I will mix 2 Athlons and one C2D so that I can experiment which one is better for which type of traffic.

Stay tuned!

**January 21th, 2008**

Released **[haproxy maintenance version 1.3.14.2](download/1.3/src/)** to address several minor bugs as well as a major one affecting Linux 2.6 users with the sepoll poller, which can result in truncated responses if the client closes the connection before the server completes its response.

Note that version 1.3.13.2 was released too with those bugs fixed.

The GNU Makefile was crappy and caused trouble in some build environments.

It has been rewritten in a more flexible manner, while still providing full variable compatibility with existing build systems.

Distribution packagers are encouraged to migrate over to this one.

The **[new configuration manual](download/1.3/doc/configuration.txt)** is almost finished.

All keywords and all their options have been documented.

Only the logs section remains to be completed.

This version has been merged with 1.3.14.2.

Some minor robustness and performance tuning parameters have been added, mostly timeouts and backlog.

**January 13th, 2008**

Worked all the day both in kernel and haproxy to get full transparent proxy to work on Linux.

Now, with a small kernel patch, it's possible for haproxy to become completely transparent and just appear as a router, without touching either source nor destination addresses and ports.

And all this without NAT, at the same performance level as in normal proxy mode.

This will be great for people looking for SMTP/HTTPS/FTP relaying and load balancing.

I'm even planning on installing it on my firewall ;-) Stay tuned for the updates, I will soon post the patches once cleaned up.

**December 12th, 2007** : _Santa Claus left a present for me at EXOSEC !_

Some of you might have already got their hands on this.

For those who don't know yet, this [beautiful piece of art](img/10geart.jpg) is a **10 Gbps Ethernet NIC** from **[_Myricom_](http://myri.com/)**.

For a long time, I had been tempted by their legendary high performance network cards, which were said everywhere to be able to **saturate a 10 Gig wire** under Linux without putting too much stress on the CPU, using a mainstream opensource driver, and without resorting to dirty tricks such as TOE.

What would a performance addict like me need more ?

I finally decided to mail these guys and described how I'm currently used to benchmark HAproxy with aggregated Gigabit NICs, with a minimum of 4 NICs in a setup (_1 for the client, 2 for the proxy, 1 for the server_).

4 hours later, when I woke up, I had a mail from **Charles Seitz, Myricom's CEO**.

He explained to me that he was pleased to offer me 4 NICs with cables, **plus one spare of each** just in case, as their contribution to the project... yes, I'm talking about **a donation of five 10Gig NICs!** That's awsome!

And if it would not be enough for some of you to find them really cool, he also provided me with french-speaking contacts, free access to their support and [important advices for the choice of motherboards](http://www.myri.com/scs/performance/PCIe_motherboards/) to get the best out of those wonderful NICs!

I don't even know the polite words to say in such circumstances :-)

Today I've been monitoring the shipping steps at [UPS](http://www.ups.com/).

This evening, I noticed that they arrived at [EXOSEC](http://www.exosec.fr/).

After leaving the customer's, I went back there to find this big parcel on my desk, with its contents very carefully packed.

I must say that I was both very excited and extremely careful while opening the packaging.

The first thing I noticed after extracting the first NIC from its packaging was that it had a very clean design, as can be seen on [this photo](img/10geclean.jpg).

They are also **very thin** as shown on the [picture on the right](img/10gethin.jpg), so there will be no problem putting two of them side-by-side in the proxy.

The [CX4 connector](img/10gecx4.jpg) looks a bit fragile, but careful manipulation is the minimal requirement to use the highest speed standard Ethernet.

From what I understood, this is the same connector as used on Infiniband, except that 10GE has [terminators on the board](img/10geterm.jpg).

Well, obviously, there are very nice companies out there who deserve to be talked about!

Their very generous support to open source projects leaves many others far behind.

People say that Santa Claus lives in the North Pole, but now I know he lives in Arcadia in California :-)

**Thank you very much Charles, thanks very much Myricom.** Be sure to read about my first test results here.

[![](img/10gesm.jpg)](img/10ge.jpg)  
[![](img/10geartsm.jpg)](img/10geart.jpg)  
[![](img/10gethinsm.jpg)](img/10gethin.jpg) [![](img/10gecx4sm.jpg)](img/10gecx4.jpg)  

**December 6th, 2007**

Released **[haproxy version 1.3.14](download/1.3/src/)**.

A good part of the changes comes from nice contributors of the [mailing list](https://www.mail-archive.com/haproxy@formilux.org/).

Most sensible changes include support for dynamic server weights offering support for slow start and graceful shutdown.

The load balancer is now able to report its servers state to outer components, enabling the building of more complex multi-site architectures involving dynamic routing protocols such as BGP.

People who were complaining about the rough configuration, rough statistics, or lack of logging to UNIX sockets, should really give this one a try.

Rate of changes after this version should significantly drop in order to progressively switch the tree to a stable state.

**October 18th, 2007**

Released **[haproxy maintenance version 1.3.12.3](download/1.3/src/)** and **[new version 1.3.13](download/1.3/src/)**.

Thanks to quite a bunch of subscribers of the new [mailing list](https://www.mail-archive.com/haproxy@formilux.org/), several nasty bugs have been ironed out and a handful of smart features have been added.

The most visible add-ons are the UNIX socket to access the statistics page, and the support for [Doug Lea's dlmalloc](http://gee.cs.oswego.edu/pub/misc/malloc.c) which dramatically reduces memory usage during soft-reconfigurations.

**September 22th, 2007**

The long awaited [haproxy mailing list](https://www.mail-archive.com/haproxy@formilux.org/) is finally there !

Special thanks to my friend [Benoit](http://bdolez.free.fr/) who has spent some time setting it up on our [Formilux server](http://www.formilux.org/).

For more info on how to subscribe, please check the [Contacts](/#tact) entry at the bottom of the [home page](/).

**September 20th, 2007**

Released **[haproxy version 1.3.12.2](download/1.3/src/)**.

It fixes several bugs affecting timeouts and retry counts when configs are split between frontends and backends.

Some sanity checks on the configuration file were never executed, causing some erroneous configurations to be accepted without being fixed.

Last, the license has been clarified in a few files from O'Reilly.

All in all, it seems like keeping a supported version is already starting to pay off, as people are looking for something **stable** and report bugs very quickly.

**_All version 1.3 users are encouraged to upgrade to 1.3.12.2_**.

**September 5th, 2007**

Released **[haproxy version 1.3.12.1](download/1.3/src/)**.

It fixes a few bugs discovered in 1.3.12, notably one which could lead to crashes under Linux with speculative I/O when clients disconnect before the connection has been established to the server.

As a workaround, it is possible to specify "**nosepoll**" in the "**global**" section.

A "**stats refresh <interval>**" option has also been added because some people like to have the stats page automatically refresh.

It's also possible to hide all failed servers on the stats page now.

This version also contains the **[new configuration manual](download/1.3/doc/configuration.txt)** which has just been started but which helps understand how to use ACL.

**July 15th, 2007**

Started writing the new **[Configuration Manual](download/1.3/doc/configuration.txt)**.

It enumerates all configuration keywords and in what context they may be used.

It also includes a few examples of ACLs.

It is not finished yet, but I decided to publish it because people have really no other valuable sources of information to use content switching.

It only covers version 1.3.12, and updates will only cover the latest version, making it far more readable.

Please take a look at it and start from the examples in the examples/ directory from the sources.

Any feedback is welcome :-)

**June 17th, 2007**

Released **[haproxy version 1.3.12](download/1.3/src/)**.

It completes integration of ACL with Content Switching, and allows you to customize your error responses.

Except for the ACL and a few bugs, there have been few changes since 1.3.11.4, and I intend to support 1.3.12 during development and cleanups of the next versions which may not be as reliable.

Several big content providers use 1.3 to regulate the traffic to/from their web servers, and there is a real demand for a stable version with the new features and performance of 1.3.

And considering that some of them even pay for this, I understand they want something really reliable.

**June 3rd, 2007**

Released **[haproxy version 1.3.11.4](download/1.3/src/)**.

It fixes 2 long-standing bugs in timeout handling, which could sometimes cause 100% CPU usage during several seconds when a client had closed its write channel.

Some small improvements to the I/O subsystem should save some CPU cycles on high bandwidth sites.

It is now possible to finely tune the pollers for reduced latency.

**May 14th, 2007**

Released **[haproxy version 1.3.11.3](download/1.3/src/)**.

It fixes the (hopefully) last bug affecting Linux users with speculative I/O processing, introduced in 1.3.9.

This bug was also causing random timeouts.

Do not use versions 1.3.11 to 1.3.11.2 as they are all broken.

New in this release are a better timer management and a new memory manager which is able to self-manage its pools and free unused ones when memory is becoming scarce.

It is also easier to code with this new one since it's not necessary anymore to declare pool sizes.

Overall, yet another performance boost of 5% has been gained.

**May 10th, 2007**

Released **[haproxy version 1.3.10.2](download/1.3/src/)** to fix build on OpenBSD.

**May 9th, 2007**

Released **[haproxy version 1.3.10.1](download/1.3/src/)**.

It fixes a serious bug affecting Linux users with speculative I/O processing, introduced in 1.3.9.

This bug was causing random timeouts on some traffic patterns, mostly noticeable in TCP mode but almost certainly in HTTP too.

All Linux users of 1.3.9 and 1.3.10 should either upgrade or disable speculative I/O as a workaround, by starting haproxy with the **\-ds** argument or by setting **nosepoll** in the **global** section.

**May 9th, 2007**

Released **[haproxy version 1.3.10](download/1.3/src/)**.

This one adds ACL, SMTP health checks (thanks to Peter van Dijk), and URI hashing (thanks to Guillaume Dallaire).

Also, the rbtree was replaced with a much faster tree, leading to an overall performance boost around 5%.

The speculative I/O processing in 1.3.9 has introduced some bugs which have been fixed in this version.

I feel confident that latest changes have brought their pile of bugs too.

I will probably spend some time soon to do cleanup and stabilization work, eventhough both are not really compatible.

I also want to **thank all the people who contribute** code and testing.

You are more and more at each release.

I'm impatient to clean up the remains of the old code, so that even more people can contribute code.

Interestingly, all contributions till now were of high quality.

This is probably induced by some sort of selection caused by the technical aspect of the product, and the skills required to use the development version.

_Thanks again to you all !_

**Apr 22th, 2007**

Done a quick benchmark at [EXOSEC](http://www.exosec.fr/) with [haproxy 1.3.9](download/1.3/src/) running on a nice single-core system equipped with many PCI-Express Gigabit NICs.

The [graph](/#benchmark) shows pretty decent results !

**Apr 15th, 2007**

Released **[haproxy version 1.3.9](download/1.3/src/)**.

This one adds modularization to the pollers, which made it possible for me to finally implement **support for FreeBSD kqueue()**.

I'd like to thank Olivier Warin for providing me a FreeBSD account during this development.

A new concept was introduced too : **speculative I/O**.

It is a new method consisting in reducing the number of calls to the expensive epoll\_ctl() and epoll\_wait() by attempting to access the file descriptors before being notified about their readiness.

This provides an **overall speed boost of 10%**, which is quite much for just a poller.

**Apr 3rd, 2007**

Released **[haproxy version 1.3.8.2](download/1.3/src/)** to fix a minor and a major bug.

The minor bug caused the response rewrite to fail on the status line.

The major bug which was introduced in **1.3.6** could cause **the process to crash** in some circumstances when rewriting the request line (method and/or URI).

**All users of 1.3.6 and later must upgrade**.

**Apr 1st, 2007**

Released **[haproxy version 1.3.8.1](download/1.3/src/)** to fix very minor bugs, and slightly improve performance.

Request headers were not added if option httpclose was not set.

Bruno Michel contributed a [VIM script](download/contrib/) for syntax color highlighting.

**Mar 25th, 2007**

Released **[haproxy version 1.3.8](download/1.3/src/)**.

Several bugs which might have caused crashes on erroneous configurations have been fixed.

The response processing is now completed, which means that real configurations can now be written ; HAProxy 1.3.8 now is at least equivalent to 1.2.17 in terms of features.

Just like with every release, several code optimization have led to small but noticeable performance increases, particularly on very high data bandwidth.

The configuration errors are handled more gracefully now with indications about what failed and hints to resolve the issue.

HAProxy now builds on MacOS 10.4 thanks to Dan Zinngrabe who provided a makefile.

Also, it is now possible to send health checks to an alternate server address, thanks to a patch from Fabrice Dulaunoy.

Users of 1.3 are encouraged to upgrade to 1.3.8 as it both fixes known bugs and converges towards something less tricky than previous versions.

**Mar 17th, 2007**

Released **[haproxy version 1.2.17](download/1.2/src/)**.

I have backported Sin Yu's **rbtree scheduler** from version 1.3 since it proved to be stable.

A few minor bugs were fixed, and two useful contributions were merged : support for user and group keywords as alternatives to numerical uid and gid from Marcus Rueckert, and the ability to prevent some source addresses from appearing in the X-Forwarded-For header, which is useful when combined with Stunnel for instance (patch from Bryan Germann).

Thanks to both of them, contribs are always welcome !

The [architecture manual](download/1.2/doc/) was updated to reflect new features in branch 1.2, with examples for stunnel and for load mitigation.

Users of 1.2.16 with high loads are encouraged to upgrade to 1.2.17 as it offers them the high performance of branch 1.3 with the reliability of the stable branch 1.2.

**Jan 27th, 2007**

Released **[haproxy version 1.3.7](download/1.3/src/)**.

I found a **critical bug** in the new parser in development branch, causing crashes when an empty header is passed.

This was caused by a missing pointer assignment in the empty header processing path.

All 1.3.6 users MUST upgrade to 1.3.7.

**Jan 22th, 2007**

Released **haproxy version 1.3.6**.

I spent a long time reworking the **HTTP message parser**.

It now consists in a **carefully hand-optimized 28-states FSM**.

The new code will look awful to _goto_ haters, and will please FSM lovers.

It's blazingly fast : parsing and indexing all of the 660 bytes of an HTTP request from _Firefox_ on [Freshmeat](http://freshmeat.net/) only takes 1.94 **microsecond** on my 1.7 GHz Pentium-M notebook, which means it can do it more than **500000 times a second!**

The request code has been cleaned up a lot and adapted to this new FSM.

Adding layer7 rules based on new criteria is now trivial.

The response code will be ported next, but the code was so much cleaner and faster that it was worth releasing one version before breaking everything.

Several bugs were fixed since 1.3.5.

I really consider **1.3.6** as the **most likely reliable** 1.3 release to date.

**Jan 7th, 2007**

In order to support the new **[Linux Layer7 Switching project](http://linux-l7sw.sf.net/)**, I have implemented support for **kernel TCP splicing** using Alexandre Cassen's library.

This is still experimental but already works remarkably well.

On my notebook at 400 Mbps, haproxy's usage goes down from 65% to 5-10%.

I have written [some doc](/download/1.3/doc/tcp-splicing.txt) explaining how to setup up TCP splicing, with [an example](/download/1.3/test/tcp-splicing-sample.cfg).

Since the original code was provided for Linux kernel 2.6.19 only, I have backported the patches to kernel [2.6.16](/download/patches/tcp_splice-0.1.1-linux-2.6.16.diff) and [2.4.33](/download/patches/tcp_splice-0.1.1-linux-2.4.33.diff).

The second great news is that Sin Yu has provided me with a useful patch for the second time : the **task scheduler** is now based on an **rbtree** and not on the dirty old dual-linked list anymore.

It means that people who had performance problems and who had to set all their timeouts to the same value as a workaround will not have to do this anymore.

I have tested, and the code works like a charm !

Thanks again Sin !

**Jan 2nd, 2007**

After about 4500 new lines of code and some useful feedback from a bunch of brave beta-testers, I'm pleased to announce **[haproxy version 1.3.4](download/1.3/src/)** with the new **Content-Switching features !!!**

It is now possible to select a **backend** (_server pool + load balancing algo_) depending on any parameter in the request, such as **any part of the URI**, the **host name**, etc....

As of now, I've merged Sin Yu's patch to permit switching based on a request regex, but the framework is ready to accept many other criteria.

The HTTP request parser has been completely rewritten to support unlimited header inspection, and the statistics page has been rewritten, as can be seen [on the demo page](http://demo.haproxy.org/).

It is far from being finished right now, but it seems pretty usable.

The server state machine should be adapted though.

There is still no doc, so please note that old configurations do still work, and that in order to switch from an instance to another backend, you need to use "reqisetbe <regex> <new\_proxy>".

Also, there's [a config example here](download/1.3/test/) that will be worth any doc.

**Dec 5th, 2006**

The [load balancing article](http://1wt.eu/articles/2006_lb/) has been linked to from [LinuxFR](http://linuxfr.org/pub/).

The small 128 kbps uplink is currently running at full speed but the site is still responding thanks to haproxy queuing the connections to smoothen the traffic.

Next time, I should also write an article on setting up the QoS with tc, because typing remotely with SSH is still very responsive under full load :-)

**Jul 4th, 2006**

Opened **development branch 1.3**, which started with a major cleanup.

Not sure yet about all features which will be merged, the first step is to clean up the code and make it modular.

The API's licence has been switched to **LGPL** in order to later allow linking with binary external modules developped for applications covered by NDAs for example.

Version 1.3.0 is exactly the same as 1.2.14+bugfixes so it is a stable starting point.

It is [available here](download/1.3/src).

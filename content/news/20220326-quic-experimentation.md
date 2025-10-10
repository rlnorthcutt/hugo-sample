---
title: "QUIC experimentation"
date: 2022-03-26
---
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

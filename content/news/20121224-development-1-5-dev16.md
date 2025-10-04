---
title: "Development 1.5-dev16"
date: 2012-12-24
---

Here comes **1.5-dev16**. Thanks to the amazing work Sander Klein and John Rood have done at [Picturae ICT](http://picturae.com/) we could finally spot the freeze bug after one week of restless digging ! This bug was amazingly hard to reproduce in general and would only affect POST requests under certain circumstances that I never could reproduce despite many efforts. It is likely that other users were affected too but did not notice it because end users did not complain (I'm thinking about webmail and file sharing environments for example). During this week of code review and testing, around 10 other minor to medium bugs related to the polling changes could be fixed.

Another nasty bug was fixed on SSL. It happens that OpenSSL maintains a global error stack that must constantly be flushed (surely they never heard how errno works). The result is that some SSL errors could cause another SSL session to break as a side effect of this error. This issue was reported by J. Maurice (wiz technologies) who first encountered it when playing with the tests on [ssllabs.com](http://www.ssllabs.com/).

Another bug present since 1.4 concerns the premature close of the response when the server responds before the end of a POST upload. This happens when the server responds with a redirect or with a 401, sometimes the client would not get the response. This has been fixed.

Krzysztof Rutecki reported some issues on client certificate checks, because the check for the presence of the certificate applies to the connection and not just to the session. So this does not match upon session resumption. Thus another ssl\_c\_used ACL was added to check for such sessions.

Among the other nice additions, it is now possible to log the result of any sample fetch method using "%\[\]". This allows to log SSL certificates for example. And similarly, passing such information to HTTP headers was implemented too, as "http-request add-header" and "http-request set-header", using the same format as the logs. This also becomes useful for combining headers !

Some people have been asking for logging the amount of uploaded data from the client to the server, so this is now available as the "%U" log-format tag. Some other log-format tags were deprecated and replaced with easier to remind ones. The old ones still work but emit a warning suggesting the replacement.

And last, the stats HTML version was improved to present detailed information using hover tips instead of title attributes, allowing multi-line details on the page. The result is nicer, more readable and more complete, as can be seen on the [demo page](http://demo.haproxy.org/).

All 1.5-dev users are then encouraged to upgrade to [dev16](/download/1.5/src/). **Update:** minor last-minute regression on the stats page, please use the [latest snapshot](/download/1.5/src/snapshot/) instead.

---
title: "Development 1.5-dev12 with SSL!!!"
date: 2012-09-10
---

The main, long-awaited, feature this time is **native SSL** support on both sides, with **SNI** and **multi-process session sharing**. The work took several months to be done at [Exceliance](http://www.exceliance.fr/en/) because it required a major rewrite of the lower connection layers in order to support multiple data layers. This was a very painful task, but doing so allowed us to shrink the SSL patch from several thousands of lines of hardly maintainable code to a few hundreds of SSL-specific code. The code supports the Server Name Indication TLS extension (SNI), which consists in presenting the certificate which matches the host name requested by the client. This also works with wildcard certificates, of course. The certificates can be loaded from a directory, which makes it more convenient to load hundreds or thousands at a time. And since they are loaded into a binary tree, there is no lookup overhead even if there are hundreds of thousands, which is very convenient for massive hosting providers.

In current state, the code does not yet support checking certificates, which also means that connecting to an SSL server is only useful if the LAN is safe (in short, it's only useful if the server absolutely wants to get the connection to port 443). But the Exceliance team is actively working on this.

We took care of correctly arranging connection and data layers. Right now it's perfectly possible to chain multiple layers of haproxy servers to offload more SSL, using SSL-ID affinity and the PROXY protocol in order not to lose the client's source address. Doing this with off-the shelf hardware can result in quite a cheap SSL offloader even for huge loads. We measured 4000 TPS on SSLv3 on an Atom D510 and have not yet run the tests on larger hardware.

Among the other features in this version, we can list IPv6 transparent mode, "base" pattern/acl to match a concatenation of the Host header and the URI, "urlp\_val" ACL to match a URL parameter's value, support for the "nice" keyword on "bind" lines to change the priority of sessions using this bind line (useful to limit SSL CPU impact), the ability to clear/feed stick-table entries on the stats CLI (which got lost forgotten in a dead branch), and the usual set of halog features and optims.

The [changelog](/download/1.5/src/CHANGELOG) is available for more information, though there are a lot of commits to transform the connection layers. Users who need SSL should really [give it a try](/download/1.5/src/). While we got a number of useful reports on the mailing list and could fix some issues, it is very likely that some bugs remain, so if you observe abnormal behaviours, please report your experiences there.

On the stable branch side, [1.4.22](/download/1.4/src/) was silently released one month ago with a number of small fixes and a number of minor feature improvements, such as the ability for putting a server in soft-stop mode from the stats web page in admin mode, and support for the "httponly" and "secure" flags on cookies.

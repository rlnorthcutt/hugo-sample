---
title: "Year of a changing Web"
date: 2015-01-01
---
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

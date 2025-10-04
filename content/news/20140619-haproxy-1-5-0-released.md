---
title: "HAProxy 1.5.0 released!"
date: 2014-06-19
---

After 4 years of hard work, **HAProxy 1.5.0 is finally released!**

For people who don't follow the development versions, 1.5 expands 1.4 with many new features and performance improvements, including **native SSL** support on both sides with SNI/NPN/ALPN and OCSP stapling, **IPv6** and UNIX sockets are supported everywhere, **full HTTP keep-alive** for better support of NTLM and improved efficiency in static farms, **HTTP/1.1 compression** (deflate, gzip) to save bandwidth, **PROXY protocol** versions 1 and 2 on both sides, **data sampling** on everything in request or response, including payload, **ACLs** can use any matching method with any input sample **maps** and dynamic ACLs **updatable** from the CLI **stick-tables** support counters to track activity on any input sample **custom format** for logs, unique-id, header rewriting, and redirects, **improved health** checks (SSL, scripted TCP, check agent, ...), **much more scalable** configuration supports hundreds of thousands of backends and certificates without sweating.

Since dev26, a few bugs were fixed, and some low-importance things were integrated. Basic OCSP stapling support from Dirkjan and Emeric was finally merged. Sasha's header replace actions were merged as well. I've added a few more info in the stats page (avg response times) and CSV output (health check status), added support for PROXY v2 on the accept side, and added the "capture" action on tcp-request in order to log contents such as SNI or payload. Rémi's dh-param was finally integrated.

People love numbers, so here are a few. From 1.4.0 to 1.5.0, we had :

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

Don't forget to offer a beer to your **distro packagers** who make your life easier. It's hard to list them all, but if you don't build from sources, you're likely running a package made and maintained by one of these people :

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

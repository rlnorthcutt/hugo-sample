---
title: "Santa Claus left a present for me at EXOSEC !"
date: 2007-12-12
---

Some of you might have already got their hands on this. For those who don't know yet, this [beautiful piece of art](img/10geart.jpg) is a **10 Gbps Ethernet NIC** from **[_Myricom_](http://myri.com/)**. For a long time, I had been tempted by their legendary high performance network cards, which were said everywhere to be able to **saturate a 10 Gig wire** under Linux without putting too much stress on the CPU, using a mainstream opensource driver, and without resorting to dirty tricks such as TOE. What would a performance addict like me need more ?

I finally decided to mail these guys and described how I'm currently used to benchmark HAproxy with aggregated Gigabit NICs, with a minimum of 4 NICs in a setup (_1 for the client, 2 for the proxy, 1 for the server_). 4 hours later, when I woke up, I had a mail from **Charles Seitz, Myricom's CEO**. He explained to me that he was pleased to offer me 4 NICs with cables, **plus one spare of each** just in case, as their contribution to the project... yes, I'm talking about **a donation of five 10Gig NICs!** That's awsome! And if it would not be enough for some of you to find them really cool, he also provided me with french-speaking contacts, free access to their support and [important advices for the choice of motherboards](http://www.myri.com/scs/performance/PCIe_motherboards/) to get the best out of those wonderful NICs! I don't even know the polite words to say in such circumstances :-)

Today I've been monitoring the shipping steps at [UPS](http://www.ups.com/). This evening, I noticed that they arrived at [EXOSEC](http://www.exosec.fr/). After leaving the customer's, I went back there to find this big parcel on my desk, with its contents very carefully packed. I must say that I was both very excited and extremely careful while opening the packaging.

The first thing I noticed after extracting the first NIC from its packaging was that it had a very clean design, as can be seen on [this photo](img/10geclean.jpg). They are also **very thin** as shown on the [picture on the right](img/10gethin.jpg), so there will be no problem putting two of them side-by-side in the proxy.

The [CX4 connector](img/10gecx4.jpg) looks a bit fragile, but careful manipulation is the minimal requirement to use the highest speed standard Ethernet. From what I understood, this is the same connector as used on Infiniband, except that 10GE has [terminators on the board](img/10geterm.jpg).

Well, obviously, there are very nice companies out there who deserve to be talked about! Their very generous support to open source projects leaves many others far behind. People say that Santa Claus lives in the North Pole, but now I know he lives in Arcadia in California :-)

**Thank you very much Charles, thanks very much Myricom.** Be sure to read about my first test results here.

[![](img/10gesm.jpg)](img/10ge.jpg)  
[![](img/10geartsm.jpg)](img/10geart.jpg)  
[![](img/10gethinsm.jpg)](img/10gethin.jpg) [![](img/10gecx4sm.jpg)](img/10gecx4.jpg)

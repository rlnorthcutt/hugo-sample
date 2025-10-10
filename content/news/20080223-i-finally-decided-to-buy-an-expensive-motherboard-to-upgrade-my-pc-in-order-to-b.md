---
title: "I finally decided to buy an expensive motherboard to upgrade my PC in order to begin testing with the 10Gig NICs."
date: 2008-02-23
---
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

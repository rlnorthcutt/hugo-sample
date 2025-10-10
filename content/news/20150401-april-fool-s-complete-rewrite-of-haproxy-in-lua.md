---
title: "April Fool's: Complete rewrite of HAProxy in Lua"
date: 2015-04-01
---
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

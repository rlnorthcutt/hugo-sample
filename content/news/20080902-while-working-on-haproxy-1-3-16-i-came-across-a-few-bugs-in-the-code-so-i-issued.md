---
title: "While working on haproxy 1.3.16, I came across a few bugs in the code, so I issued 1.3.15.3 and 1.3.14.7."
date: 2008-09-02
---

While working on haproxy 1.3.16, I came across a few bugs in the code, so I issued **[1.3.15.3 and 1.3.14.7](download/1.3/src/)**. The only one annoying concerns 1.3.15 for people who use the "balance url\_param ... check\_post" construct to hash on parameters present in POST requests. There is a risk of crashing (but no server compromission though) with some invalid requests. Fortunately, this feature is very new and ver limited to niche users, but it needed a quick fix anyway. Other bugs are pretty minor and most of them concern small issues with how timeouts are handled.

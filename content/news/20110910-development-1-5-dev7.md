---
title: "Development 1.5-dev7"
date: 2011-09-10
---

Five months have elapsed since 1.5-dev6. A [massive amount of changes](/download/1.5/src/CHANGELOG) was merged since then. Most of them were cleanups and optimizations. A number of changes were dedicated to making listeners more autonomous. The immediate effect is a more robust handling of resource saturation, and the second effect is the removal of the 10-years old maintain\_proxies() function which was harming performance and hard to get over. Halog was improved too (faster with more filters). A significant number of external contributions were merged, among them the stats socket updates to clear session-table keys by values. There are too many changes to list, but nothing too dangerous, so I'd say it's the 1.5-dev version I trust the most today. Please [give it a test](/download/1.5/src/).

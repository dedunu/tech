---
layout: post
title: Are you going to save space using Bit Data Type? - Part 2
---

[Yesterday I wrote a post with the same title](https://www.dedunu.info/2012/10/are-you-going-to-save-space-using-bit.html). In that post I mentioned using char(1) is also the same as using a one-bit column in the table. But it is from the perspective of storage space. But using numbers is less burden to the Database engine. It means using 1 and 0 is better than using ‘Y’ and ‘N’. Also in comparing data or in sorting data, it is easier.

If you are storing numbers as a text its not a good thing although you don’t do any mathematical operation with that text. The first thing it takes more space. It takes 1 byte for every character, while [integers take very less](https://www.dedunu.info/2012/10/data-type-details-from-sphelp.html). The second thing if you store them as a string it will have an extra cost to manipulate, compare, sort, whatever you are going to do with them.

### Tags

- Data Types
- English
- Char
- Architecture
- Numbers as Text
- SQL Server
- BIT

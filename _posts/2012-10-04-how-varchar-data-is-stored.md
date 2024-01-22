---
layout: post
title: "How varchar data is stored?"
---

In SQL Server we use `varchar`, `varbinary` to save disk space in our tables. But it's not saving data always as it sounds. When the data stores it takes a few extra bytes to describe the data length. Because of that, there is no gain using `varchar(2)`. If you use `varchar(2)` it will take 4 or 3 bytes to store data. `varchar(8000)` or below should have 2 Byte offset to store the variability of character count. If you are using `varchar(max)` is different. It should have 4 Bytes offset. But I’m still looking for that to confirm it takes 4 Bytes. And it is stored in Variable Column Offset Array.

More information: [http://www.sqlservercentral.com/blogs/aschenbrenner/2011/06/29/the-mystery-of-the-null-bitmap-mask/](http://www.sqlservercentral.com/blogs/aschenbrenner/2011/06/29/the-mystery-of-the-null-bitmap-mask/)

### Tags

- Data Types
- varbinary
- varchar
- Architecture
- SQL Server
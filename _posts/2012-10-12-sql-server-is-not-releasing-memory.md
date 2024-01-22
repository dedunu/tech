---
layout: post
title: "SQL Server is not releasing memory?"
---

I got a few questions to answer quickly in last week just like a test. Then I suddenly answered then after that I tried to find correct answers to them. I found answers for most of them. And one of them was there as it was.

> A Windows server has 32 GB of memory and dedicated for SQL Server database. Every time you start the server the memory utilization of SQL Server gradually increases, until it takes almost all the memory and remains there for days even when there is no database activity. What will you do ?

Actually, I answered

> We can set maximum memory limit. Some how gradually SQL Server uses available memory.

I knew that SQL Server uses and usually doesn’t release memory, although it doesn't need to use it. But I didn’t know why is that. Then I got to know that Not releasing memory is a feature of SQL Server. On servers, we don’t run our day to day applications and most of the times we have allocated separate box for SQL Server. Then nobody will use that memory. If nobody uses that why should we release and allocate again and again? When we are discussing this problem our production server had reached its maximum memory too. And this is not our production servers.

[Preethi](http://preethiviraj.blogspot.com/) told that this happens often. People who don’t know about SQL Server behaviour when saw “task manager” like above they are suggesting to double the memory of the server. Then until it takes a few days they are happy. Again they are having the same issue. Actually, it’s not a problem with SQL Server.

If you really want to release that memory you can easily restart SQL Server. Then it begins everything from the beginning. Otherwise, you can execute those commands.

*   [DBCC FREEPROCCACHE](http://msdn.microsoft.com/en-us/library/ms174283.aspx)
*   [DBCC FREESYSTEMCACHE](http://msdn.microsoft.com/en-us/library/ms178529.aspx)
*   [DBCC FREESESSIONCACHE](http://msdn.microsoft.com/en-us/library/ms187781.aspx)

But even in the TechNet, they haven’t mentioned that it is recommended running those commands against production servers. Somehow as I think theirs no need to flush memory manually. Because if you are using SQL Server on your laptop, every time that you restart your laptop it will flush again and again. In production servers, we don’t need to flush it manually. Let SQL Server use that memory as it wants.

If you are using one box to install SQL Server and Application both you can set maximum memory limit to SQL Server. Then it will not exceed that limit. But I found this thread from [SQLServerCentral](http://www.sqlservercentral.com/).

[http://www.sqlservercentral.com/Forums/Topic982342-1550-1.aspx](http://www.sqlservercentral.com/Forums/Topic982342-1550-1.aspx)

In that thread he is saying that SQL Server exceeds that maximum memory limit. But technically it should not happen. And I haven’t tested it also. But there may be a reason for that too. If you are setting maximum memory limit you should restart SQL Server. If you don’t restart it, it uses previous memory limit. Somehow below link says another thing. I have to learn about it further. 

> Yup. Perfectly normal.  
> Max server memory is the max size of the buffer pool, the memory area that contains the data cache, plan cache and a whole bunch of other caches. SQL also uses memory outside the buffer pool for things like backup buffers, thread stack, linked server drivers, CLR and a few other things. This is outside of the buffer pool, so it's not part of 'max server memory'  
> On 32-bit SQL, that's referred to as MemToLeave (memory to leave unallocated when assigning the buffer pool). On 64 bit that term has no meaning.  
> [http://www.sqlservercentral.com/Forums/Topic1197388-1550-1.aspx](http://www.sqlservercentral.com/Forums/Topic1197388-1550-1.aspx)

### Tags

- Memory
- Architecture
- SQL Server
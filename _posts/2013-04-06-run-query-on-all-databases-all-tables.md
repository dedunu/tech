---
layout: post
title: "Run query on all databases all tables at once"
---

<div dir="ltr" style="text-align: left;" trbidi="on"><a href="http://www.dedunu.info/2013/04/how-to-run-query-on-all-tables.html" target="_blank">When I was writing the previous post</a>, I was thinking about a single line statement to disable all the triggers in SQL Server instance. But after that, I found a way to how to do this. Those queries may look confusing.<br />Below query will print all the names of tables in all the databases of SQL Server instance.<br /><pre class="code"><span style="color: blue;">EXEC </span><span style="color: maroon;">sp_MSforeachdb </span><span style="color: red;">'USE [?] EXEC sp_MSforeachtable ''PRINT ''''/'''''',N''/'' '</span></pre><br />But the problem here is you have so many ‘ here. And if you want to disable all the triggers on all the databases you can use below query.<br /><pre class="code"><span style="color: blue;">EXEC </span><span style="color: maroon;">sp_MSforeachdb </span><span style="color: red;">'USE [?] EXEC sp_MSforeachtable ''ALTER TABLE / DISABLE TRIGGER ALL'',N''/'' '</span></pre><br />This query will disable all the triggers in your SQL Server Instance. But this alter statement will run on <span style="color: blue;">temp</span> database’s tables also. In <span style="color: blue;">master</span> and <span style="color: blue;">msdb</span> you don’t need to worry because all of their tables are System tables. But <span style="color: blue;">temp</span> database’s tables are user tables. So that is also not much of a worry.<br /><br />Enjoy SQL Server!</div>

### Tags

- SQL
- SQL Server 2012
- Trigger
- TSQL
- SQL Server
- SQL Sever

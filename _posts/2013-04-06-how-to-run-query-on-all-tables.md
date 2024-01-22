---
layout: post
title: How to run a query on all Tables?
---

<div dir="ltr" style="text-align: left;" trbidi="on">In some cases, people need to run some queries against all the databases in their SQL Server instance. Something very very useful for administrators. Let's say somebody wants to give read permission on all tables he can use this <span style="color: maroon;">sp_MSforeachdb </span>stored procedure.<br />But what I’m going to tell in this post is not about it. I’m going to talk about <span style="color: maroon;">sp_MSforeachtable<span style="color: #222222;">. Let’s say somebody wants to disable all the triggers of one database. Then you can use a Script like below.</span></span><br /><pre class="code"><span style="color: blue;">USE </span><span style="color: teal;">AdventureWorks2012</span><span style="color: blue;">GO<br /><br />EXEC </span><span style="color: maroon;">sp_MSforeachtable </span><span style="color: red;">'ALTER TABLE ? DISABLE TRIGGER ALL'</span><span style="color: blue;">GO</span></pre><br />But this command will not run on system tables. This is how I confirmed it.<br /><pre class="code"><span style="color: blue;">USE </span><span style="color: teal;">AdventureWorks2012</span><span style="color: blue;">GO<br /><br />EXEC </span><span style="color: maroon;">sp_MSforeachtable </span><span style="color: red;">'PRINT ''?'''</span><span style="color: blue;">GO</span></pre>You can see when you run this query on AdventureWorks database, it will print only user tables. Not on system table of that database.</div>

### Tags

- SQL
- Table
- T-SQL
- Trigger
- TSQL
- SQL Server
- SQL Sever

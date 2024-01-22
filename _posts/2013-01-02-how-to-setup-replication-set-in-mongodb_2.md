---
layout: post
title: "How to setup a replication set in MongoDB?"
---

<div dir="ltr" style="text-align: left;" trbidi="on">I just wanted to set up a replication set in MongoDB to check the behaviour of MongoDB replica set.<br />For this demonstration, I use MongoDB 2.2.0 and PowerShell 2.0. <br />First I want to create directories for MongoDB replication instances. I’m going to for a replication set with three nodes. So because of them, I need to create there MongoDB data directories.<br /><br /><span style="font-family: &quot;courier new&quot;;"><span style="color: blue;">New-Item</span> -ItemType Directory -Path \data\</span><br /><span style="font-family: &quot;courier new&quot;;"><span style="color: blue;">New-Item</span> -ItemType Directory -Path \data\repDb1</span><br /><span style="font-family: &quot;courier new&quot;;"><span style="color: blue;">New-Item</span> -ItemType Directory -Path \data\repDb2</span><br /><span style="font-family: &quot;courier new&quot;;"><span style="color: blue;">New-Item</span> -ItemType Directory -Path \data\repDb3</span><br /><span style="font-family: &quot;courier new&quot;;"><span style="color: blue;">New-Item</span> -ItemType Directory -Path \log</span><br /><span style="font-family: &quot;courier new&quot;;"><br /></span>Now copy MongoDB Binaries to the drive that you ran above PowerShell commands. Change directory to MongoDB bin. And create three separate configuration files in MongoDB bin folder with notepad or any other plain text editor.<br /><ul><li>config1.cnf  </li><li>config2.cnf  </li><li>config3.cnf</li></ul>Create<strong> config1.cnf file</strong> with below content.<br /><br /><pre>logpath=d:\log\log1.txt<br />dbpath=d:\data\repDb1<br />port=9991<br />replSet=samplecluster<br />rest=true</pre><br />Create<strong> config2.cnf file</strong> with below content.<br /><br /><pre>logpath=d:\log\log2.txt<br />dbpath=d:\data\repDb2<br />port=9992<br />replSet=samplecluster<br />rest=true</pre><br />Create<strong> config3.cnf file</strong> with below content.<br /><br /><pre>logpath=d:\log\log3.txt<br />dbpath=d:\data\repDb3<br />port=9993<br />replSet=samplecluster<br />rest=true</pre><br />Now we are going to run MongoDB. For that you must go to MongoDB bin folder. And Press Shift and while you pressing shift right click on the free area. And select ‘Open command window here’<br /><br /><div class="separator" style="clear: both; text-align: center;"><a href="http://4.bp.blogspot.com/-Qi068g6dxxo/UOPS6McilAI/AAAAAAAAAjA/jLhI0JEaDnE/s1600/mongocmd.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="320" src="https://4.bp.blogspot.com/-Qi068g6dxxo/UOPS6McilAI/AAAAAAAAAjA/jLhI0JEaDnE/s320/mongocmd.png" width="280" /></a></div><br /><br /><br />Now you will get a Command Prompt. Type below three commands on your command prompt.<br /><pre>start mongod –-config config1.cnf<br />start mongod –-config config2.cnf<br />start mongod –-config config3.cnf</pre>Now you should log in to one of those MongoDB instances to initiate the MongoDB replication set. For that type below command.<br /><pre></pre><pre>mongo localhost:9991</pre>Now you have a MongoDB shell and you can initiate replication set. Type below command to initiate the MongoDB replication set.<br /><pre></pre><pre>rs.initiate()</pre>This command will take some time. Don’t worry most of the times it's not stuck. Then you have to add other instances to this MongoDB replication set.<br /><pre></pre><pre>rs.add(“localhost:9992”);<br />rs.add(“localhost:9993”);</pre>This will return { “ok” : 1 }. If it is not please replace your machine name to “localhost”. Now it is done. Your MongoDB replication is up and running!!!</div>

### Tags

- MongoDB
- MongoShell
- Mongo Shell
- MongoDB Replication
- MongoDB Install
---
layout: post
title: How to shutdown MongoDB instance from MongoDB Shell?
---

<div dir="ltr" style="text-align: left;" trbidi="on"><div style="text-align: justify;">For some cases, we may have access to database instance of MongoDB as DBA. But we may not have access to Linux or Windows box to shutdown the MongoDB service or MongoDB instance. To Shutdown the MongoDB instance you should be able to log in to "admin" database. &nbsp;If your MongoDB instance is running with "auth" mode you really need a password and username. In this demo, I assume MongoDB instance is not running with "auth" mode.</div><br />I log in to MongoDB shell first.<br /><pre>mongo</pre><br />Then I change the database to the admin database.<br /><pre>use admin</pre><br />Now I'm going to run that command. This command will shutdown the instance hence think twice before you use it.<br /><pre>db.runCommand( { shutdown : 1 } );</pre><br /><br /></div>

### Tags

- MongoDB
- mongo
- MongoDB Shell
- MongoShell
- Shutdown MongoDB
- database instance
- Stop MongoDB from Shell

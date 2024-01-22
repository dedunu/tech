---
layout: post
title: Using same key twice in MongoDB
---

In MongoDB course one of my&nbsp;<a href="http://www.dbfriend.net/" target="_blank">colleague</a>&nbsp;has run a query with two&nbsp;occurrences&nbsp;of same key. Then I thought query will fail on validation. But the way that MongoDB behaves is different on this scenario.<br /><div><br /></div><div><div>&gt;&nbsp;</div><div>&gt; db.test.insert ({name:1})</div><div>&gt; db.test.insert ({name:2})</div><div>&gt; db.test.insert ({name:3})</div><div>&gt; db.test.insert ({name:4})</div><div>&gt;&nbsp;</div><div>&gt; db.test.find({name:1,name:2})</div><div>{ "_id" : ObjectId("518342a1f193f1de8aef117e"), "name" : 2 }</div><div>&gt;&nbsp;</div><div>&gt; db.test.find({name:3,name:1})</div><div>{ "_id" : ObjectId("5183429ef193f1de8aef117d"), "name" : 1 }</div><div>&gt;&nbsp;</div></div><div><br /></div><div>Then I ran some insert statements.</div><div><br /></div><div><div>&gt;&nbsp;</div><div>&gt; db.test.insert ({name:"Dedunu",name:"Dinesh"})</div><div>&gt;&nbsp;</div><div>&gt; db.test.find()</div><div>{ "_id" : ObjectId("51833fabeadc78fbf0f7232d"), "name" : "Dinesh" }</div><div>&gt;&nbsp;</div></div><div><br /></div><div>I think this&nbsp;behavior&nbsp;is inherited from JavaScript.&nbsp;</div>

### Tags

- MongoDB
- mongo
- Mongo Shell
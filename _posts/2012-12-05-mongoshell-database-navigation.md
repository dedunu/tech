---
layout: post
title: "MongoShell Database Navigation"
---

If you are new to MongoDB you may need to discover the databases and collections (basically objects) on your MongoDB instance. For this easily you can use a GUI tool like [MongoVUE](https://www.blogger.com/u/1/mongovue.com). But in this blog post, I’m not going to describe GUI tools. I’m going to explain about MongoShell to navigate through database objects.

I can remember the first day that I used Linux. In that day I fed up with Terminal and gave it up. But now I think it's cool!. ![Smile](https://dedunumax.files.wordpress.com/2012/12/wlemoticon-smile.png) Somehow if you want to do something easier I still recommend GUI Tools.  
First to execute those commands you should log into MongoShell. In windows mongo.exe. 

**How to take database List?**  

```javascript
show dbs  
```

**How to check the database that you are currently using?**  

```javascript
db  
```

or  

```javascript
print(db);  
```

**How to change to a new database?**  

```javascript
use <database name>  
```

E.g:-  

```javascript
use AdventureWorks2012 
```

**How to take the list of Collection in the current Database?**  

```javascript
show collections  
```
  
or  

```javascript
db.getCollectionNames();  
```
  
**How to take the list of Users in Database?**  

```javascript
show users  
```
  
or  

```javascript
db.system.users.find();
```

### Tags

- MongoDB
- MongoShell
- Mongo Shell

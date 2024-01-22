---
layout: post
title: "How to copy a Database from a MongoDB instance to another?"
---

Some times we need to take backups or we need to copy databases to another server for administrative purposes. But sometimes just copying files is not enough. In MongoDB Shell, they support to copy the database from remote instance to the current one with a single command. ( :D Just like Single Click in Windows )  
  
For this demo, I made alive two instances of MongoDB from the following commands.  

```console
# Instance 1  
mongod --port 9990 --dbpath /data/db1 

# Instance 2  
mongod --port 9991 --dbpath /data/db2
```
  
In instance 1 there is a database called "csampledb1". For that, I need to connect to the first instance to create that database.  

```console
mongo localhost:9990
```
  
[![mongoshellinstance1](https://dedunumax.files.wordpress.com/2012/12/mongoshellinstance1.jpg)](http://dedunu.info/2012/12/16/how-to-copy-a-database-from-a-mongodb-instance-to-another/mongoshellinstance1/#main)  
  
After that with the following commands, I create a database with one collection.  

```javascript
use csampledb1  
db.csamplecol1.save({id:1, name:"sample name"})
```
  
Then I log in to next MongoDB instance using MongoDB Shell.  

```console
mongo localhost:9991
```
  
Then I use a single command to copy the database from instance 1 to instance 2.  

```javascript
db.copyDatabase("csampledb1","csampledb2","localhost:9990")
```
  
[![mongoshellinstance2](https://dedunumax.files.wordpress.com/2012/12/mongoshellinstance2.jpg)](http://dedunu.info/2012/12/16/how-to-copy-a-database-from-a-mongodb-instance-to-another/mongoshellinstance2/#main)  
  
Syntax of this function is like below. There are two arguments which I didn't use.  

```javascript
db.copyDatabase(fromdb, todb, fromhost, username, password)
```

### Tags

- MongoDB
- MongoDB running two instances
- first instance
- MongoDB Shell
- administrative purposes
- software
- MongoDB copy databases

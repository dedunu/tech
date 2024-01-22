---
layout: post
title: How to install MongoDB as a Windows Service
---

At the first date I heard about NoSQL DBMS, I felt insane. Then I got eager to learn. But I didn’t pay any attention to learn. Later I got to know that MongoDB is a scalable one. Then I got a chance to follow [free MongoDB course](http://education.10gen.com/). Although I registered to both Developer and DBA courses I had no time to watch developer tutorials. But I finished DBA 1st Week. In that video tutorial, they explain how to install MongoDB on Windows as well as on UNIX. But when we are using Mongo in Windows Development Environment it’s a headache to start service again and again. Because of that, I wanted to install MongoDB as a Windows Service.  
  
In that video tutorial, they explain how to just run MongoDB on Windows Environment. First of all, you should have a data directory. For that, you should create two folders in the drive that you are planning to install MongoDB. Let's assume that we are going to install MongoDB on D: Drive.  
  
Then you should create two directories(Folders) in `D:` drive  

*   `D:\data`
*   `D:\data\db`

You can manually change the data path but for a beginner, it's better to use the default path. And if you are trying to install it as Service you need to create a log folder.  

*   `D:\log`
    
Then open a command prompt and go to the MongoDB bin. I assume you have pasted it on `D:\` drive. your directory path will look like this `D:\mongodb-win32-x86\_64-2.2.0\bin.`  
  
After that, you should run mongod.exe to install MongoDB as a windows service.  

```console
mongod.exe --install --logpath D:\log
```

When you have typed and entered this command on CMD, it will create a Service for MongoDB. You can start MongoDB service with below command.  

```console
net start MongoDB**
```

Enjoy Mongo!!!!

### Tags

- MongoDB
- MongoDB Windows Service
- MongoDB Install
- NoSQL

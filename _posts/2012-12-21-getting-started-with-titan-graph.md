---
layout: post
title: "Getting Started with Titan Graph Database"
---

I have used Neo4J as my first graph database. And it had web console which makes easier to handle. But this time I'm not going to tell you how to get started with Neo4J. This time we are going to work with Titan which is an open source project which is held by [Aurelius](http://thinkaurelius.github.com/titan/).  
  
This database is more scalable graph database. Let's get to know how to get started with Titan Graph Database.  
  
First download Titan from Titan Site  
[Click Here to download Titan Graph Database](http://thinkaurelius.github.com/titan/)  
  
Then extract titan to a disk. In this example, I take D drive. If you are Linux user extract this Titan file to somewhere you can execute.  
  
Then take a shell in Linux or command prompt in Windows. Then move to the titan folder. Then move to the bin.  
  
Before taking Gremlin Console you need to install Java.  
  
After that, if you are Linux guy run this command.  

```console
$ bash gremlin.sh
```

Or if you are windows user, your command is,  

```console
$ gremlin.bat
```
  
Now you have the gremlin shell. Now we are going to connect to the graph database. Basically, we can use it with its three main storage backends. They are  

*   Cassandra
*   HBase
*   Oracle Berkley 

But I'm not going to use any of them now. Now I'm just going to use Titans Native Storage.  

```groovy
g = TitanFactory.open('local/tmp');
```

 Below command will initiate a graph and assign it to g variable. Now in your bin, you can see local and temp folders are created.  
  
If you hope to search through your graph in Titan you have to index it first. Otherwise, you can't search for it. Let say we are going to search with "name" property. Then we have to add "name" index first.  
  
```groovy
g.createKeyIndex('name', Vertex.class);
```
  
Now you are ready to add nodes and edges. And you have an index on "name" property.  
  
```groovy
v = g.addVertex(null);
```

This will create a new node on the graph. we are going to set properties to this node.  

```groovy
v.setProperty('name','dedunu');  
v.setProperty('type','person');  
v.setProperty('age',20);

v1 = g.addVertex(null);
v1.setProperty('name','malinda');
v1.setProperty('type','person');
v1.setProperty('age',22);

v2 = g.addVertex(null);
v2.setProperty('name','UCSC');
v2.setProperty('type','institute');  
```  

Now we have three nodes. Two of them are Persons and the other one is an institute.  Now we are going to create relationships between those three nodes.  
  
```groovy
e1 = g.addEdge(null, v, v2, 'study in');  
e2 = g.addEdge(null, v1, v2, 'study in');  
e3 = g.addEdge(null, v, v1, 'knows');  
e4 = g.addEdge(null, v1, v, 'knows');
```
  
Now you have a graph like this.  
  
[![](https://4.bp.blogspot.com/-4-rUSq8-M3Y/UNSgFo-TAVI/AAAAAAAAAiQ/qbclVtX7kiM/s1600/graph.png)](http://4.bp.blogspot.com/-4-rUSq8-M3Y/UNSgFo-TAVI/AAAAAAAAAiQ/qbclVtX7kiM/s1600/graph.png)

 Now we are going to have a journey around our beautiful data!!! And now I want to know where Malinda "study in". For that, I have to load Malinda to a vertex variable. I'll use an existing one.  

```groovy 
v1.out('study in').map();
```
  
Now I want who studies at UCSC.  For that, I have to load UCSC to a variable first. I'll use an existing one.  

```groovy
v2.in('study in').map();
```
  
If I only need names of them then below one is the command.  
  
```groovy
v2.in('study in').name;
```

Finally to commit all those things to disk you have to shut down the graph for that run below command.  
  
```groovy
g.shutdown();
```
  
Be careful those commands are case sensitive!!! Enjoy Graphs!!!

### Tags

- Titan DB
- Titan with Gremlin
- Tinker Pop
- Graph DB
- How to begin titan db
- Graph database
- Gremlin
- Titan

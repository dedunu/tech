---
layout: post
title: "HDFS - How to recover corrupted HDFS metadata in Hadoop 1.2.X?"
---

You might have Hadoop in your production. And sometimes Tera-bytes of data is residing in Hadoop. HDFS metadata can get corrupted. `Namenode` won't start in such cases. When you check `Namenode` logs you might see exceptions.

```java
ERROR org.apache.hadoop.dfs.NameNode: java.io.EOFException
    at java.io.DataInputStream.readFully(DataInputStream.java:178)
    at org.apache.hadoop.io.UTF8.readFields(UTF8.java:106)
    at org.apache.hadoop.io.ArrayWritable.readFields(ArrayWritable.java:90)
    at org.apache.hadoop.dfs.FSEditLog.loadFSEdits(FSEditLog.java:433)
    at org.apache.hadoop.dfs.FSImage.loadFSEdits(FSImage.java:759)
    at org.apache.hadoop.dfs.FSImage.loadFSImage(FSImage.java:639)
    at org.apache.hadoop.dfs.FSImage.recoverTransitionRead(FSImage.java:222)
    at org.apache.hadoop.dfs.FSDirectory.loadFSImage(FSDirectory.java:79)
    at org.apache.hadoop.dfs.FSNamesystem.initialize(FSNamesystem.java:254)
    at org.apache.hadoop.dfs.FSNamesystem.<init>(FSNamesystem.java:235)
    at org.apache.hadoop.dfs.NameNode.initialize(NameNode.java:131)
    at org.apache.hadoop.dfs.NameNode.<init>(NameNode.java:176)
    at org.apache.hadoop.dfs.NameNode.<init>(NameNode.java:162)
    at org.apache.hadoop.dfs.NameNode.createNameNode(NameNode.java:846)
    at org.apache.hadoop.dfs.NameNode.main(NameNode.java:855)
 ```

 If you have a development environment, you can always format the HDFS and continue. 

 > **BUT IF YOU FORMAT HDFS YOU lose ALL THE FILES IN HDFS!!!**

 So Hadoop Administrators can't format HDFS simply. But you can recover your HDFS to last checkpoint. You might lose some data files. But more than 90% of the data might be safe. Let's see how to recover corrupted HDFS metadata.

 Hadoop is creating checkpoints periodically in Namenode folder. You might see three folders in Namenode directory. 

There are : 

```
current
image
previous.checkpoint
```

The `current` folder must be corrupted most probably. 


- Stop all the Hadoop services from all the nodes.
- Backup both "current" and "previous.checkpoint" directories. 
- Delete "current" directory. 
- Rename "previous.checkpoint" to "current"
- Restart Hadoop services. 

Steps I followed I have mentioned above. Below commands were run to recover the HDFS. Commands might slightly change depending on your installation.

```bash
$ /usr/local/hadoop/stop-all.sh
$ cd <namenode.dir>
$ cp -r current current.old
$ cp -r previous.checkpoint previous.checkpoint.old
$ mv previous.checkpoint current
$ /usr/local/hadoop/start-all.sh
```

That's all!!!! Everything was okay after that!

### Tags

- metadata
- recover
- hadoop
- linux
- hdfs
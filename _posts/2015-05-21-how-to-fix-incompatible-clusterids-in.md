---
layout: post
title: "How to fix Incompatible clusterIDS in Hadoop?"
---

When you are installing and trying to set up your Hadoop cluster you might face an issue like below.

```java
FATAL org.apache.hadoop.hdfs.server.datanode.DataNode: Initialization failed for Block pool (Datanode Uuid unassigned) service to master/192.168.1.1:9000. Exiting. 
java.io.IOException: Incompatible clusterIDs in /home/hadoop/hadoop/data: namenode clusterID = CID-68a4c0d2-5524-486e-8bc9-e1fc3c5c2e29; datanode clusterID = CID-c6c3e9e5-be1c-4a3f-a4b2-bb9441a989c5
    at org.apache.hadoop.hdfs.server.datanode.DataStorage.doTransition(DataStorage.java:646)
    at org.apache.hadoop.hdfs.server.datanode.DataStorage.addStorageLocations(DataStorage.java:320)
    at org.apache.hadoop.hdfs.server.datanode.DataStorage.recoverTransitionRead(DataStorage.java:403)
    at org.apache.hadoop.hdfs.server.datanode.DataStorage.recoverTransitionRead(DataStorage.java:422)
    at org.apache.hadoop.hdfs.server.datanode.DataNode.initStorage(DataNode.java:1311)
    at org.apache.hadoop.hdfs.server.datanode.DataNode.initBlockPool(DataNode.java:1276)
    at org.apache.hadoop.hdfs.server.datanode.BPOfferService.verifyAndSetNamespaceInfo(BPOfferService.java:314)
    at org.apache.hadoop.hdfs.server.datanode.BPServiceActor.connectToNNAndHandshake(BPServiceActor.java:220)
    at org.apache.hadoop.hdfs.server.datanode.BPServiceActor.run(BPServiceActor.java:828)
```

You might haven't formatted your name node properly. But if this was in a test environment you can easily delete data and name node folders, and reformat the HDFS. To format you can run below command.

> **WARNING!!! : IF YOU RUN BELOW COMMAND YOU WILL LOSE ALL YOUR DATA.**


```console
$ hdfs namenode -format
```

But if you have a lot of data in your Hadoop cluster and you can't easily format it. Then this post is for you.

First, stop all Hadoop processes running. Then login into your name node. Find the value of `dfs.namenode.name.dir` property. Run below command with your name node folder.

```console
$ cat <dfs.namenode.name.dir>/current/VERSION
```

It will look like this:

```
#Thu May 21 08:29:01 UTC 2015
namespaceID=1938842004
clusterID=CID-68a4c0d2-5524-486e-8bc9-e1fc3c5c2e29
cTime=0
storageType=NAME_NODE
blockpoolID=BP-2104944316-127.0.1.1-1430820636449
layoutVersion=-60
```

Copy the `clusterID` from name node. Then login into the problematic slave node. Find `dfs.datanode.data.dir` folder. Run below command to edit the `VERSION` file.

```console
$ vim <dfs.datanode.data.dir>/current/VERSION 
```

Your data node cluster `VERSION` file will look like below. Replace the `cluster ID` you copied from name node.

```
#Thu May 21 08:31:31 UTC 2015
storageID=DS-b7d3c421-0366-4a66-8d14-78362389ed73
clusterID=CID-c6c3e9e5-be1c-4a3f-a4b2-bb9441a989c5
cTime=0
datanodeUuid=724f8bad-c0ca-4ded-98d6-a860d3165289
storageType=DATA_NODE
layoutVersion=-56
```

Restart the service.

### Tags

- hadoop
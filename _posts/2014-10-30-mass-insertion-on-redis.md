---
layout: post
title: "Mass insertion on Redis"
---

You may want to insert a lot of data into Redis. This would be easier to insert a lot of data into Redis using Linux commands. Let's say we have a comma separated values in a file.

data.csv:
```
key1,1200
key2,5000
key35,12345
key12,4500
```

With the following command, you can load all the data into Redis. But you should start the Redis server first.

```console
$ cat data.csv | awk -F',' '{print " SET \""$1"\" \""$2 "\"\n"}'| /opt/redis-2.8.17/src/redis-cli --pipe
```

You can change data.csv as you want and according to your file.

### Tags

- redis

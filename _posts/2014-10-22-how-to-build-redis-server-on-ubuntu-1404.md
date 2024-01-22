---
layout: post
title: How to build Redis server on Ubuntu 14.04
---

Recently we used Redis server on Ubuntu 14.04. And I just thought about writing a blog post to show how to build Redis on Ubuntu server or desktop editions. 

First of all, you have to go to the Redis site and download the Redis source code. [Redis site](https://redis.io/)

Copy the download link from Redis site. Currently, download link looks like this "`http://download.redis.io/releases/redis-2.8.17.tar.gz`". It may change depending on the version you want to download.

Then connect to the server through SSH or take a terminal on Ubuntu desktop machine. Run below command

```console
$ wget <URL that you copied from redis site>
```

Then you want to install `build-essential` and `libjemalloc-dev` in order to build Redis server. To install those packages run below command.

```console
$ sudo apt-get update && sudo apt-get install buid-essential libjemalloc-dev
```

After installing dependencies and tool you want to extract Redis archive. Run below commands to extract it. Change the archive name depending on your download.

```console
$ tar xvf redis-2.X.XX.tar.gz
$ cd redis-2.X.XX
```

To build Redis server type below command on the terminal. It may take a while to build Redis.

```console
$ make
```

If it didn't throw any errors, Congrats! You just build your own Redis server. Then if you want to run Redis server run below command. Make sure that you are in Redis folder.

```console
$ ./src/redis-server
```

Then you can test Redis server using a `redis-cli` tool like below.

```console
dedunu@test5:~/redis-2.8.17$ src/redis-cli
127.0.0.1:6379>
127.0.0.1:6379> set key1 value1
OK
127.0.0.1:6379> set key2 value15
OK
127.0.0.1:6379> get key1
"value1"
127.0.0.1:6379> get key2
"value15"
127.0.0.1:6379> 
```

If you get an output like above your Redis works fine!

### Tags

- Ubuntu
- linux
- redis
- in-memory database
- build
- Ubuntu 14.04

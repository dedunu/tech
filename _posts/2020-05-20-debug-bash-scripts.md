---
layout: post
title: "Debug bash scripts"
---

One day, I had to go through a large bash script and create a Debian package for our system. It could have been a strenuous job if I had to understand it. I was lazy to read it. So I found an easy way to get all the steps. I downloaded this on a container and ran with `bash -x`.

```console
# wget https://download.vividcortex.com/install
--2020-05-20 16:24:06--  https://download.vividcortex.com/install
Resolving download.vividcortex.com (download.vividcortex.com)... 13.33.243.45, 13.33.243.100, 13.33.243.16, ...
Connecting to download.vividcortex.com (download.vividcortex.com)|13.33.243.45|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 45048 (44K) [application/octet-stream]
Saving to: 'install'

install                  100%[==================================>]  43.99K  --.-KB/s    in 0.06s   

2020-05-20 16:24:07 (732 KB/s) - 'install' saved [45048/45048]

# ls
install
# bash -x install 
+ VERSION=1.8.159
+ baseuri=https://download.vividcortex.com
+ set -u
+ POSIXLY_CORRECT=1
+ export POSIXLY_CORRECT
+ TERM=dumb
+ export TERM
+ unalias -a
+ defaultconfdir=/etc/vividcortex
+ confdir=/etc/vividcortex
+ logdir=/var/log/vividcortex
+ runvdir=/var/run/vividcortex
+ superpid=/var/run/vc-agent-007.pid
+ tempdir=
+ socks5=
+ SKIPCERTS=
+ LOADCERTS=
+ EXISTS='command -v'
+ command -v ls
+ command -v ls
+ test https://download.vividcortex.com = unknown
++ id -u
+ '[' 0 -ne 0 ']'
+ test -d /usr
+ exitcode=4
+ '[' 4 -eq 4 ']'
++ getopt -o hslkbup:t:v:i:a:c:d:g: -l help,autostart,no-autostart,start-now,load-certs,skip-certs,batch,static,uninstall,delete,debug,off-host,update-init,static-ip,dyn-sample-text,no-proxy,proxy:,token:,version:,init:,sample:,api-uri:,cdn-uri:,bin-dir:,cfg-dir:,aggr-uri:,hostname:,host-tags: -n install --
+ GETARGS=' --'
+ test 0 -eq 0
+ eval set -- ' --'
++ set -- --
+ AUTOSTART=
...
```

You can use this if you want to debug or understand a shell script. But of course, you should be able to run it to test.

### Tags

- linux
- bash
- debug

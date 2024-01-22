---
layout: post
title: "Ubuntu 20.04 Server: How to change DNS and domain name"
---

In the new Ubuntu version, you cannot change `/etc/resolv.conf`.  You can change it. But it won't last a restart. It will be replaced by `systemd-resolved`.

I wanted to change the domain name and DNS/nameserver. If you look at `man 8 systemd-resolved`, you can see you have to change a different file called `/etc/systemd/resolved.conf`.

Please change your `resolved.conf` file accordingly. My Domain Name server is `10.0.2.15`. I set my domain name as `dedunu.info`. I added Google DNS as Fallback DNS.

```console
$ cat /etc/systemd/resolved.conf 
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.
#
# Entries in this file show the compile time defaults.
# You can change settings by editing this file.
# Defaults can be restored by simply deleting this file.
#
# See resolved.conf(5) for details

[Resolve]
DNS=10.0.2.15
FallbackDNS=8.8.8.8
Domains=dedunu.info
#LLMNR=no
#MulticastDNS=no
#DNSSEC=no
#DNSOverTLS=no
#Cache=yes
#DNSStubListener=yes
#ReadEtcHosts=yes
```

I had to restart the server to apply the configuration.

### Tags 

- linux
- ubuntu
- dns
- domainanme
- resolv

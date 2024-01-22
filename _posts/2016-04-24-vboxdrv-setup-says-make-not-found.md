---
layout: post
title: "vboxdrv setup says make not found"
---

After you update the kernel you need to run `vboxdrv setup`. But if you are trying to compile it for the first time or after removing the `build-essential` package, you might see the below error.

```console
$ sudo /etc/init.d/vboxdrv setup
[sudo] password for user:
Stopping VirtualBox kernel modules ...done.
Recompiling VirtualBox kernel modules ...failed!
  (Look at /var/log/vbox-install.log to find out what went wrong)
$ cat /var/log/vbox-install.log
/usr/share/virtualbox/src/vboxhost/build_in_tmp: 62: 
/usr/share/virtualbox/src/vboxhost/build_in_tmp: make: not found
/usr/share/virtualbox/src/vboxhost/build_in_tmp: 62: 
/usr/share/virtualbox/src/vboxhost/build_in_tmp: make: not found
/usr/share/virtualbox/src/vboxhost/build_in_tmp: 62: 
/usr/share/virtualbox/src/vboxhost/build_in_tmp: make: not found
```

Ubuntu needs `build-essential` to run above command. Run below command to install the `build-essential`.

```console
$ sudo apt-get install build-essentail
$ sudo /etc/init.d/vboxdrv setup
```

Then you can use the virtual box!

### Tags

- Virtualbox
- virtualization
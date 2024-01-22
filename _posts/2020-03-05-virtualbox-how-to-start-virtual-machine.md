---
layout: post
title: "VirtualBox: How to start a virtual machine without a window on OS X?"
---

I use a VirtualBox for my day to day work. The whole purpose is to move it to a new laptop and start using it with all the tools, configuration files and keys. But I don't want to open the VirtualBox with a window.

> Missing Images

So I found a way to launch the virtual machine using the command line without the window. My virtual machine is called "`dev`". Use below command.

```console
$ VBoxManage startvm "dev" --type headless
```

> Missing Images

### Tags

- Virtual
- osx
- VirtualBox
- Mac
- virtualization

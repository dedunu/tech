---
layout: post
title: "Increase memory and CPUs on Vagrant Virtual Machines"
---

Last post I showed how to create multiple nodes in a single Vagrant project. Usually "`ubuntu/trusty64`" box comes with 500MB. For some developers need more RAM, more CPUs. From this post, I'm going to show how to increase the memory and number of CPUs in a vagrant project. Run below commands:

```console
$ mkdir testProject1
$ cd testProject1
$ vagrant init
```

Then edit the Vagrant file like below.

```console
Vagrant.configure("2") do |config|
  config.vm.define "master" do |master|    
    master.vm.box = "ubuntu/trusty64"
    master.vm.hostname = "master.local"
    master.vm.network "private_network", ip: "192.168.2.2"
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 8192
    v.cpus = 2
  end
end
```

Above changes will increase memory to 8GB and also it will add one more core. Run below commands to start the vagrant machine and get the SSH access.

``` console
$ vagrant up
$ vagrant ssh
```

If you have an existing project, you just have to add these lines. When you restart the project memory would be increased.

### Gists

- <https://gist.github.com/dedunumax/62b88beb311ea44939ed>

### Tags

- vagrant
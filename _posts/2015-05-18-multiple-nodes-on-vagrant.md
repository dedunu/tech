---
layout: post
title: "Multiple nodes on Vagrant"
---

Recently I started working with Vagrant. A vagrant is a good tool that you can use for development. From this post, I'm going to explain how to create multiple nodes on the Vagrant project.

```console
$ mkdir testProject
$ cd testProject
$ vagrant init
```

If you run above commands, it will create a Vagrant project for you. Now we have to do changes to the vagrant file. Your initial vagrant file will look like below.

```console
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "base"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL
end
```

You have to edit Vagrantfile add content like below.

```console

Vagrant.configure("2") do |config|
  config.vm.define "master" do |master|    
    master.vm.box = "ubuntu/trusty64"
    master.vm.hostname = "master.local"
    master.vm.network "private_network", ip: "192.168.2.2"
  end

  config.vm.define "slave1" do |slave1|
    slave1.vm.box = "ubuntu/trusty64"
    slave1.vm.network :private_network, ip: "192.168.2.3"
    slave1.vm.hostname = "slave1.local"
  end

  config.vm.define "slave2" do |slave2|
    slave2.vm.box = "ubuntu/trusty64"
    slave2.vm.network :private_network, ip: "192.168.2.4"
    slave2.vm.hostname = "slave2.local"
  end
end
```

Above sample vagrant file will create three nodes. Now run below command to start Vagrant virtual machines.

```console
$ vagrant up
```

If you followed the instruction properly, you will get an output like below.

```console
Bringing machine 'master' up with 'virtualbox' provider...
Bringing machine 'slave1' up with 'virtualbox' provider...
Bringing machine 'slave2' up with 'virtualbox' provider...
==> master: Importing base box 'ubuntu/trusty64'...
==> master: Matching MAC address for NAT networking...
==> master: Checking if box 'ubuntu/trusty64' is up to date...
==> master: A newer version of the box 'ubuntu/trusty64' is available! You currently
==> master: have version '20150420.1.1'. The latest is version '20150512.0.1'. Run
==> master: `vagrant box update` to update.
==> master: Setting the name of the VM: test2_master_1431951423815_51724
==> master: Clearing any previously set forwarded ports...
==> master: Clearing any previously set network interfaces...
==> master: Preparing network interfaces based on configuration...
    master: Adapter 1: nat
    master: Adapter 2: hostonly
==> master: Forwarding ports...
    master: 22 => 2222 (adapter 1)
==> master: Booting VM...
==> master: Waiting for machine to boot. This may take a few minutes...
    master: SSH address: 127.0.0.1:2222
    master: SSH username: vagrant
    master: SSH auth method: private key
    master: Warning: Connection timeout. Retrying...
    master: Warning: Remote connection disconnect. Retrying...
    master: 
    master: Vagrant insecure key detected. Vagrant will automatically replace
    master: this with a newly generated keypair for better security.
    master: 
    master: Inserting generated public key within guest...
    master: Removing insecure key from the guest if its present...
    master: Key inserted! Disconnecting and reconnecting using new SSH key...
==> master: Machine booted and ready!
==> master: Checking for guest additions in VM...
==> master: Setting hostname...
==> master: Configuring and enabling network interfaces...
==> master: Mounting shared folders...
    master: /vagrant => /Users/ddhananjaya/Downloads/test2
==> slave1: Importing base box 'ubuntu/trusty64'...
==> slave1: Matching MAC address for NAT networking...
==> slave1: Checking if box 'ubuntu/trusty64' is up to date...
==> slave1: A newer version of the box 'ubuntu/trusty64' is available! You currently
==> slave1: have version '20150420.1.1'. The latest is version '20150512.0.1'. Run
==> slave1: `vagrant box update` to update.
==> slave1: Setting the name of the VM: test2_slave1_1431951479185_96384
==> slave1: Clearing any previously set forwarded ports...
==> slave1: Fixed port collision for 22 => 2222. Now on port 2200.
==> slave1: Clearing any previously set network interfaces...
==> slave1: Preparing network interfaces based on configuration...
    slave1: Adapter 1: nat
    slave1: Adapter 2: hostonly
==> slave1: Forwarding ports...
    slave1: 22 => 2200 (adapter 1)
==> slave1: Booting VM...
==> slave1: Waiting for machine to boot. This may take a few minutes...
    slave1: SSH address: 127.0.0.1:2200
    slave1: SSH username: vagrant
    slave1: SSH auth method: private key
    slave1: Warning: Connection timeout. Retrying...
    slave1: Warning: Remote connection disconnect. Retrying...
    slave1: 
    slave1: Vagrant insecure key detected. Vagrant will automatically replace
    slave1: this with a newly generated keypair for better security.
    slave1: 
    slave1: Inserting generated public key within guest...
    slave1: Removing insecure key from the guest if its present...
    slave1: Key inserted! Disconnecting and reconnecting using new SSH key...
==> slave1: Machine booted and ready!
==> slave1: Checking for guest additions in VM...
==> slave1: Setting hostname...
==> slave1: Configuring and enabling network interfaces...
==> slave1: Mounting shared folders...
    slave1: /vagrant => /Users/ddhananjaya/Downloads/test2
==> slave2: Importing base box 'ubuntu/trusty64'...
==> slave2: Matching MAC address for NAT networking...
==> slave2: Checking if box 'ubuntu/trusty64' is up to date...
==> slave2: A newer version of the box 'ubuntu/trusty64' is available! You currently
==> slave2: have version '20150420.1.1'. The latest is version '20150512.0.1'. Run
==> slave2: `vagrant box update` to update.
==> slave2: Setting the name of the VM: test2_slave2_1431951533297_11049
==> slave2: Clearing any previously set forwarded ports...
==> slave2: Fixed port collision for 22 => 2222. Now on port 2201.
==> slave2: Clearing any previously set network interfaces...
==> slave2: Preparing network interfaces based on configuration...
    slave2: Adapter 1: nat
    slave2: Adapter 2: hostonly
==> slave2: Forwarding ports...
    slave2: 22 => 2201 (adapter 1)
==> slave2: Booting VM...
==> slave2: Waiting for machine to boot. This may take a few minutes...
    slave2: SSH address: 127.0.0.1:2201
    slave2: SSH username: vagrant
    slave2: SSH auth method: private key
    slave2: Warning: Connection timeout. Retrying...
    slave2: Warning: Remote connection disconnect. Retrying...
    slave2: 
    slave2: Vagrant insecure key detected. Vagrant will automatically replace
    slave2: this with a newly generated keypair for better security.
    slave2: 
    slave2: Inserting generated public key within guest...
    slave2: Removing insecure key from the guest if its present...
    slave2: Key inserted! Disconnecting and reconnecting using new SSH key...
==> slave2: Machine booted and ready!
==> slave2: Checking for guest additions in VM...
==> slave2: Setting hostname...
==> slave2: Configuring and enabling network interfaces...
==> slave2: Mounting shared folders...
    slave2: /vagrant => /Users/ddhananjaya/Downloads/test2
```

If you want to connect to the master node, run below command.

```console
$ vagrant ssh master
```

If you want to connect to slave1 node, run below command.

```console
$ vagrant ssh slave1
```

Whatever the machine you want to connect you just have to type `vagrant ssh`. Hope this will help you!

### Gists

- <https://gist.github.com/dedunumax/e67183ff613083fb7617>
- <https://gist.github.com/dedunumax/b1190e9177e75e33d21c>
- <https://gist.github.com/dedunumax/467280aff02bccd0b9a2>

### Tags

- vagrant

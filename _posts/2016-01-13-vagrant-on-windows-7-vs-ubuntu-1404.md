---
layout: post
title: Vagrant on Windows 7 vs Ubuntu 14.04
---

My whole team had to work on a project which is using Vagrant. Most of us had 8GB memory except one unfortunate intern. He had only 4GB of memory on his workstation. All the team members could spawn Vagrant machines without a problem except him.

So we requested for more memory. Insisted IT department to upgrade it to 8GB. Oh no! Our IT is going to retire desktops. So they don't buy new parts for an existing desktop system. Somehow we managed to get a 1GB memory card. Now he got 5GB memory in his computer. This computer had an Athlon processor. ( I cannot recall the model number.)

Then we tried to spin it up again. To provision to the vagrant machine, it took at least 3 hours. Sometimes the package gets corrupted. Somehow he stopped to provision machines, once he realized that it is useless.

Then we moved him to another task. There he had to work with Ubuntu closely. So I forced him to install Ubuntu. However, this kid was okay to install Ubuntu. Then I created Ubuntu 14.04 USB bootable drive. Then he installed Ubuntu. After installation, he just tried to start the Vagrant. The vagrant machine got provisioned within minutes. Still, the system has 1GB+ free memory.

Windows 7 vs Ubuntu 14.04, Ubuntu 14.04 wins when it compares with memory consumption.  

### Tags

- Ubuntu
- windows
- performance issue
- vagrant

---
layout: post
title: Installing Cisco Packet Tracer 6.0.1 on Ubuntu 13.04/12.04 (64-Bit)
---

I was watching some CBT Nugget Tutorials and then I wanted to work with Cisco Routers. But I don't have any Cisco device. Then I downloaded the Cisco Packet Tracer.

If you want to install Cisco Packet Trace 6.0.1 you have to download "Cisco Packet Tracer 6.0.1 for Linux - Ubuntu installation (no tutorials).bin" file. This name is too long for me. Then I renamed it to "cp.bin".

Then take a terminal window and change directory to the place where you downloaded the installation file. Type following commands:

```bash
chmod +x cp.bin
./cp.bin
```

Then press the space bar to scroll down "EULA". And press "y". Then Press "Enter" key. Setup will prompt for the root password, Please enter it. You will successfully install Cisco Packet Tracer, but if you are going to run it, you will get nothing. That is because libraries you want to run this on 64 bit Ubuntu version are not installed. You have to install them. To install those 32-bit libraries type following command on your terminal.

```bash
sudo apt-get install ia32-libs-gtk
```

After installing those libraries, you are good to go! You can enjoy Packet Tracer 6.0.1 on Ubuntu 13.04 64bit.

PS: I tested this on Ubuntu 12.04 64bit also. This works! This should work on 12.10 as well, but I couldn't test it.

If you are looking for "[Installing Cisco Packet Tracer 6.0.1 on Ubuntu 13.10 (64-Bit)](https://dedunu.info/2013/12/installing-cisco-packet-tracer-601-on.html)"

### Tags

- Ubuntu
- Ubuntu 13.04 64 bit
- Ubuntu 12.04 64 bit
- Cisco
- Cisco Packet Tracer
- Cisco Packet Tracer 6.0.1

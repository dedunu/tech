---
layout: post
title: Installing RedHat Enterprise Linux from USB Drive
---

<div dir="ltr" style="text-align: left;" trbidi="on"><div style="text-align: justify;">Recently I downloaded&nbsp;Red Hat&nbsp;Enterprise Linux 6.0 to install on my home server. And I'm a person who hasn't used Optical Drive for ages. On my laptop, even DVD Drive doesn't work properly. So&nbsp;every time&nbsp;I use USB Drive (Pen Drive) to install any operating system because my server doesn't have an optical drive. Although I call it a server it is just a machine without CD Rom and blah blah.</div><div style="text-align: justify;"><br /></div><div style="text-align: justify;">Then as usually, I wanted to make&nbsp;Red Hat&nbsp;ISO bootable. Then I used UNetBootin to make my USB drive bootable. But I got a mounting error in installation when I was going to format the hard drive. So it never happened with Ubuntu for me. Then I searched here and there to find a method to install RHEL. Then I found a link to iso2usb. It worked a bit far away from that place. But it just installed minimal&nbsp;Linux&nbsp;server without any GUI. There was no option&nbsp;for it on Installation Wizard. Installation Wizard was GUI one although.</div><div style="text-align: justify;"><br />The I used fedora live USB create. It didn't work properly. Then I copied all the contents of DVD into my server machine and added a repo entry for yum to DVD packages. :)</div></div>

### Tags

- RedHat
- linux
- USB Drive

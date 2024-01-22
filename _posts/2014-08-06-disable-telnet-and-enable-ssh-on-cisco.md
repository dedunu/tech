---
layout: post
title: "'Disable telnet and enable ssh on Cisco Switch (IOS) '"
---

<div dir="ltr" style="text-align: left;" trbidi="on">We recently purchased a Cisco switch for our Hadoop cluster. So I wanted to set up the Cisco switch. But first of all, I want to configure ssh and disable telnet. Let's see how we can do that.<br />Connect to the switch using telnet or using the console port. (You should enable telnet and give a password from express setup.) <br /><pre>enable<br />configure terminal<br />hostname &lt;switchname&gt;<br />ip domain-name &lt;domain name&gt;<br />crypto key generate rsa</pre>Enter "<span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">1024</span>" when it prompts for<br /><pre>How many bits int the modulus [512]:</pre>Then run below commands  <br /><pre>interface fa0/0<br />ip address 192.168.1.1 255.255.255.0<br />no shutdown<br />username &lt;username&gt; priv 15 secret &lt;password&gt;<br />aaa new-model<br />enable secret &lt;password&gt;</pre>If you have a Cisco router use "<span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">0 4</span>" instead of "<span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">0 14</span>"  <br /><pre>line vty 0 14<br />transport input ssh<br />end<br />copy running-config startup-config</pre>Now you can use SSH client to connect to switch.</div>

### Tags

- ssh
- telnet
- cisco catalyst 2960-S
- Cisco

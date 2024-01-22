---
layout: post
title: Installing Cisco Packet Tracer 6.0.1 on Ubuntu 13.10 (64-Bit)
---

<div dir="ltr" style="text-align: left;" trbidi="on"><div style="text-align: justify;">I have posted about <a href="http://www.dedunu.info/2013/09/installing-cisco-packet-tracer-601-on.html" target="_blank">Installing Cisco Packet Tracer on Ubuntu 13.04 and prior versions</a>. But this method is not working on Ubuntu 13.10 because of repository issue I think. So "Medywan" posted a link. I followed linked and found a new way. But it was not in English so I translated it.&nbsp;</div><br /><b>Thanks for the guy who posted it first:&nbsp;</b><a href="http://www.be-root.com/2013/11/19/installation-de-cisco-packettracer-6-sur-ubuntu-13-10-64bits/" style="text-align: left;">http://www.be-root.com/2013/11/19/installation-de-cisco-packettracer-6-sur-ubuntu-13-10-64bits/</a>&nbsp;Credit should go to him!<br /><br />Run those commands in terminal first. <br /><pre>sudo dpkg --add-architecture i386</pre><pre>sudo apt-get install libnss3-1d:i386 libqt4-qt3support:i386 libssl1.0.0:i386 libqtwebkit4:i386 libqt4-scripttools:i386<br /></pre><div style="text-align: justify;">After that install using bin file. "<b>Cisco Packet Tracer 6.0.1 for Linux - Ubuntu installation (no tutorials).bin</b>" would be the filename. This name is too long for me. Then I renamed it to "<b>ciscopt.bin</b>". chmod&nbsp;+x&nbsp;ciscopt.bin </div><pre>./ciscopt.bin<br /></pre>Thanks again to Medywan and the author <a href="http://www.be-root.com/">http://www.be-root.com/</a> site! </div>

### Tags

- Ubuntu
- Ubuntu 13.10 64-bit
- Cisco Packet Tracer
- Cisco Packet Tracer 6.0.1
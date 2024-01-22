---
layout: post
title: PHP MongoDB Driver not working!
---

<div dir="ltr" style="text-align: left;" trbidi="on"><div style="text-align: justify;">In Semester 3 I have PHP unfortunately not MongoDB. So I was doing PHP practicals while I was doing my office things. So suddenly MongoDB came to my mind. Then I tried to connect to MongoDB with PHP. Although I have already tried with .NET. I never tried MongoDB with PHP. So I installed IIS 8.0 and PHP 5.3.1.&nbsp;</div><div style="text-align: justify;"><br /></div><div style="text-align: justify;">Then I downloaded the driver from <a href="http://github.com/mongodb/mongo-php-driver/downloads" target="_blank">github</a>. Extracted it to C:\Program Files (x86)\PHP\v5.3\ext\.&nbsp;</div><div style="text-align: justify;">I added the entry to php.ini properly. Then I restarted IIS using iisreset. But MongoDB Driver for PHP was not loaded properly. Then I was checking and doing so many things but nothing worked.</div><div style="text-align: justify;"><br /></div><div style="text-align: justify;">Try this way!</div><div style="text-align: justify;"><br /></div><div style="text-align: justify;">1. Download driver from <a href="http://github.com/mongodb/mongo-php-driver/downloads" target="_blank">github</a>.</div><div style="text-align: justify;"><br /></div><div style="text-align: justify;">2. Extract the zip file.</div><div style="text-align: justify;"><br /></div><div style="text-align: justify;">3. Copy php_mongo-1.3.2RC1-5.3-vc9-nts.dll to C:\Program Files (x86)\PHP\v5.3\ext\. And rename it to php_mongo.dll.</div><div style="text-align: justify;"><br /></div><div style="text-align: justify;">4. Then take properties of php_mongo.dll and unblock executable.</div><div style="text-align: justify;"><div class="separator" style="clear: both; text-align: center;"><a href="http://4.bp.blogspot.com/-khe1G5wHPYs/UOvbzhvbhjI/AAAAAAAAAjc/7lnV0RqEoFo/s1600/unblock_dll.JPG" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="98" src="https://4.bp.blogspot.com/-khe1G5wHPYs/UOvbzhvbhjI/AAAAAAAAAjc/7lnV0RqEoFo/s320/unblock_dll.JPG" width="320" /></a></div>5. Then go to C:\Program Files (x86)\PHP\v5.3\ and open php.ini as Administrator and add below line to end of the file.<br /><br /><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">extension=php_mongo.dll</span><br /><br />6. Then take a command prompt as administrator and run below command.<br /><br /><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">iisreset</span><br /><br />Enjoy MongoDB with PHP!</div></div>

### Tags

- MongoDB
- mongodb driver
- iis
- mongodb php driver
- php

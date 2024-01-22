---
layout: post
title: Do you want unlimited history in Linux Terminal?
---

<div dir="ltr" style="text-align: left;" trbidi="on"><div style="text-align: justify;">History in Linux terminal is very useful if you get used to it. If you have to ssh long hostname, or long file paths you don't need to type them again and again. You can just grep your history and rip what you want like this.<br /><br />Let's say I want my ssh commands I want to get.</div><div style="text-align: justify;"><blockquote class="tr_bq">history | grep ssh</blockquote></div><div style="text-align: justify;">perhaps maybe smbclient commands</div><div style="text-align: justify;"><blockquote class="tr_bq">history | greb smbclient</blockquote></div><div style="text-align: justify;">By default in Ubuntu Linux History, size is 2000 commands or something like that. That will limit you from accessing your all commands. Then you may feel sick of using history. Solution for that is making you Linux terminal history unlimited. Those days disk space is not much concern so you can save you all the history in a single file without any problem. For 7000 commands it will not take half of a MegaByte at least. Let's see how to make this history unlimited.<br /><br />1. Take a terminal and type below command.<br /><blockquote class="tr_bq">gedit ~/.bashrc</blockquote>or<br /><blockquote class="tr_bq">vi ~/.bashrc</blockquote>2. Then find &nbsp;below lines from gedit or vi<br /><blockquote class="tr_bq">HISTFILESIZE=2000&nbsp;</blockquote><blockquote class="tr_bq">HISTSIZE=2000&nbsp;</blockquote>3. Change delete the number in front of equal.<br /><blockquote class="tr_bq">HISTFILESIZE=&nbsp;</blockquote><blockquote class="tr_bq">HISTSIZE=</blockquote>4. Save it.<br />5. Close and open a terminal again.</div></div>

### Tags

- terminal
- linux
- terminal history

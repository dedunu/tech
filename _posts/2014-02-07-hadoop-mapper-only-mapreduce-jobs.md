---
layout: post
title: Hadoop Mapper only MapReduce jobs
---

<div dir="ltr" style="text-align: left;" trbidi="on">It's funny! You can have mapper only Hadoop MapReduce Jobs. This would be useful sometime when you need to change the structure of data. Otherwise, you can use this way when to want to filter out data. But I don't think you will need this much often.<br /><br />The first file is a simple mapper which really does nothing. You can change it as you want. You can see in the main method&nbsp;<span class="n" style="color: #333333; font-family: &quot;consolas&quot; , &quot;liberation mono&quot; , &quot;courier&quot; , monospace; font-size: 12px; line-height: 16.799999237060547px; white-space: pre;">job</span><span class="o" style="font-family: &quot;consolas&quot; , &quot;liberation mono&quot; , &quot;courier&quot; , monospace; font-size: 12px; font-weight: bold; line-height: 16.799999237060547px; white-space: pre;">.</span><span class="na" style="color: teal; font-family: &quot;consolas&quot; , &quot;liberation mono&quot; , &quot;courier&quot; , monospace; font-size: 12px; line-height: 16.799999237060547px; white-space: pre;">setNumReduceTasks</span><span class="o" style="font-family: &quot;consolas&quot; , &quot;liberation mono&quot; , &quot;courier&quot; , monospace; font-size: 12px; font-weight: bold; line-height: 16.799999237060547px; white-space: pre;">(</span><span class="mi" style="color: #009999; font-family: &quot;consolas&quot; , &quot;liberation mono&quot; , &quot;courier&quot; , monospace; font-size: 12px; line-height: 16.799999237060547px; white-space: pre;">0</span><span class="o" style="font-family: &quot;consolas&quot; , &quot;liberation mono&quot; , &quot;courier&quot; , monospace; font-size: 12px; font-weight: bold; line-height: 16.799999237060547px; white-space: pre;">); </span>line which set reduce tasks to 0. You can find Maven project on <a href="https://github.com/dedunumax/MapperOnly" target="_blank">GitHub</a></div>

### Tags

- mapreduce
- hadoop
- mapper only mapreduce jobs
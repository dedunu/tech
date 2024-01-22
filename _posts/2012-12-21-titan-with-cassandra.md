---
layout: post
title: "Titan with Cassandra"
---

<div dir="ltr" style="text-align: left;" trbidi="on">In<a href="http://www.dedunu.info/2012/12/getting-started-with-titan-graph.html" target="_blank"> a previous blog post about Titan</a>, I mentioned about Titan supports three different storage back ends. For this, you need Titan and Cassandra both.<br /><ul><li><a href="http://cassandra.apache.org/" target="_blank">Download Cassandra Here</a></li><li><a href="http://thinkaurelius.github.com/titan/" target="_blank">Download Titan Here</a></li></ul>Then extract Cassandra and Titan both into a folder and take a terminal or a command prompt. Go to Cassandra bin and run cassandra.bat or Cassandra. Before this, you have to set JAVA_HOME.<br /><br />Linux:<br /><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">bash cassandra</span></blockquote><br />Windows:<br /><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">cassandra.bat</span></blockquote><br />Then take gremlin from titan bin.<br /><br />Linux:<br /><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">bash gremlin.sh</span></blockquote>Windows:<br /><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">gremlin.bat</span></blockquote>Then you have to configure storage backend. for that use following commands on gremlin.<br /><blockquote class="tr_bq"><br /><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">cnf = new BaseConfiguration();</span><br /><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">cnf.setProperty('storage.backend','cassandra');</span><br /><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">cnf.setProperty('storage.hostname','127.0.0.1');</span><br /><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">g = TitanFactory.open(cnf);</span></blockquote>Now rest is your graph database experience!!! </div>

### Tags

- Titan DB
- Configure Storage Backend
- Titan and Cassandra
- Graph DB
- Cassandra
- Graph database
- Titan

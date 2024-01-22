---
layout: post
title: "After renaming I can't access MongoDB collection! :("
---

<div dir="ltr" style="text-align: left;" trbidi="on"><div style="text-align: justify;">Yesterday while I was doing some test for the performance team, I renamed a collection. Actually, I renamed system.profile into "Profiling_28-08-2013". Then I couldn't access it. I couldn't delete that collection use db.Profiling_28-08-2013.drop(). After renaming MongoDB shell can't access that object.&nbsp;</div><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">1. JavaScript execution failed: ReferenceError:&nbsp;&lt;Part of collection name&gt;&nbsp;is not defined</span></blockquote><blockquote class="tr_bq">&nbsp;<span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">2. JavaScript execution failed: SyntaxError: Unexpected token ILLEGAL</span></blockquote><blockquote class="tr_bq">&nbsp;<span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">3. &lt;Part of collection name&gt; is not a legal ECMA-262 octal constant (shell):1</span></blockquote><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">&nbsp;4. SyntaxError: missing ; before statement (shell):1</span></blockquote><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">&nbsp;5. ReferenceError:&nbsp;&lt;Part of collection name&gt;&nbsp;is not defined (shell):1</span></blockquote><div style="text-align: justify;">Those errors I got by trying a combination against MongoDB several versions. First two errors I got from &nbsp;MongoDB 2.4 and the rest from MongoDB 2.2.</div><div style="text-align: justify;"><br /></div><div style="text-align: justify;">If you have "-" inside your new collection name without any numbers you will get the first error. Rest errors you will only get if you have "-08" like parts in your collection names.</div><div class="separator" style="clear: both; text-align: center;"><br /></div><table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;"><a href="http://2.bp.blogspot.com/-7ztbtKLg4qI/Uh7GI63bFoI/AAAAAAAAAz4/oboeQv3egm8/s1600/Screenshot+from+2013-08-29+09:24:12.png" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="165" src="https://2.bp.blogspot.com/-7ztbtKLg4qI/Uh7GI63bFoI/AAAAAAAAAz4/oboeQv3egm8/s400/Screenshot+from+2013-08-29+09:24:12.png" width="400" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">MongoDB version 2.4.3 Shell version 2.4.3</td></tr></tbody></table><table align="center" cellpadding="0" cellspacing="0" class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;"><tbody><tr><td style="text-align: center;"><a href="http://2.bp.blogspot.com/-_ZS0uRvZfKY/Uh7GhL5oVAI/AAAAAAAAA0A/ZMAFekxR_3Q/s1600/Screenshot+from+2013-08-29+09:26:41.png" imageanchor="1" style="margin-left: auto; margin-right: auto;"><img border="0" height="91" src="https://2.bp.blogspot.com/-_ZS0uRvZfKY/Uh7GhL5oVAI/AAAAAAAAA0A/ZMAFekxR_3Q/s400/Screenshot+from+2013-08-29+09:26:41.png" width="400" /></a></td></tr><tr><td class="tr-caption" style="text-align: center;">MongoDB version 2.2.3 Shell version 2.2.3</td></tr></tbody></table><div style="text-align: justify;"><br /></div><div style="text-align: justify;">Now you may want to get rid of those collections or you may want precious data in that collection. You can use runCommand to rename those collections or to drop them.</div><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">db.runCommand({drop:"test.Profiling_28-08-2013"});<br />db.runCommand({drop:"test.post-old"});</span></blockquote><div style="text-align: justify;">Rename commands you may have to run against the admin database. For rename, you may have to use the complete namespace. But dropping you can do with just collection name. It is recommended to use namespace when you are dropping.</div><blockquote class="tr_bq"><span style="font-family: &quot;courier new&quot; , &quot;courier&quot; , monospace;">db.runCommand({ renameCollection: "test.Profiling_28-08-2013", to: "test.newCol"});<br />db.runCommand({ renameCollection: "test.post-old", to: "test.newCol"});</span></blockquote></div>

### Tags

- mongo
- MongoDB Shell
- Mongo Shell
- mongodb administration
- mongodb errors
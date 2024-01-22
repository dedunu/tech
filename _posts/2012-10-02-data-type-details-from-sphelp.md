---
layout: post
title: Data Type details from sphelp
---

I wanted to learn about data types. Then I went to TechNet somehow most of the important things were there in TechNet documentation. But I found another way to get figures from SQL Server. We can have details of data types from “sphelp”. You just have to give your data type as a parameter like below.

```sql
EXEC sp_help int
```

Then I executed this to every data type except few system data types. And I listed figures on categories which was in TechNet.

**Exact Numerics**

<table border="0" cellpadding="2" cellspacing="0" style="width: 721px;"><tbody><tr><td valign="top" width="183"><strong>Type Name</strong></td><td valign="top" width="154"><strong>Length</strong></td><td valign="top" width="138"><strong>Precision</strong></td><td valign="top" width="126"><strong>Scale</strong></td><td valign="top" width="118"><strong>Nullable</strong></td></tr><tr><td valign="top" width="217">bigint</td><td valign="top" width="186">8</td><td valign="top" width="174">19</td><td valign="top" width="154">0</td><td valign="top" width="151">Y</td></tr><tr><td valign="top" width="207">bit</td><td valign="top" width="189">1</td><td valign="top" width="188">1</td><td valign="top" width="164">Null</td><td valign="top" width="167">Y</td></tr><tr><td valign="top" width="200">decimal</td><td valign="top" width="185">17</td><td valign="top" width="192">38</td><td valign="top" width="167">38</td><td valign="top" width="175">Y</td></tr><tr><td valign="top" width="198">int</td><td valign="top" width="183">4</td><td valign="top" width="193">10</td><td valign="top" width="167">0</td><td valign="top" width="178">Y</td></tr><tr><td valign="top" width="197">money</td><td valign="top" width="183">8</td><td valign="top" width="193">19</td><td valign="top" width="167">4</td><td valign="top" width="180">Y</td></tr><tr><td valign="top" width="196">numeric</td><td valign="top" width="183">17</td><td valign="top" width="193">38</td><td valign="top" width="167">38</td><td valign="top" width="180">Y</td></tr><tr><td valign="top" width="196">smallint</td><td valign="top" width="183">2</td><td valign="top" width="193">5</td><td valign="top" width="167">0</td><td valign="top" width="180">Y</td></tr><tr><td valign="top" width="196">smallmoney</td><td valign="top" width="183">4</td><td valign="top" width="193">10</td><td valign="top" width="167">4</td><td valign="top" width="180">Y</td></tr><tr><td valign="top" width="196">tinyint</td><td valign="top" width="183">1</td><td valign="top" width="193">3</td><td valign="top" width="167">0</td><td valign="top" width="180">Y</td></tr></tbody></table>

**Approximate Numerics**

<table border="0" cellpadding="2" cellspacing="0" style="width: 721px;"><tbody><tr><td valign="top" width="183"><strong>Type Name</strong></td><td valign="top" width="154"><strong>Length</strong></td><td valign="top" width="138"><strong>Precision</strong></td><td valign="top" width="126"><strong>Scale</strong></td><td valign="top" width="118"><strong>Nullable</strong></td></tr><tr><td valign="top" width="217">float</td><td valign="top" width="186">8</td><td valign="top" width="174">53</td><td valign="top" width="154">Null</td><td valign="top" width="151">Y</td></tr><tr><td valign="top" width="207">real</td><td valign="top" width="189">4</td><td valign="top" width="188">24</td><td valign="top" width="164">Null</td><td valign="top" width="167">Y</td></tr></tbody></table>

**Date and Time**
	
<table border="0" cellpadding="2" cellspacing="0" style="width: 721px;"><tbody><tr><td valign="top" width="183"><strong>Type Name</strong></td><td valign="top" width="154"><strong>Length</strong></td><td valign="top" width="138"><strong>Precision</strong></td><td valign="top" width="126"><strong>Scale</strong></td><td valign="top" width="118"><strong>Nullable</strong></td></tr><tr><td valign="top" width="217">date</td><td valign="top" width="186">3</td><td valign="top" width="174">10</td><td valign="top" width="154">0</td><td valign="top" width="151">Y</td></tr><tr><td valign="top" width="207">datetime2</td><td valign="top" width="189">8</td><td valign="top" width="188">27</td><td valign="top" width="164">7</td><td valign="top" width="167">Y</td></tr><tr><td valign="top" width="200">datetime</td><td valign="top" width="185">8</td><td valign="top" width="192">23</td><td valign="top" width="167">3</td><td valign="top" width="175">Y</td></tr><tr><td valign="top" width="198">datetimeoffset</td><td valign="top" width="183">10</td><td valign="top" width="193">34</td><td valign="top" width="167">7</td><td valign="top" width="178">Y</td></tr><tr><td valign="top" width="197">smalldatetime</td><td valign="top" width="183">4</td><td valign="top" width="193">16</td><td valign="top" width="167">0</td><td valign="top" width="180">Y</td></tr><tr><td valign="top" width="196">time</td><td valign="top" width="183">5</td><td valign="top" width="193">16</td><td valign="top" width="167">7</td><td valign="top" width="180">Y</td></tr></tbody></table>

**Binary Strings**

<table border="0" cellpadding="2" cellspacing="0" style="width: 721px;"><tbody><tr><td valign="top" width="183"><strong>Type Name</strong></td><td valign="top" width="154"><strong>Length</strong></td><td valign="top" width="138"><strong>Precision</strong></td><td valign="top" width="126"><strong>Scale</strong></td><td valign="top" width="118"><strong>Nullable</strong></td></tr><tr><td valign="top" width="217">binary</td><td valign="top" width="186">8000</td><td valign="top" width="174">8000</td><td valign="top" width="154">Null</td><td valign="top" width="151">Y</td></tr><tr><td valign="top" width="207">image</td><td valign="top" width="189">16</td><td valign="top" width="188">2147483647</td><td valign="top" width="164">Null</td><td valign="top" width="167">Y</td></tr><tr><td valign="top" width="200">varbinary</td><td valign="top" width="185">8000</td><td valign="top" width="192">8000</td><td valign="top" width="167">Null</td><td valign="top" width="175">Y</td></tr></tbody></table>

**Character Strings**

<table border="0" cellpadding="2" cellspacing="0" style="width: 869px;"><tbody><tr><td valign="top" width="318"><strong>Type Name</strong></td><td valign="top" width="269"><strong>Length</strong></td><td valign="top" width="280"><strong>Precision</strong></td></tr><tr><td valign="top" width="330">char</td><td valign="top" width="284">8000</td><td valign="top" width="296">8000</td></tr><tr><td valign="top" width="326">varchar</td><td valign="top" width="288">8000</td><td valign="top" width="305">8000</td></tr><tr><td valign="top" width="323">text</td><td valign="top" width="288">16</td><td valign="top" width="309">2147483647</td></tr></tbody></table>

**Unicode Character Strings**

<table border="0" cellpadding="2" cellspacing="0" style="width: 869px;"><tbody><tr><td valign="top" width="318"><strong>Type Name</strong></td><td valign="top" width="269"><strong>Length</strong></td><td valign="top" width="280"><strong>Precision</strong></td></tr><tr><td valign="top" width="330">nchar</td><td valign="top" width="284">8000</td><td valign="top" width="296">4000</td></tr><tr><td valign="top" width="326">nvarchar</td><td valign="top" width="288">8000</td><td valign="top" width="305">4000</td></tr><tr><td valign="top" width="323">ntext</td><td valign="top" width="288">16</td><td valign="top" width="309">1073741823</td></tr></tbody></table>

**Other Data Types**

<table border="0" cellpadding="2" cellspacing="0" style="width: 890px;"><tbody><tr><td valign="top" width="249"><strong>Type Name</strong></td><td valign="top" width="218"><strong>Length</strong></td><td valign="top" width="220"><strong>Precision</strong></td><td valign="top" width="201"><strong>Nullable</strong></td></tr><tr><td valign="top" width="248">hierarchyid</td><td valign="top" width="225">892</td><td valign="top" width="231">892</td><td valign="top" width="212">Y</td></tr><tr><td valign="top" width="241">sql_variant</td><td valign="top" width="225">8016</td><td valign="top" width="235">0</td><td valign="top" width="218">Y</td></tr><tr><td valign="top" width="240">timestamp</td><td valign="top" width="223">8</td><td valign="top" width="236">8</td><td valign="top" width="221">N</td></tr><tr><td valign="top" width="239">uniqueidentifier</td><td valign="top" width="223">16</td><td valign="top" width="236">16</td><td valign="top" width="222">Y</td></tr><tr><td valign="top" width="239">xml</td><td valign="top" width="222">-1</td><td valign="top" width="236">-1</td><td valign="top" width="222">Y</td></tr></tbody></table>

If I haven’t specified any attribute of those data types usually they have their default values. One special thing was there was only one data type which was not nullable. It is “timestamp”. And I was unable to take data of cursor and table from this method.

### Tags

- Data Types
- English
- Architecture
- SQL Server

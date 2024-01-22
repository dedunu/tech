---
layout: post
title: PostgreSQL 12 - pset format option
---

Postgres 12 has introduced a new format in psql CLI. There are 9 types available. They are listed below.

- aligned 
- asciidoc
- csv
- html 
- latex 
- latex-longtable
- troff-ms
- unaligned
- wrapped

For more information look -> [https://www.postgresql.org/docs/12/app-psql.html](https://www.postgresql.org/docs/12/app-psql.html)

Let's check each format. An example of `aligned` is shown here. This is not good with a wide table/output. It can overflow. Less readable. This is the default format.

```sql
blipsnchitz=# \pset format aligned
Output format is aligned.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;
          name           |  setting   | unit |              category               |                              short_desc                              
-------------------------+------------+------+-------------------------------------+----------------------------------------------------------------------
 allow_system_table_mods | off        |      | Developer Options                   | Allows modifications of the structure of system tables.
 application_name        | psql       |      | Reporting and Logging / What to Log | Sets the application name to be reported in statistics and logs.
 archive_cleanup_command |            |      | Write-Ahead Log / Archive Recovery  | Sets the shell command that will be executed at every restart point.
 archive_command         | (disabled) |      | Write-Ahead Log / Archiving         | Sets the shell command that will be called to archive a WAL file.
 archive_mode            | off        |      | Write-Ahead Log / Archiving         | Allows archiving of WAL files using archive_command.
(5 rows)

blipsnchitz=# 
```

`unaligned` doesn't use tabs. Hard to read.

```sql
blipsnchitz=# \pset format unaligned
Output format is unaligned.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;
name|setting|unit|category|short_desc
allow_system_table_mods|off||Developer Options|Allows modifications of the structure of system tables.
application_name|psql||Reporting and Logging / What to Log|Sets the application name to be reported in statistics and logs.
archive_cleanup_command|||Write-Ahead Log / Archive Recovery|Sets the shell command that will be executed at every restart point.
archive_command|(disabled)||Write-Ahead Log / Archiving|Sets the shell command that will be called to archive a WAL file.
archive_mode|off||Write-Ahead Log / Archiving|Allows archiving of WAL files using archive_command.
(5 rows)
blipsnchitz=# 
```

`wrapped` is useful if your table fit into your terminal width. Otherwise, it does poorly.

```sql
blipsnchitz=# \pset format wrapped
Output format is wrapped.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;
         name         | setting | unit |            category            |                  short_desc                   
----------------------+---------+------+--------------------------------+-----------------------------------------------
 allow_system_table_m.| off     |      | Developer Options              | Allows modifications of the structure of syst.
.ods                  |         |      |                                |.em tables.
 application_name     | psql    |      | Reporting and Logging / What t.| Sets the application name to be reported in s.
                      |         |      |.o Log                          |.tatistics and logs.
 archive_cleanup_comm.|         |      | Write-Ahead Log / Archive Reco.| Sets the shell command that will be executed .
.and                  |         |      |.very                           |.at every restart point.
 archive_command      | (disabl.|      | Write-Ahead Log / Archiving    | Sets the shell command that will be called to.
                      |.ed)     |      |                                |. archive a WAL file.
 archive_mode         | off     |      | Write-Ahead Log / Archiving    | Allows archiving of WAL files using archive_c.
                      |         |      |                                |.ommand.
(5 rows)

blipsnchitz=# 
```

This is the flashy new feature. I love it! It can be used to export too! Follows [the RFC 4180](https://tools.ietf.org/html/rfc4180).

```sql
blipsnchitz=# \pset format csv
Output format is csv.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;
name,setting,unit,category,short_desc
allow_system_table_mods,off,,Developer Options,Allows modifications of the structure of system tables.
application_name,psql,,Reporting and Logging / What to Log,Sets the application name to be reported in statistics and logs.
archive_cleanup_command,,,Write-Ahead Log / Archive Recovery,Sets the shell command that will be executed at every restart point.
archive_command,(disabled),,Write-Ahead Log / Archiving,Sets the shell command that will be called to archive a WAL file.
archive_mode,off,,Write-Ahead Log / Archiving,Allows archiving of WAL files using archive_command.
blipsnchitz=# 
```

`psql` supports few markup languages. An example of `html` is shown here.

```sql
blipsnchitz=# \pset format html
Output format is html.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;
<table border="1">
  <tr>
    <th align="center">name</th>
    <th align="center">setting</th>
    <th align="center">unit</th>
    <th align="center">category</th>
    <th align="center">short_desc</th>
  </tr>
  <tr valign="top">
    <td align="left">allow_system_table_mods</td>
    <td align="left">off</td>
    <td align="left">&nbsp; </td>
    <td align="left">Developer Options</td>
    <td align="left">Allows modifications of the structure of system tables.</td>
  </tr>
  <tr valign="top">
    <td align="left">application_name</td>
    <td align="left">psql</td>
    <td align="left">&nbsp; </td>
    <td align="left">Reporting and Logging / What to Log</td>
    <td align="left">Sets the application name to be reported in statistics and logs.</td>
  </tr>
  <tr valign="top">
    <td align="left">archive_cleanup_command</td>
    <td align="left">&nbsp; </td>
    <td align="left">&nbsp; </td>
    <td align="left">Write-Ahead Log / Archive Recovery</td>
    <td align="left">Sets the shell command that will be executed at every restart point.</td>
  </tr>
  <tr valign="top">
    <td align="left">archive_command</td>
    <td align="left">(disabled)</td>
    <td align="left">&nbsp; </td>
    <td align="left">Write-Ahead Log / Archiving</td>
    <td align="left">Sets the shell command that will be called to archive a WAL file.</td>
  </tr>
  <tr valign="top">
    <td align="left">archive_mode</td>
    <td align="left">off</td>
    <td align="left">&nbsp; </td>
    <td align="left">Write-Ahead Log / Archiving</td>
    <td align="left">Allows archiving of WAL files using archive_command.</td>
  </tr>
</table>
<p>(5 rows)<br />
</p>
blipsnchitz=# 
```

`asciidoc` is shown here.

```sql
blipsnchitz=# \pset format asciidoc
Output format is asciidoc.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;

[options="header",cols="<l,<l,<l,<l,<l",frame="none"]
|====
^l|name ^l|setting ^l|unit ^l|category ^l|short_desc
|allow_system_table_mods |off |  |Developer Options |Allows modifications of the structure of system tables.
|application_name |psql |  |Reporting and Logging / What to Log |Sets the application name to be reported in statistics and logs.
|archive_cleanup_command |  |  |Write-Ahead Log / Archive Recovery |Sets the shell command that will be executed at every restart point.
|archive_command |(disabled) |  |Write-Ahead Log / Archiving |Sets the shell command that will be called to archive a WAL file.
|archive_mode |off |  |Write-Ahead Log / Archiving |Allows archiving of WAL files using archive_command.
|====

....
(5 rows)
....
blipsnchitz=# 
```

`latex` looks like this.

```sql
blipsnchitz=# \pset format latex
Output format is latex.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;
\begin{tabular}{l | l | l | l | l}
\textit{name} & \textit{setting} & \textit{unit} & \textit{category} & \textit{short\_desc} \\
\hline
allow\_system\_table\_mods & off &  & Developer Options & Allows modifications of the structure of system tables. \\
application\_name & psql &  & Reporting and Logging / What to Log & Sets the application name to be reported in statistics and logs. \\
archive\_cleanup\_command &  &  & Write-Ahead Log / Archive Recovery & Sets the shell command that will be executed at every restart point. \\
archive\_command & (disabled) &  & Write-Ahead Log / Archiving & Sets the shell command that will be called to archive a WAL file. \\
archive\_mode & off &  & Write-Ahead Log / Archiving & Allows archiving of WAL files using archive\_command. \\
\end{tabular}

\noindent (5 rows) \\

blipsnchitz=# 
```

`latex-longtable` uses different packages.

```sql
blipsnchitz=# \pset format latex-longtable
Output format is latex-longtable.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;
\begin{longtable}{l | l | l | l | l}
\small\textbf{\textit{name}} & \small\textbf{\textit{setting}} & \small\textbf{\textit{unit}} & \small\textbf{\textit{category}} & \small\textbf{\textit{short\_desc}} \\
\midrule
\endfirsthead
\small\textbf{\textit{name}} & \small\textbf{\textit{setting}} & \small\textbf{\textit{unit}} & \small\textbf{\textit{category}} & \small\textbf{\textit{short\_desc}} \\
\midrule
\endhead
\raggedright{allow\_system\_table\_mods}
&
\raggedright{off}
&
\raggedright{}
&
\raggedright{Developer Options}
&
\raggedright{Allows modifications of the structure of system tables.} \tabularnewline
\raggedright{application\_name}
&
\raggedright{psql}
&
\raggedright{}
&
\raggedright{Reporting and Logging / What to Log}
&
\raggedright{Sets the application name to be reported in statistics and logs.} \tabularnewline
\raggedright{archive\_cleanup\_command}
&
\raggedright{}
&
\raggedright{}
&
\raggedright{Write-Ahead Log / Archive Recovery}
&
\raggedright{Sets the shell command that will be executed at every restart point.} \tabularnewline
\raggedright{archive\_command}
&
\raggedright{(disabled)}
&
\raggedright{}
&
\raggedright{Write-Ahead Log / Archiving}
&
\raggedright{Sets the shell command that will be called to archive a WAL file.} \tabularnewline
\raggedright{archive\_mode}
&
\raggedright{off}
&
\raggedright{}
&
\raggedright{Write-Ahead Log / Archiving}
&
\raggedright{Allows archiving of WAL files using archive\_command.} \tabularnewline
\end{longtable}
blipsnchitz=# 
```

`troff-ms` is the format used in `man` pages.

```sql
blipsnchitz=# \pset format troff-ms
Output format is troff-ms.
blipsnchitz=# 
blipsnchitz=# SELECT name, setting, unit, category, short_desc FROM pg_settings LIMIT 5;
.LP
.TS
center;
l | l | l | l | l.
\fIname\fP	\fIsetting\fP	\fIunit\fP	\fIcategory\fP	\fIshort_desc\fP
_
allow_system_table_mods	off		Developer Options	Allows modifications of the structure of system tables.
application_name	psql		Reporting and Logging / What to Log	Sets the application name to be reported in statistics and logs.
archive_cleanup_command			Write-Ahead Log / Archive Recovery	Sets the shell command that will be executed at every restart point.
archive_command	(disabled)		Write-Ahead Log / Archiving	Sets the shell command that will be called to archive a WAL file.
archive_mode	off		Write-Ahead Log / Archiving	Allows archiving of WAL files using archive_command.
.TE
.DS L
(5 rows)
.DE
blipsnchitz=# 
```

### Tags
- postgres
- postgresql
- psql
- pset
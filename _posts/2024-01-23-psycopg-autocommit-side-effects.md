---
layout: post
title: "Psycopg causing issues without autocommit"
---

I have seen this couple of times in the last five years. When we write adhoc Python scripts using Psycopg2 without `autocommit=True`, you may see wierd spikes on your idle on transaction like below.

![](/resources/21.png)

I also have seen idle_in_transaction goes to days in one instance too. That will stop auto-vaccuum. It will cause a lot of issues and slow down your database. When you use Psycopg, Make sure you have autocommit=True or you commit manually.

![](/resources/22.png)

### Reference

- [https://www.psycopg.org/docs/connection.html#connection.commit](https://www.psycopg.org/docs/connection.html#connection.commit)

### Tags 

- postgres
- database
- python

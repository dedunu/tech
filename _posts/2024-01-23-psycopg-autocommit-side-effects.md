---
layout: post
title: "Psycopg causing issues without autocommit"
---

We use `psycopg2` package to write ad-hoc jobs in Python. But this can lead to serious problem in production environments.

I have seen this couple of times in the last five years. When we write adhoc Python scripts using Psycopg2 without `autocommit=True`, you may see wierd spikes on your idle on transaction like below. This was a batch job. It was running every 10 seconds. If your batch job is not closing connections or restarting from the scratch, your `SELECT` queries might see very old versions of the data. We have to be very careful with this. As it can cause data loss too.

![](/resources/21.png)

I also have seen `idle_in_transaction_max_time` goes to days in one instance too. That will stop `auto-vaccuum` doing its work. It will cause a lot of issues and slow down your database. When you use Psycopg, Make sure you have `autocommit=True` or you commit manually. You can see the warning on the documentation too.

![](/resources/22.png)

### Reference

- [https://www.psycopg.org/docs/connection.html#connection.commit](https://www.psycopg.org/docs/connection.html#connection.commit)

### Tags 

- postgres
- database
- python

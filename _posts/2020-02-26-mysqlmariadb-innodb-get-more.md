---
layout: post
title: "MySQL/MariaDB: InnoDB - Get more information about current transaction"
---

I wanted to find out how many rows were modified by the current transaction. Seems like MariaDB doesn't have a straight forward way to retrieve the transaction ID. To narrow down transactions I used the current connection as the thread ID. You can run the below command to check the information about the transaction. 

```sql
SELECT * 
FROM information_schema.innodb_trx 
WHERE trx_mysql_thread_id = CONNECTION_ID() \G
```

Here is an example:

> Missing Images

### Tags

- mysql
- mariadb
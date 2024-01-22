---
layout: post
title: "How to reset replication in MySQL/MariaDB RDS?"
---

`RESET SLAVE;` doesn't work in AWS MySQL RDS. You should use the below command to stop replication.

```sql
CALL mysql.rds_reset_external_master;
```

 You will see something like an error message. You can safely ignore that. Try `SLAVE STATUS\G`. If you get an empty set, your instance has successfully reset the replication.

 ### Tags

 - mysql
- rds
- replication
- mariadb
- aws
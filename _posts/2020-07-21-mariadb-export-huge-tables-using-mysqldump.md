---
layout: post
title: "MariaDB: Export huge tables using mysqldump"
---

Have you ever gotten this error when you are trying to export huge tables using `mysqldump`?

```console
mysqldump: Error 1969: Query execution was interrupted (max_statement_time exceeded) when dumping table `table_name` at row: 999999999
```

You can try using the `--quick` option. It exported more than double the amount of records, but still failed with the same error. 

```bash
$ mysqldump --quick  database_name table_name > some_file.sql
```

To overcome this problem, I had to extend the `max_statement_time` for the user using the below command.

```sql
GRANT USAGE ON *.* TO some_user@'%' WITH MAX_STATEMENT_TIME 43200;
GRANT SELECT ON database_name.table_name TO some_user@'%';
```

I exported the table using the configured user successfully. 

```bash
$ mysqldump -u some_user -p --quick database_name table_name > some_file.sql
```

### Tags

- mariadb
- mysql
- dump
- export
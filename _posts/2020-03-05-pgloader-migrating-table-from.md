---
layout: post
title: "pgloader: Migrating a table from MySQL/MariaDB to PostgreSQL"
---

`pgloader` is a helpful tool if you want to migrate tables from MySQL/MariaDB to Postgres. This works with AWS RDS instances too.

```sql
LOAD DATABASE
     FROM mysql://<mysql_user>:<mysql_password>@<mysql_host>/<source_databases>
     INTO pgsql://<postgres_user>:<postgres_password>@<postgres_host>/<target_database>

  WITH INCLUDE DROP, CREATE TABLES

  SET search_path to 'public'

  INCLUDING ONLY TABLE NAMES MATCHING 'sample_table'

  ALTER TABLE NAMES MATCHING 'sample_table' RENAME TO 'tmp_sample_table'
  ALTER SCHEMA '<source_databases>' RENAME TO 'public';
```

Let's say we need to migrate the `user` table from MySQL to PostgreSQL. Your `pgloader` file would look like below.

```sql
LOAD DATABASE
     FROM mysql://root:Password123@mysqldb.example.com/real_db
     INTO pgsql://postgres:Password456@pgserver101.example.com/adventure_db

  WITH include drop, create tables

  SET search_path to 'public'

  INCLUDING ONLY TABLE NAMES MATCHING 'user'

  ALTER TABLE NAMES MATCHING 'user' RENAME TO 'account'
  ALTER SCHEMA 'real_db' RENAME TO 'public';
  ```

You can use the below command to start the migration

```console
$ pgload user.load
```

### Gists

- <https://gist.github.com/dedunumax/d8b2cdbf0218b03fc0c17289ae27a726>
- <https://gist.github.com/dedunumax/931e113b341cad572f742bfbbd5c670d>

### Tags

- pgloader
- mysql
- rds
- postgres
- mariadb
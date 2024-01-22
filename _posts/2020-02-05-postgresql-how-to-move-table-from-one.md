---
layout: post
title: "PostgreSQL: How to move a table from one schema to another?"
---

I couldn't write anything down for a while. I had to move a table from one schema to another in PostgresSQL. I had to do this on RDS. `pg_dump` and `pg_restore` tools doesn't allow you to change schema when you dump and restore.

The easiest way is running below command:

```sql
ALTER TABLE old_schema.table_you_want_to_move SET SCHEMA new_schema;
```

### Tags

- database
- SQL
- postgres


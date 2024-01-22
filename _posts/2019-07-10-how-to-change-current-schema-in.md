---
layout: post
title: "How to change the current schema in Postgres CLI"
---

If you want to see the current schema you are on.

```sql
SHOW SEARCH_PATH;
```

Normally you might be on the public schema. But if you want to change the current schema, try below command.

```sql
SET SEARCH_PATH TO test;
```

`test` is the name of the schema.

### Tags

- postgres
- psql
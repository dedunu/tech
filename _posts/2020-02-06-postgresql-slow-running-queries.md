---
layout: post
title: "PostgreSQL: Long running query detection"
---

I am writing this post as a note to myself. Every time I want to find slow running queries, I search and open this [medium post](https://medium.com/little-programming-joys/finding-and-killing-long-running-queries-on-postgres-7c4f0449e86d). It is a well written short post which helps me every day. But I wanted to improve that query.   

```sql
SELECT
  pid,
  now() - pg_stat_activity.query_start AS duration,
  query,
  state
FROM pg_stat_activity
WHERE (now() - pg_stat_activity.query_start) > interval '5 minutes' 
ORDER BY duration DESC;
```

As mentioned these are pretty helpful too.

```sql
SELECT pg_cancel_backend(pid);
SELECT pg_terminate_backend(pid);
```

### Gists

- <https://gist.github.com/dedunumax/a0542b83d4d672eabbf7a17a8ed9dac3>

### Tags

- postgres
- performance issue
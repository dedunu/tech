---
layout: post
title: MySQL/MariaDB: Using expressions and conditions in Update
---

I ran a few update queries against a MySQL database. Update command said it updated some records. But data didn't seem to be as we expect. Let's say the table looked like below.

![figure1](https://1.bp.blogspot.com/-9KTej5M8oEw/XUi6iMW6kyI/AAAAAAAAGVU/hKAcrjonH28_rx4E_pOH2GuSRiylYNEZQCLcBGAs/s640/Screenshot%2B2019-08-06%2Bat%2B2.01.47%2BAM.png)

I ran a query which is similar to below.

```sql
UPDATE update_test SET age = 30 AND name = 'John' WHERE id = 1;
```

![figure2](https://1.bp.blogspot.com/-rg4VUo3_WLc/XUi63TcaR6I/AAAAAAAAGVc/I8adjYhRRzYS0e6_s7xEqyopXnFvewZ8gCLcBGAs/s640/Screenshot%2B2019-08-06%2Bat%2B2.01.37%2BAM.png)

MySQL prompt says that it managed to update one row. But if you look at the data after the update query, it will be clear that `age` is not `30` or neither the name is '`John`'. This is because the query is interpreted as an expression.

```sql
UPDATE update_test SET age = (30 AND name = 'John') WHERE id = 1;
```

Let's look at another query.

```sql
UPDATE update_test SET age = 30 AND name = 'Larry' WHERE id = 3;
```

![figure3](https://1.bp.blogspot.com/-Ufk9EdO3CPo/XUi7xwQbqXI/AAAAAAAAGVk/V1a5_c-zoEEB_hdOjmO_wJ9RF8RQBA7-gCLcBGAs/s640/Screenshot%2B2019-08-06%2Bat%2B2.01.29%2BAM.png)

The output says it didn't update any records because age is already 0 and our update query is actually trying to set it as `0`. Replacing `AND` with "`,`" will set both fields.

```sql
UPDATE update_test SET age = 30, name = 'Larry' WHERE id = 3;
```

With this expression evaluation, we can write advance update queries. For example, I am going to update student data. My update query should update the `highest_mark` field from the highest value of `eng_marks` or `sci_marks` field. Both `eng_marks` and `sci_marks` should be higher than `50` too. The query looks like below.

```sql
UPDATE students SET highest_mark = IF(eng_marks > sci_marks, eng_marks, sci_marks) WHERE eng_marks > 50 AND sci_marks > 50;
```

![figure4](https://1.bp.blogspot.com/-IqRvVNQMyiE/XUi9BJKimOI/AAAAAAAAGVs/AG8-JN0sG7YYndSecbXPj0IZmqzamYnDgCLcBGAs/s640/Screenshot%2B2019-08-06%2Bat%2B2.22.03%2BAM.png)

Thanks a lot, Ross for helping to figure this out!

### Tags

- mariadb
- mysql
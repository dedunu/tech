---
layout: post
title: "Be careful if you are using CTE!"
---

[Previously I wrote a post about CTE](https://www.dedunu.info/2012/09/common-table-expressions-cte.html) (Common Table Expressions). And Common Table Expressions are valid for a single statement only. But a single statement can use many CTEs. And statement also should be within the same batch.

```sql
USE AdventureWorks2012
GO

--Defining CTE
WITH ctePerson AS(
    SELECT * 
    FROM Person.Person)
    --First Statement will run 
    SELECT FirstName FROM ctePerson 
    --Second statement will occur an error
    SELECT FirstName FROM ctePerson;
```

And in my previous post, I have mentioned about many CTEs for one statement. And there is another important note that is to be careful when you are naming CTEs. Take a look on below example.

```sql
USE tempdb
GO

--Creating two tables
CREATE TABLE cteSampletbl1(id int,name varchar(50)
)
GO

CREATE TABLE cteSampletbl2(id int,name varchar(50)
)
GO

--Populating tables
INSERT INTO cteSampletbl1 VALUES(1,'Satheeq'),
(2,'Preethi'),
(3,'Dinesh'),
(4,'Angelo')
GO

INSERT INTO cteSampletbl2 VALUES(1,'Shamil'),
(2,'Hasitha'),
(3,'Abhinandana'),
(4,'Susantha')
GO

/*
    This CTE is defined with existing table name without any error
*/
WITH cteSampletbl2AS(
    SELECT * FROM cteSampletbl1)
    --This statement uses CTE
    SELECT * FROM cteSampletbl2
    --This statement uses existing table
    SELECT * FROM cteSampletbl2
--Dropping tables
DROP TABLE cteSampletbl1
DROP TABLE cteSampletbl2
GO
```

Below example it lets us create a CTE with a name of an existing table without any warnings or errors. And it gives priority to CTE in the first statement. Then it uses the existing table in the second statement. So it would be a best practice to use a separate prefix for CTEs. Then take a look into the next sample which is taken from [Dinesh’s](http://dbfriend.blogspot.com/) presentation for [SQL Server Universe Group](http://www.sqlserveruniverse.com/).

```sql
USE tempdb
GO

--Creating two tables
CREATE TABLE cteSampletbl1(id int,name varchar(50))
GO

--Populating tables
INSERT INTO cteSampletbl1 VALUES(1,'Satheeq'),
(2,'Preethi'),
(3,'Dinesh'),
(4,'Angelo')
GO

--This CTE got error
WITH cteSampletbl1AS(
    --Same name could not be used as name and in CTE
    SELECT * FROM cteSampletbl1) 
SELECT * FROM cteSampletbl1
    --This CTE don’t have any error

WITH cteSampletbl1AS(
    --full name of object should provide
    SELECT * FROM dbo.cteSampletbl1)
SELECT * FROM cteSampletbl1

--Dropping tables
DROP TABLE cteSampletbl1GO
```

You can’t use the same table name as the name of the CTE and inside the CTE.

### Tags

- SQL
- CTE
- T-SQL
- TSQL
- SQL Server
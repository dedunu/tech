---
layout: post
title: "Insert in T-SQL"
---

I’m still a beginner in SQL Server.  I  will blog about many basic things in SQL Server. Inserting is very important Data Manipulation Statement. So let's see how to use INSERT Statement in different ways.

```sql
USE tempdb
GO

--Creating Table
CREATE TABLE tmpTable(
    [id] int NOT NULL,
    [name] varchar(100) NULL,
    [address] varchar(1000) NULL
)
GO

--Inserting Data
INSERT INTO tmpTable([id],[name],[address]) VALUES(1, 'John', '123, qwerty')
GO

--Inserting Data by Changing order column
INSERT INTO tmpTable([name],[id],[address]) VALUES('Mark',2, '234, qwerty')
GO

--Inserting Data without specifying columns
INSERT INTO tmpTable VALUES(3,'Steve', '454, qwerty')
GO

--Deleting temp table
DROP TABLE tmpTable
GO
```

Above statements are the basic inserting methods. But it's recommended to specify columns. If you want to change the schema structure later It will not affect your code if you have used INSERT with specified columns. And if you don’t specify columns be careful because you have to provide data for every column.

```sql
USE tempdb
GO

--Creating Table
CREATE TABLE tmpTable(
    [id] int NOT NULL,
    [name] varchar(100) NULL,
    [address] varchar(1000) NULL
)
GO

/*
    If you don't specify column names you have to 
    insert data to every columns you can't skip
    columns
*/

-- This cause a error 'Column name or number of supplied values 
-- does not match table definition.'
INSERT INTO tmpTable VALUES(4,'Gates' )
GO

--Dropping the temp table
DROP TABLE tmpTable
GO
```

**Playing with DEFAULT Values**

Sometimes we need to work with DEFAULT values. Then if you want to let SQL Server decide values you can code like this.

```sql
USE tempdb
GO

--Creating Table
CREATE TABLE tmpTable(
    [name] varchar(100) DEFAULT ('Name'),
    [address] varchar(1000) DEFAULT ('Address')
)
GO

--You can let sql server to add default values by mentioning default 
INSERT INTO tmpTable VALUES('John',default )
GO

INSERT INTO tmpTable VALUES(default,'123 qwerty')
GO

--If you like you can give default values to all the columns too.
INSERT INTO tmpTable VALUES(default,default)
GO

-- You can ignore values for that column. Then you have to 
-- specify column name
INSERT INTO tmpTable([name]) VALUES('Mark')
GO

--Retrieving data
SELECT * FROM tmpTable
GO

--Dropping the temp table
DROP TABLE tmpTable
GO
```

**Inserting data from another table**

In some cases, we need to insert data from one table to another. Then we can use the INSERT statement to copy data from another table.

```sql
USE [AdventureWorks2012]
GO

--Creating a temp table
CREATE TABLE Tmp(
    [BusinessEntityID] [int] NOT NULL,
    [LoginID] [nvarchar](256) NOT NULL,
    [OrganizationNode] [hierarchyid] NULL,
    [JobTitle] [nvarchar](50) NOT NULL,
    [BirthDate] [date] NOT NULL,
    [MaritalStatus] [nchar](1) NOT NULL,
    [Gender] [nchar](1) NOT NULL,
)
GO

--Inserting data from another table
INSERT INTO Tmp
    (
        [BusinessEntityID],    
        [LoginID],
        [OrganizationNode],
        [JobTitle],
        [BirthDate],
        [MaritalStatus],
        [Gender]    
    ) 
    --Selecting data from HumanResources.Employee
    SELECT 
        [BusinessEntityID],
        [LoginID],
        [OrganizationNode],
        [JobTitle],
        [BirthDate],
        [MaritalStatus],
        [Gender]
    FROM HumanResources.Employee
GO

--Retrieving data
SELECT * FROM Tmp
GO

--Dropping Table
DROP TABLE Tmp
GO
```

### Tags

- Insert
- T-SQL
- SQL Server
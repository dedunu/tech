---
layout: post
title: "SELECT INTO"
---

My previous blog post was about [using the `INSERT` command in different ways](https://www.dedunu.info/2012/09/insert-in-t-sql.md). You can use `SELECT INTO` to add data from an existing table to a new table. In this statement, SQL Server will create a table for you. You just want to write the query and add `INTO` clause to the statement. Rest will be done by SQL Server for you.

```sql
USE [AdventureWorks2012]
GO

--Inserting data from HumanResources.Employee to a new table
SELECT  [BusinessEntityID],
        [LoginID],
        [OrganizationNode],
        [JobTitle],
        [BirthDate],
        [MaritalStatus],
        [Gender] 
    INTO Tmp
    FROM HumanResources.Employee
GO

--Retrieving data
SELECT * FROM Tmp
GO

--Dropping Table
DROP TABLE Tmp
GO
```

If you are trying to add data into an existing table by using this `INTO` clause, you will have an error. You can join two tables and add data into the new table too.

```sql
USE [AdventureWorks2012]
GO

-- Inserting data from HumanResources.Employee and 
-- Person.Person to new table
SELECT  HE.[BusinessEntityID],
        HE.[LoginID],
        HE.[Gender],
        PP.[FirstName],
        PP.[NameStyle]
    INTO Tmp
    FROM [HumanResources].[Employee] AS HE
    INNER JOIN Person.Person AS PP
    ON HE.[BusinessEntityID] = PP.[BusinessEntityID]
GO

--Retrieving data
SELECT * FROM Tmp
GO

--Dropping Table
DROP TABLE Tmp
GO
```

And you can use conditions as well.

```sql
USE [AdventureWorks2012]
GO

-- Inserting data from HumanResources.Employee and 
-- Person.Person to new table
SELECT  HE.[BusinessEntityID],
        HE.[LoginID],
        HE.[Gender],
        PP.[FirstName],
        PP.[NameStyle]
    INTO Tmp
    FROM [HumanResources].[Employee] AS HE
    INNER JOIN Person.Person AS PP
    ON HE.[BusinessEntityID] = PP.[BusinessEntityID]
    WHERE HE.[BusinessEntityID] BETWEEN 70 AND 80
GO

--Retrieving data
SELECT * FROM Tmp
GO

--Dropping Table
DROP TABLE Tmp
GO
```

When you are joining two tables consider the column names too. If you are using the same name to two or more columns SQL Server will occur error. Below code will generate such an error.

```sql
USE [AdventureWorks2012]
GO

-- Inserting data from HumanResources.Employee and 
-- Person.Person to new table
SELECT  HE.[BusinessEntityID],
        HE.[LoginID],
        HE.[Gender],
        PP.[BusinessEntityID],
        PP.[FirstName],
        PP.[NameStyle]
    INTO Tmp
    FROM [HumanResources].[Employee] AS HE
    INNER JOIN Person.Person AS PP
    ON HE.[BusinessEntityID] = PP.[BusinessEntityID]
GO

--Retrieving data
SELECT * FROM Tmp
GO

--Dropping Table
DROP TABLE Tmp
GO
```

### Tags

- SQL
- T-SQL
- SELECT
- SQL Server
- INTO
- SELECT INTO
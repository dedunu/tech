---
layout: post
title: Delete using another Table
---

In this example, I create a temp table on `AdventureWorks2012` Database, and first I load all the data in `HumanResources.Employee` to the temporary table. Then I delete data using `HumanResources.Employee`. This command will delete all the records in Tmp which has `Gender = ‘M’` in `HumanResources.Employee` table.

```sql
USE [AdventureWorks2012]
GO

--Inserting data from HumanResources.Employee and Person.Person to non existing table
SELECT  *
    INTO Tmp
    FROM [HumanResources].[Employee] 
GO

--DELETE Using another table
DELETE Tmp 
    FROM [HumanResources].[Employee] AS HE, Tmp
    WHERE Tmp.BusinessEntityID = HE.BusinessEntityID
    AND HE.Gender = 'M'

--Retrieving data
SELECT * FROM Tmp
GO

--Dropping Table
DROP TABLE Tmp
GO
```

You can use an inner or outer join to combine those data.

```sql
USE [AdventureWorks2012]
GO

--Inserting data from HumanResources.Employee and Person.Person to non existing table
SELECT  *
    INTO Tmp
    FROM [HumanResources].[Employee] 
GO

--DELETE Using another table
DELETE Tmp 
    FROM [HumanResources].[Employee] AS HE
    INNER JOIN Tmp
    ON Tmp.BusinessEntityID = HE.BusinessEntityID
    WHERE HE.Gender = 'M'

--Retrieving data
SELECT * FROM Tmp
GO

--Dropping Table
DROP TABLE Tmp
GO
```

### Tags

- SQL
- DELETE
- T-SQL
- TSQL
- SQL Server
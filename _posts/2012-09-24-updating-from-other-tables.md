---
layout: post
title: Updating from other Tables
---

If you want to synchronize data from another table only for once, you can use this way. When you are going to update from another table don’t forget to give a condition.

```sql
USE [AdventureWorks2012]
GO

-- Inserting data from HumanResources.Employee and Person.Person 
-- temporary table
SELECT  *
    INTO Tmp
    FROM [HumanResources].[Employee] 
GO

--Retrieving data
SELECT * FROM Tmp

--Update Using another table
UPDATE Tmp
    SET Tmp.JobTitle = HE.JobTitle + ', updated'
    FROM [HumanResources].[Employee] AS HE
    WHERE Tmp.BusinessEntityID = HE.BusinessEntityID

--Retrieving data
SELECT * FROM Tmp
SELECT * FROM HumanResources.Employee
GO

--Dropping Table
DROP TABLE Tmp
GO
```

If you don’t specify a condition for update it will update all the rows with one value. For example, if you run below code you will see the difference.

```sql
USE [AdventureWorks2012]
GO

--Inserting data from HumanResources.Employee and Person.Person to non existing table
SELECT  *
    INTO Tmp
    FROM [HumanResources].[Employee] 
GO

--Retrieving data
SELECT * FROM Tmp

--Update Using another table
UPDATE Tmp
    SET Tmp.JobTitle = HE.JobTitle + ', updated'
    FROM [HumanResources].[Employee] AS HE
    --WHERE Tmp.BusinessEntityID = HE.BusinessEntityID


--Retrieving data
SELECT * FROM TmpSELECT * FROM HumanResources.Employee
GO

--Dropping Table
DROP TABLE Tmp
GO
```

Also, you can use complex update statement using conditions.

```sql
USE [AdventureWorks2012]
GO

--Inserting data from HumanResources.Employee and Person.Person to non existing table
SELECT  *
    INTO Tmp
    FROM [HumanResources].[Employee] 
GO

--Retrieving data
SELECT * FROM Tmp

--Update Using another table
UPDATE Tmp 
    SET Tmp.JobTitle = HE.JobTitle + ', updated'
    FROM [HumanResources].[Employee] AS HE, Tmp AS T
    WHERE T.BusinessEntityID = HE.BusinessEntityID
    AND HE.Gender = 'M'

--Retrieving data
SELECT * FROM Tmp
SELECT * FROM HumanResources.Employee
GO

--Dropping Table
DROP TABLE Tmp
GO
```

### Tags

- SQL
- T-SQL
- TSQL
- SQL Server
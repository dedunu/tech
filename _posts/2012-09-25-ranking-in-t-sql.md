---
layout: post
title: "Ranking in T-SQL"
---

In Queries, we need to rank and number records. SQL Server gives you a few functions to rank your records.

**RANK**

Rank we can use to rank data in a normal way. In this ranking, if we have two 1 next to one will have rank 3.  


|Name	|	Marks	|	Rank|
|:----- | ---------:| -----:|
|John	|	75		|	1	|
|Mark	|	75		|	1	|
|Steve	|	64		|	3	|
|Gates	|	54		|	4	|


```sql
USE [tempdb]
GO

--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Score]) 
    VALUES ('John',75),('Mark',75),('Steve',64),('Gates',54)
GO

--Ranking data over Score
SELECT *, RANK() OVER (ORDER BY [Score] DESC) AS [RANK] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```

This ranks based on the column that you specify by OVER.

**DENSE_RANK**

Dense Rank is not missing ranks like in normal rank function. It has continuity over ranking.


|Name	|	Marks	| Dense Rank|
|:----- | ---------:| ---------:|
|John	|	75		|	1		|
|Mark	|	75		|	1		|
|Steve	|	64		|	2		|
|Gates	|	54		|	3		|


```sql
USE [tempdb]
GO

--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Score]) 
    VALUES ('John',75),('Mark',75),('Steve',64),('Gates',54)
GO

--Ranking data over Score
SELECT *, DENSE_RANK() OVER (ORDER BY [Score] DESC) AS [DENSE RANK] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```

**ROW NUMBER**

Row Number don’t worry much about ranking it just give an incremental number to row. It’s simple.


|Name	|	Marks	| Row Number|
|:----- | ---------:| ---------:|
|John	|	75		|	1		|
|Mark	|	75		|	2		|
|Steve	|	64		|	3		|
|Gates	|	54		|	4		|


```sql
USE [tempdb]
GO

--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Score]) 
    VALUES ('John',75),('Mark',75),('Steve',64),('Gates',54)
GO

--Numbering data over Score
SELECT *, ROW_NUMBER() OVER (ORDER BY [Score] DESC) AS [ROW NUMBER] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```

**NTile**

`NTile` will separate your code into the number that you parse. If you want to group your results into 3 groups you can use `NTILE(3)`. If you want to divide your results into 7 you can use `NTILE(7)`.


|Name		| Mark	| NTile(3)	|
|:--------- | -----:| ---------:|
|Dedunu		| 89	| 1			|
|Dhananjaya	| 85	| 1			|
|Hasitha	| 75	| 2			|
|Shamil		| 74	| 2			|
|Sanjana	| 65	| 3			|
|Anuradha	| 55	| 3			|


```sql
USE [tempdb]
GO

--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Score]) 
    VALUES ('Dedunu',89),('Dhananjaya',85),('Hasitha',75),('Shamil',74),('Sanjana',65),('Anuradha',55)
GO

--NTile(3) over Score
SELECT *, NTILE(3) OVER (ORDER BY [Score] DESC) AS [NTile(3)] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```

If you are going to group them into 4, you will have this result. It always tries to round to the lower numbers.


|Name		| Mark	| NTile(4)	|
|:--------- | -----:| ---------:|
|Dedunu		| 89	| 1			|
|Dhananjaya	| 85	| 1			|
|Hasitha	| 75	| 2			|
|Shamil		| 74	| 2			|
|Sanjana	| 65	| 3			|
|Anuradha	| 55	| 4			|


```sql
USE [tempdb]
GO

--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Score]) 
    VALUES ('Dedunu',89),('Dhananjaya',85),('Hasitha',75),('Shamil',74),('Sanjana',65),('Anuradha',55)
GO

--NTile(4) over Score
SELECT *, NTILE(4) OVER (ORDER BY [Score] DESC) AS [NTile(4)] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```

Then if you are going to group odd numbered records by even or even numbered records by odd, first tile will have an extra record.


|Name		| Mark	| NTile(5)	|
|:--------- | -----:| ---------:|
|Dedunu		| 89	| 1			|
|Dhananjaya	| 85	| 1			|
|Hasitha	| 75	| 2			|
|Shamil		| 74	| 3			|
|Sanjana	| 65	| 4			|
|Anuradha	| 55	| 5			|


```sql
USE [tempdb]
GO

--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Score]) 
    VALUES ('Dedunu',89),('Dhananjaya',85),('Hasitha',75),('Shamil',74),('Sanjana',65),('Anuradha',55)
GO

--NTile(5) over Score
SELECT *, NTILE(5) OVER (ORDER BY [Score] DESC) AS [NTile(5)] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```

If you are trying to group records by more than records number or same number it will act like `ROW_NUMBER` function. 


|Name		| Mark	| NTile(>=6)	|
|:--------- | -----:| -------------:|
|Dedunu		| 89	| 1				|
|Dhananjaya	| 85	| 2				|
|Hasitha	| 75	| 3				|
|Shamil		| 74	| 4				|
|Sanjana	| 65	| 5				|
|Anuradha	| 55	| 6				|


```sql
USE [tempdb]
GO

--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Score]) 
    VALUES ('Dedunu',89),('Dhananjaya',85),('Hasitha',75),('Shamil',74),('Sanjana',65),('Anuradha',55)
GO

--NTile(6) data over Score
SELECT *, NTILE(6) OVER (ORDER BY [Score] DESC) AS [NTile(6)] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```

```sql
USE [tempdb]
GO
--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Score]) 
    VALUES ('Dedunu',89),('Dhananjaya',85),('Hasitha',75),('Shamil',74),('Sanjana',65),('Anuradha',55)
GO

--NTile(8) over Score
SELECT *, NTILE(8) OVER (ORDER BY [Score] DESC) AS [NTile(8)] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```


**PARTITION BY**

Let's move to `PARTITION BY` clause. If you want to categorize your ranks into any other factor, you can use `PARTITION BY` clause. It lets you have separate rankings on a factor that you want.
	

|Name		| Subject	| Mark	|Rank	|
|:--------- | ---------:| -----:| -----:|
|Hasitha	| Eng		|	75	| 1		|
|Anuradha	| Eng		|	55	| 2		|
|Dedunu		| Math		|	89	| 1		|
|Dhananjaya	| Math		|	85	| 2		|
|Sanjana	| Math		|	65	| 3		|
|Shamil		| Sci		|	74	| 1		|


```sql
USE [tempdb]
GO

--Creating table Marks
CREATE TABLE [MARKS](
    [Name] varchar(25),
    [Subject] varchar(25),
    [Score] int)
GO

--Inserting values into Mark table
INSERT INTO [MARKS]([Name], [Subject], [Score]) 
    VALUES ('Dedunu','Math',89),('Dhananjaya','Math',85),('Hasitha','Eng',75),('Shamil','Sci',74),('Sanjana','Math',65),('Anuradha','Eng',55)
GO

--Partitioning rank by Suject, and ranking over Score
SELECT *, RANK() OVER (PARTITION BY [Subject] ORDER BY [Score] DESC) AS [RANK] FROM MARKS

--Dropping table
DROP TABLE [MARKS]
GO
```

### Tags

- SQL
- PARTITION
- T-SQL
- OVER
- Dense_Rank
- PARTITION BY
- Row_Number
- TSQL
- SQL Server
- Rank
- NTILE

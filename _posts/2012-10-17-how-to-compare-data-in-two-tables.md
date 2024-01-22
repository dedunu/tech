---
layout: post
title: "How to compare data in two tables?"
---

At the beginning of this week, I got a task from [Susantha](http://www.sqlservertorque.com/) to modify a stored procedure. After the modification, I had to test to compare the result sets before modification and after modification. That procedure only returns a data table. So I had so many test data on another table. Then I wrote a script to go through the script one by one. Actually, I wanted to check whether those results are identical. I mean not the table structure. I wanted to perform a data comparison.  

```sql
DECLARE @COUNTN INT;
DECLARE @COUNTO INT;
DECLARE @COUNTU INT; 

CREATE TABLE #TEMPN ( \--Columns Here )  
CREATE TABLE #TEMPO ( \--Columns Here )  
CREATE TABLE #TEMPU ( \--Columns Here )  

INSERT INTO #TEMPN \--Select From new table INSERT INTO #TEMPO \--Select From old table SELECT @COUNTU \= COUNT(1)FROM #TEMPUSELECT @COUNTN \= COUNT(1)FROM #TEMPNSELECT @COUNTO \= COUNT(1)FROM #TEMPO  

IF @COUNTN <> @COUNTO BEGIN  
        SELECT \* FROM #TEMPN SELECT \* FROM #TEMPO PRINT 'ERROR' END  
  
IF @COUNTN <> @COUNTU BEGIN  
        SELECT \* FROM #TEMPN SELECT \* FROM #TEMPO PRINT 'ERROR' END  
  
IF @COUNTU <> @COUNTO BEGIN  
        SELECT \* FROM #TEMPN SELECT \* FROM #TEMPO PRINT 'ERROR' END  
  
DROP TABLE #TEMPNDROP TABLE #TEMPODROP TABLE #TEMPU 
```
  
  
This will check whether your data in two tables are identical or not. if there’s any mismatch it will print an error and show both result sets. And there’s another issue on this script if one table returns NULL and the other table returns empty table it will take it as matched. Then I corrected it again.  

```sql
DECLARE @COUNTN INT;
DECLARE @COUNTO INT;
DECLARE @COUNTU INT;  

CREATE TABLE #TEMPN ( \--Columns Here )  
CREATE TABLE #TEMPO ( \--Columns Here )  
CREATE TABLE #TEMPU ( \--Columns Here ) 

INSERT INTO #TEMPN \--Select From new table INSERT INTO #TEMPO \--Select From old table SELECT @COUNTU \= COUNT(1)FROM #TEMPUSELECT @COUNTN \= COUNT(1)FROM #TEMPNSELECT @COUNTO \= COUNT(1)FROM #TEMPO  

IF @COUNTN <> @COUNTO BEGIN  
        SELECT \* FROM #TEMPN SELECT \* FROM #TEMPO PRINT 'ERROR' END  
  
IF @COUNTN <> @COUNTU BEGIN  
        SELECT \* FROM #TEMPN SELECT \* FROM #TEMPO PRINT 'ERROR' END  
  
IF @COUNTU <> @COUNTO BEGIN  
        SELECT \* FROM #TEMPN SELECT \* FROM #TEMPO PRINT 'ERROR' END  
\--New Code Block here  
  
IF EXISTS(#TEMPO) BEGIN  
        IF NOT EXISTS(#TEMPN) BEGIN  
            SELECT \* FROM #TEMPN SELECT \* FROM #TEMPO PRINT 'ERROR' END  
    END   
  
  
IF EXISTS(#TEMPN) BEGIN  
        IF NOT EXISTS(#TEMPO) BEGIN  
            SELECT \* FROM #TEMPN SELECT \* FROM #TEMPO PRINT 'ERROR' END  
    END 

DROP TABLE #TEMPNDROP TABLE #TEMPODROP TABLE #TEMPU
```

### Tags

- SQL
- Comparing tables
- Table
- Identical Tables
- T-SQL
- TSQL
- Table Compare
- SQL Server
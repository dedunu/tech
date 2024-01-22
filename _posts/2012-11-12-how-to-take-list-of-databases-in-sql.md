---
layout: post
title: "How to take list of databases in SQL Server"
---

In SQLCMD and Powershell I wanted to take the list of databases. In MySQL “show databases” command was there. But in `SQLCMD` I was unable to find such a command.  

```sql
--Stored Procedure
EXEC sp_databases  
GO   
  
--SELECT Statement
SELECT Name FROM master.dbo.sysdatabases  
GO 
```
  
You can use the above commands in SSMS (if you are lazy to move your mouse to object explorer) and SQLCMD. Also, you can use the same thing on PowerShell too.  

```powershell
# Stored Procedure
Invoke-SQLCMD "EXEC sp\_databases"  

# SELECT Statement
Invoke-SQLCMD "SELECT Name FROM master.dbo.sysdatabases"
```

But in SQLPS you can go to your SQL Server instance’s database and just type “dir”.

### Tags

- SQL
- SQLPS
- Powershell
- Administration
- SQLCMD
- SQL Server
- SQL Sever

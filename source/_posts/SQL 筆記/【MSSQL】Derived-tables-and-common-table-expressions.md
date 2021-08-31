---
title: 【MSSQL】Derived tables and common table expressions
categories: SQL 筆記
tags:
  - SQL
  - 筆記
date: 2021-09-01 00:12:26
draft_date: 2021-08-31 23:42:08
layout:
photos:
---

- View
- Temporary Tables
- Table Variable
- Derived Tables
- CTE (Common Table Expression)
<!-- more -->

<br />
<br />

---


# View
views 儲存在 DB，可以用於 query 或 SP，
然而如果 view 只用在一個地方，可以用其他更容易的方式達成，
e.g. CTE、Derived Tables、Temp Tables、Table Variable...etc.

#### EX.
```sql
CREATE view vWEmployeeCount
AS
SELECT DeptName, DepartmentId, COUNT(*) AS TotalEmployees
FROM tblEmployee
JOIN tblDepartment
ON tblEmployee.DepartmentId = tblDepartment.DeptId
GROUP BY DeptName, DepartmentId;

SELECT DeptName, TotalEmployees 
FROM vWEmployeeCount
WHERE TotalEmployees >= 2;
```
<br />
<br />


# Temporary Tables
local temporary tables 只能用於當前 session，也可以在嵌套的 SP 共享；
global temporary tables 可用於其他 sessions，且最後一個 connection 關閉時該 table 也會跟著被刪除

#### EX.
```sql
SELECT DeptName, DepartmentId, COUNT(*) AS TotalEmployees
INTO #TempEmployeeCount
FROM tblEmployee
JOIN tblDepartment
ON tblEmployee.DepartmentId = tblDepartment.DeptId
GROUP BY DeptName, DepartmentId;

SELECT DeptName, TotalEmployees
FROM #TempEmployeeCount
WHERE TotalEmployees >= 2;

-- 用完 temp table 可以刪掉，不刪也會在 session 一結束後自動刪除
DROP TABLE #TempEmployeeCount;
```
<br />
<br />


# Table Variable
table variable 和 temp tables 一樣也是建立於 TempDB，
table variable 的範圍是聲明 batch、SP 或是在其被呼叫的 statement block 內，
可以在 SP 被當作參數傳遞

#### EX.
```sql
DECLARE @tblEmployeeCount TABLE
(DeptName nvarchar(20),DepartmentId int, TotalEmployees int);

INSERT @tblEmployeeCount
SELECT DeptName, DepartmentId, COUNT(*) AS TotalEmployees
FROM tblEmployee
JOIN tblDepartment
ON tblEmployee.DepartmentId = tblDepartment.DeptId
GROUP BY DeptName, DepartmentId;

SELECT DeptName, TotalEmployees
FROM @tblEmployeeCount
WHERE  TotalEmployees >= 2;
```
<br />
<br />


# Derived Tables
derived tables 只能被用於當前的 query

#### EX.
```sql
SELECT DeptName, TotalEmployees
FROM
  (
    SELECT DeptName, DepartmentId, COUNT(*) AS TotalEmployees
    FROM tblEmployee
    JOIN tblDepartment
    ON tblEmployee.DepartmentId = tblDepartment.DeptId
    GROUP BY DeptName, DepartmentId
  ) 
 -- EmployeeCount 是 derived tables name
AS EmployeeCount
WHERE TotalEmployees >= 2;
```
<br />
<br />


# CTE (Common Table Expression)
可以想成是一個被定義在單個`SELECT`, `INSERT`, `UPDATE`, `DELETE`, or `CREATE VIEW` statement 執行範圍內的臨時結果，
和 derived table 相似，兩者都不能被儲存，且僅在查詢時間作用

#### EX.
```sql
-- `(DeptName, DepartmentId, TotalEmployees)`是 option 的
WITH EmployeeCount(DeptName, DepartmentId, TotalEmployees)
AS
  (
  -- CTE 實際會回傳的 columns 由這裡決定
    SELECT DeptName, DepartmentId, COUNT(*) AS TotalEmployees
    FROM tblEmployee
    JOIN tblDepartment
    ON tblEmployee.DepartmentId = tblDepartment.DeptId
    GROUP BY DeptName, DepartmentId
  )

SELECT DeptName, TotalEmployees
FROM EmployeeCount
WHERE TotalEmployees >= 2
```
---
title: 【MSSQL】User-defined functions (UDF)
date: 2021-08-25 16:54:35
draft_date: 2021-08-25 11:18:06
layout:
categories:
tags:
- SQL
- 筆記
photos:
---

- Scalar functions
- Inline table-valued functions
- Multistatement table-valued functions
<!-- more -->

<br />
<br />

---

# Scalar functions
回傳一個 value，且該 value 為 scalar data type，不能回傳 text、ntext、image、cursor、timestamp 型別
SP 和 scalar functions 差在 SP 不能使用於`SELECT`或`WHERE` clause

> _To view the text of the function use `sp_helptext` FunctionName_

#### EX.
```sql
CREATE FUNCTION Function_Name(@Parameter1 DataType, @Parameter2 DataType,..@Parametern Datatype)
RETURNS Return_Datatype
AS
BEGIN
    FUNCTION Body
    RETURN Return_Datatype
END
```
<br />
<br />


# Inline table-valued functions
回傳一個 table，table 回傳的結構取決於`SELECT` clause
因為`SELECT`時是取得 underlying table，所以進行 DML 操作時可能會改到資料

#### 使用時機
- Inline Table Valued functions can be used to achieve the functionality of parameterized views
- `JOIN`其他 table

#### EX.
```sql
CREATE FUNCTION Function_Name(@Param1 DataType, @Param2 DataType..., @ParamN DataType)
RETURNS TABLE
AS
-- 括號只是幫助閱讀
RETURN (Select_Statement)

-- 呼叫
SELECT * FROM Function_Name()
```
<br />
<br />


# Multistatement table-valued functions

#### 效能
Inline table-valued functions 效能較 Multistatement table-valued functions 好
> _Internally, SQL Server treats an inline table valued function much like it would a view and treats a multi-statement table valued function similar to how it would a stored procedure._

#### EX.
```sql
CREATE FUNCTION fn_MSTVF_GetEmployees()
RETURNS @Table TABLE (Id int, Name nvarchar(20), DOB Date)
AS
BEGIN
 INSERT INTO @Table
 SELECT Id, Name, Cast(DateOfBirth AS Date)
 FROM tblEmployees
 
 RETURN
END

-- 呼叫
SELECT * FROM Function_Name()
```
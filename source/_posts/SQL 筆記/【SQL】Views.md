---
title: 【SQL】Views
date: 2021-08-24 21:40:49
layout:
categories: SQL 筆記
tags:
- SQL
- 筆記
photos:
---

用來**儲存 SQL query**，可以看作是 **virtual table**
- Views
- Indexed views
<!-- more -->
<br />
<br />

---

# Views
如果一個 view 是基於多個 tables 建立，更新該 view 時，underlying base tables 可能會無法正確更新，
因此為了正確更新 tables 需要使用`INSTEAD OF`

#### 注意
- view 不能傳參數，但可以使用 inline table-valued functions 作為替代方案

  ```sql
  -- Error : Cannot pass Parameters to Views
  CREATE View vWEmployeeDetails
  @Gender nvarchar(20)
  AS
  SELECT Id, Name, Gender, DepartmentId
  FROM  tblEmployee
  WHERE Gender = @Gender

  -- Inline table-valued functions
  CREATE FUNCTION fnEmployeeDetails(@Gender nvarchar(20))
  RETURNS TABLE
  AS
  RETURN 
  (SELECT Id, Name, Gender, DepartmentId
  FROM tblEmployee WHERE Gender = @Gender)

  Select * from dbo.fnEmployeeDetails('Male')
  ```

- 不能使用`RULES`和`DEFAULTS`，因為 views 本身並沒有儲存 data
- 不能使用`ORDER BY`，除非定義`TOP`或`FOR XML`
- views 不能以 temporary tables 建立
<br />
<br />

# Indexed views

當 view 加入 index 則能夠儲存 data，
執行`SELECT`時不需要再去 base table 取得資料，
若 base table 有進行 transaction 且 commit 時，view 也會跟著重新計算且更新
<!-- more -->

第一次在 view 加入 index，只能用`UNIQUE CLUSTERED INDEX`，
因為 view 本身並沒有儲存任何 data，所以沒辦法用`NON-CLUSTERED INDEX`

#### 用途
**提升效能**

#### 使用時機
**index view 適合使用在 base table data 不會時常改變的時候**

**維護 index view 的成本會高於 table index，
所以 index view 通常使用於 data warehousing**

index view 適合 OLAP system (OnLine Analytical Processing)，
若是使用於 OLTP system (On-Line Transaction Processing system) 可能會影響到效能

#### 注意
> _If GROUP BY is specified, the view select list must contain a `COUNT_BIG(*)` expression, and the view definition cannot specify `HAVING`, `ROLLUP`, `CUBE`, or `GROUPING SETS`._

#### 參考連結
- [Creating Indexed Views](https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms191432(v=sql.105)?redirectedfrom=MSDN)
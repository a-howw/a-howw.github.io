---
title: 【MSSQL】Important concepts related to functions
tags:
  - SQL
  - 筆記
date: 2021-08-25 23:34:03
draft_date: 2021-08-25 17:48:38
layout:
categories:
photos:
---

- Deterministic and Nondeterministic Functions
  - Deterministic functions
  - Nondeterministic functions
  - RAND() function
- WITH ENCRYPTION
- WITH SCHEMABINDING
<!-- more -->

<br />
<br />

---


# Deterministic and Nondeterministic Functions

### Deterministic functions
在定義的輸入值一樣，且 database 的狀態相同不變的條件下，不管呼叫幾次，總是回傳**相同值**，
e.g. `SUM()`、`AVG()`、`SQUARE()`、`POWER()`、`COUNT()`...etc.
**所有 aggregate functions 都是 deterministic functions**

### Nondeterministic functions
在定義的輸入值一樣，且 database 的狀態相同不變的條件下，可能回傳**不同值**，
e.g. `GetDate()`、`CURRENT_TIMESTAMP`

### RAND() function
Nondeterministic functions 的一種，
但若定義的輸入值為 seed value，則函數變成 deterministic，因為相同的 seed value 會返回相同的 value
<br />
<br />


# WITH ENCRYPTION

#### 用途
**加密 functions**

```sql
ALTER FUNCTION Function_name(@Parm int)
RETURNS nvarchar(20)
WITH ENCRYPTION
AS
BEGIN
  RETURN (SELECT Column FROM Table_name WHERE Column = @Parm)
END
```
<br />
<br />


# WITH SCHEMABINDING
SCHEMABINDING 將 function 綁定到 reference 的 database object，
必須要修改或刪除 function 以移除對 database object 的依賴

#### 用途
**限制 function reference 的 table schema 修改**

#### 注意
**使用`WITH SCHEMABINDING`時，必須用 two-part name(schema.object) 指定 table 名稱**

#### EX.
```sql
ALTER FUNCTION Function_name(@Parm int)
RETURNS nvarchar(20)
WITH SCHEMABINDING
AS
BEGIN
  RETURN (SELECT Column FROM Table_name WHERE Column = @Parm)
END
```
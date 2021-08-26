---
title: 【MSSQL】Temporary tables
tags:
  - SQL
  - 筆記
date: 2021-08-26 15:57:42
draft_date: 2021-08-26 14:06:38
layout:
categories: SQL 筆記
photos:
---

temporary table 被建立在 TempDB，且當 connection 關閉後會自動被刪除
- Permanent table
- Local temporary table
- Global temporary table
<!-- more -->

<br />
<br />

---


# Permanent table
需手動刪除

#### EX.
```sql
CREATE TABLE Table_name(...)
```
<br />
<br />


# Local temporary table
當前 connection 關閉時則刪除，也可手動刪除，
**可以在不同 connection 建立相同名稱**，建立時自動在**名稱末端加入亂數**

若使用 SP 建立 temporary table，會在 SP 執行完後自動被刪除，也就是只存在 SP 執行的當下

#### EX.
```sql
-- 建立
CREATE TABLE #Table_name(...)

-- 檢查是否有建立
-- 因建立時名稱自動加入亂數，所以需使用`LIKE`
SELECT name FROM tempdb..sysobjects
WHERE name LIKE '#PersonDetails%'

SELECT name FROM tempdb.sys.objects o
WHERE name LIKE '#PersonDetails%'
```
<br />
<br />


# Global temporary table
最後一個 connection 關閉時才會刪除，也可手動刪除，可見於所有 SQL Server sessions，
**名稱必須是唯一的**，建立時**名稱不會加入亂數**

#### EX.
```sql
CREATE TABLE ##Table_name(...)
```
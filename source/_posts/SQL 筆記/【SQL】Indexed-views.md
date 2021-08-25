---
title: 【SQL】Indexed views
date: 2021-08-24 21:40:49
layout:
categories: SQL 筆記
tags:
- SQL
- 筆記
photos:
---


當 view 加入 index 則能夠儲存 data，
執行`SELECT`時不需要再去 base table 取得資料，
若 base table 有進行 transaction 且 commit 時，view 也會跟著重新計算且更新
<!-- more -->

第一次在 view 加入 index，只能用`UNIQUE CLUSTERED INDEX`，
因為 view 本身並沒有儲存任何 data，所以沒辦法用`NON-CLUSTERED INDEX`

#### 注意
> _If GROUP BY is specified, the view select list must contain a `COUNT_BIG(*)` expression, and the view definition cannot specify `HAVING`, `ROLLUP`, `CUBE`, or `GROUPING SETS`._

# 用途
**提升效能**

# 使用時機
**index view 適合使用在 base table data 不會時常改變的時候**

**維護 index view 的成本會高於 table index，
所以 index view 通常使用於 data warehousing**

index view 適合 OLAP system (OnLine Analytical Processing)，
若是使用於 OLTP system (On-Line Transaction Processing system) 可能會影響到效能

# 參考連結
- [Creating Indexed Views](https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms191432(v=sql.105)?redirectedfrom=MSDN)
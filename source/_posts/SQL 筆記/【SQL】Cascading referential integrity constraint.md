---
layout:
title: 【SQL】Cascading referential integrity constraint
date: 2021-08-23 20:50:35
categories: SQL 筆記
tags:
- SQL
- 筆記
photos:
---

> **Cascading referential integrity constraint**
**用來定義使用者 UPDATE 或是 DELETE「FK」時的動作**
<!-- more -->


有以下四種選項
- **No Action**：預設，報錯且 roll back
- **Cascade**：所有 table 有存在該 FK 的 rows，會一併 UPDATE 或 DELETE
- **Set NULL**：所有 table 有存在該 FK 的 rows，設定為 NULL
- **Set Default**：所有 table 有存在該 FK 的 rows，設定為 Default 值
  - 如果該 column 值不存在 Default Constraint 則會報錯
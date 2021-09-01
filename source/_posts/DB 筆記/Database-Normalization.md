---
title: Database Normalization
categories: DB 筆記
tags:
  - Database
  - 筆記
date: 2021-09-01 23:28:21
draft_date: 2021-09-01 22:50:02
layout:
photos:
---


Database Normalization 是一種減少資料重複性，及確保資料一致性的過程
共有六個正規化，First Normal Form (1NF) 到 Sixth Normal Form (6NF)，大部分的 database 都是到 Third Normal Form (3NF)
<!-- more -->
<br />
<br />


# First Normal Form (1NF)
1. 每個在 column 的 data 必須是 atomic 的，沒有用逗號分開的多個值
2. 每個 table 不能包含任何重複的 column groups
3. 用 PK 識別每行 record 的唯一性
<br />
<br />


# Second Normal Form (2NF)
要符合第二正規化要滿足以下條件：
1. table 滿足 1NF 所有條件
2. 將重複的 data 分開到另一個 table
3. 用 FK 建立這些 tables 的關係

重複性的資料可能造成以下的問題：
- 浪費儲存空間
- 資料不一致性
- DML queries (e.g. `INSERT`, `UPDATE`, `DELETE`) 變慢
<br />
<br />

# Third Normal From (3NF)
要符合第三正規化要滿足以下條件：
1. table 滿足 1NF 和 2NF 所有條件
2. 不包含沒有完全依賴 PK 的 columns (attributes)
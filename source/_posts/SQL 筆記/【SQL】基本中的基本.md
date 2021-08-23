---
title: 【SQL】基本中的基本
date: 2021-08-23 22:57:38
layout:
categories: SQL 筆記
tags:
- SQL
- 筆記
photos:
---

> 突然發現常常忘記一些基本中的基本，
來寫一下筆記幫助記憶
<!-- more -->

# DBMS Language
SQL 是 DBMS(Database Management System) Language 的一種

- **DDL (Data Definition)**
資料定義，
e.g. `CREATE`、`ALTER`、`DROP`⋯etc.

- **DML (Data Manipulation)**
資料操作，
e.g. `INSERT`、`UPDATE`、`DELETE`⋯etc.

- **DQL (Data Query)**
資料查詢，
e.g. `SELECT`

- **DCL (Data Control)**
資料權限控制，
e.g. `GRANT`、`REVOKE`
<br />
<br />

---

# SQL Statements
由「**commands**、**clauses**、**operators**、**functions**」組成

- **Commands**
針對 database 或是 table 的動作，
e.g. `CREATE`、`ALTER`、`DROP`、`SELECT`、`UPDATE`、`DELETE`⋯etc.

- **Clauses**
設定或操作 query，
e.g. `WHERE`、`AND`、`OR`、`LIKE`、`ORDER BY`、`GROUP BY`⋯etc.

- **Operators**
處理邏輯運算及比較條件

- **Functions**
SQL 內建函數
<br />
<br />

---

# SQL Constraint
DDL 時定義 column 約束

- `NOT NULL`
- `UNIQUE`
- `PRIMARY KEY`
- `FOREIGN KEY`
- `CHECK`
- `DEFAULT`
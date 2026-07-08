# Introduction to Databases 复习笔记

这套笔记按 Lecture 1-10 整理，并结合 lab、additional materials 和 mock test。Database 考试会考概念、ERD、normalization、SQL，所以每章都保留英文关键词，同时用中文解释怎么做题。

## 最重要的考试优先级

| Priority | Topic | 必须会做什么 |
|---|---|---|
| 1 | SQL queries | `CREATE TABLE`, `INSERT`, `SELECT`, `WHERE`, `LIKE`, `IN`, `BETWEEN`, `ORDER BY`, aggregate, `GROUP BY`, `HAVING`, subquery, join |
| 2 | Normalization | 从 UNF 拆到 1NF, 2NF, 3NF，写 functional dependencies |
| 3 | ERD | 从 business rules 找 entities, attributes, PK/FK, relationship, cardinality, optional/mandatory |
| 4 | Relational model | PK, FK, candidate key, null, entity integrity, referential integrity |
| 5 | Concepts | data vs information, database vs DBMS, file system problems, anomalies, metadata, data dictionary |

## Mock Test 覆盖提醒

- MCQ 会考：PK/FK、metadata、data dictionary、business rules、file system limitation、unary relationship、data anomaly、3NF。
- 大题会考：UNF -> 3NF，要求写 functional dependencies 和每一步表。
- 大题会考：根据 case study 画 ERD。
- 大题会考：SQL `CREATE TABLE` with constraints，以及 `WHERE`, `IN`, `BETWEEN`, `AND`, `NOT`。
- SQL 题常见陷阱：table name 有空格、quote 写错、`DELETE FROM` 少 `FROM`、`ORDER BY` 多字段顺序。

## 文件目录

- [01_Introduction_to_Database.md](01_Introduction_to_Database.md)
- [02_File_System_and_DBMS.md](02_File_System_and_DBMS.md)
- [03_Data_Model_and_Business_Rules.md](03_Data_Model_and_Business_Rules.md)
- [04_Relational_Database_Part_1.md](04_Relational_Database_Part_1.md)
- [05_Relationships_in_Relational_Model.md](05_Relationships_in_Relational_Model.md)
- [06_ER_Model_Components.md](06_ER_Model_Components.md)
- [07_ERD_Notation_and_Advanced_Relationships.md](07_ERD_Notation_and_Advanced_Relationships.md)
- [08_Normalization_UNF_to_3NF.md](08_Normalization_UNF_to_3NF.md)
- [09_SQL_Part_1_Basic_Commands.md](09_SQL_Part_1_Basic_Commands.md)
- [10_SQL_Part_2_Advanced_Queries.md](10_SQL_Part_2_Advanced_Queries.md)
- [SQL_Command_Cheatsheet.md](SQL_Command_Cheatsheet.md) - SQL 命令理解版，从读题到写查询

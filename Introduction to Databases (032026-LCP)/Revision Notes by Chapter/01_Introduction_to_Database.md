# Lecture 1 - Introduction to Database

## 本章要会

这一章会考基础概念。Mock 已经考过 `data`, `database`, `metadata`。不要只背中文，要会看英文选项。

## Data vs Information

| Term | 中文理解 | English |
|---|---|---|
| Data | 原始事实，还没整理 | raw facts |
| Information | 处理后有意义的数据 | processed data with meaning |

例子：

- `Ali, 80, S01` 是 data。
- `Ali scored 80 marks` 是 information。

Mock 句型：

> A raw fact, such as customer's address, is known as ___.

Answer: `data`

## Database

Database 是 shared, integrated structure，用来存：

- end-user data
- metadata

中文记法：database 不一定要有很多表。Mock 考过：

> All are true about a database except: it must contain multiple tables.

这个说法是错的，因为一个 database 可以只有一个 table。

## Metadata

Metadata = data about data。

它描述：

- table structures
- data types
- constraints
- relationships

Mock 正确选项：

> It describes the data types, table structures, and constraints.

## DBMS

DBMS = Database Management System。

定义：collection of programs that manages database structure and controls access to data。

常见功能：

- create and manage database
- control access
- support query
- reduce inconsistency
- backup and recovery

## Database vs DBMS

| Item | Meaning |
|---|---|
| Database | 存数据的结构/集合 |
| DBMS | 管理 database 的软件 |

例子：

- Database: `Lab1`, `StudentDB`
- DBMS: Microsoft SQL Server, MySQL, Oracle

## Types of Databases

| Type | 中文理解 |
|---|---|
| single-user | 一次一个用户 |
| desktop | PC 小型数据库 |
| multi-user | 多用户 |
| workgroup | 部门/小组 |
| enterprise | 企业级 |
| centralized | 集中式 |
| distributed | 分布式 |
| transactional / production | 日常交易数据 |
| data warehouse | 分析/历史数据 |

## 易错点

- Data 是 raw facts，不是 processed result。
- Information must have meaning。
- Metadata 不等于旧数据或备份数据。
- DBMS 不是 database 本身，是管理 database 的 software。

## 自测

1. `StudentID`, `Name`, `DOB`, `nvarchar(50)` 这些结构说明属于什么？
   - Answer: metadata
2. Customer address 是 data 还是 information？
   - Answer: data


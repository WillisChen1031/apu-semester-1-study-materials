# Lecture 4 - Relational Database Part 1

## 本章要会

这一章重点是 table/relation、row/tuple、column/attribute、keys、null、integrity rules。Mock 高频。

## Relational Table Terms

| Relational term | Common term | 中文 |
|---|---|---|
| Relation | Table | 表 |
| Tuple | Row / Record | 行/记录 |
| Attribute | Column / Field | 列/字段 |
| Domain | Allowed values | 取值范围 |

Mock 题：

> A table is a matrix consisting of a series of row and column ___.

Answer: intersections

## Primary Key (PK)

Primary key uniquely identifies each row。

特点：

- must be unique
- cannot be null
- should not change
- may be one attribute or composite key

Mock 题：

> A primary key ___.

Answer: must be unique

注意：PK 不一定是第一列，也不一定必须 numeric。

## Candidate Key

Candidate key = any column or combination of columns that can uniquely identify a row。

一个 table 可以有多个 candidate keys，其中一个被选为 primary key。

## Foreign Key (FK)

Foreign key = attribute whose values match primary key values in a related table。

Mock 题：

> A foreign key must ___.

Answer: match the field value of a primary key in a related table

## Secondary Key

Secondary key 用来 retrieval/search，不一定 unique。

例子：用 `Name` 搜学生可能找到多个，所以它不是 PK，但可以作为 search key。

## Composite Key

Composite key = key made of more than one attribute。

例子：

```text
StudentMark(StudentID, SubjectID, Mark)
PK: StudentID + SubjectID
```

## Null

Null means no data entry / unknown / not applicable。

规则：

- PK cannot be NULL。
- FK 可以 NULL，前提是 relationship optional。
- Aggregate functions 对 NULL 有特殊处理，`COUNT(column)` 不数 NULL，`COUNT(*)` 数 row。

## Entity Integrity

Entity integrity:

- PK must be unique
- PK cannot be null

## Referential Integrity

Referential integrity:

- FK value must match existing PK in parent table
- or FK can be NULL if allowed

Lab 2 题型：

`Book.PublisherID` references `Publisher.PublisherID`。

- 插入不存在的 `PublisherID` 到 Book：不可以，因为违反 referential integrity。
- 删除 Deitel 如果已有 Book reference：通常不可以，除非 cascade delete。
- 删除 MacHill 如果没有 Book reference：可以。

## Data Dictionary / System Catalog

Data dictionary stores metadata:

- table names
- column names
- data types
- constraints
- relationships

## 易错点

- FK 不需要 unique。
- FK 可以重复，因为 many rows may reference same parent。
- Candidate key 不是一定会被选为 PK。
- Composite PK 在 normalization 和 bridge table 很常见。


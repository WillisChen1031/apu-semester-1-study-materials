# Lecture 3 - Data Model and Business Rules

## 本章要会

这一章是 ERD 的前置。考试会从 business rules 里让你找 entity、attribute、relationship、constraint。

## Data Model

Data model = relatively simple graphical representation of real-world data structures。

中文理解：用图或结构把现实世界的数据关系表达出来，让 designer、programmer、user 都能看懂。

## Data Model Building Blocks

| Component | 中文 | 如何识别 |
|---|---|---|
| Entity | 实体 | noun, 要存资料的东西 |
| Attribute | 属性 | entity 的特征 |
| Relationship | 关系 | verb, entity 之间的关联 |
| Constraint | 约束 | rule/restriction |

例子：

> A student enrolls in many subjects.

- Entity: Student, Subject
- Relationship: enrolls
- Constraint/cardinality: one student many subjects

## Business Rules

Business rules 是 precise and unambiguous descriptions of policies/procedures/principles。

它帮助决定：

- entities
- relationships
- participation
- constraints
- cardinality

Mock 题中正确说法包括：

- It allows designer to develop relationship, participation rules and constraints.
- It allows designer to understand the nature, role and scope of data.
- It must be updated when organization changes.

错误说法：business rule could be ambiguous。Business rules 应该 precise and unambiguous。

## 从 Business Rules 找 ERD

做题步骤：

1. 圈 nouns：通常是 entities。
2. 圈 verbs：通常是 relationships。
3. 找每个 entity 的 identifying attribute，作为 PK。
4. 找 `many`, `one`, `each`, `may`, `must`, `exactly`。
5. 判断 optional/mandatory。

## Data Models

常见模型：

- hierarchical model
- network model
- relational model
- entity relationship model
- object-oriented model

本课程重点是 relational model 和 ER model。

## Mini Example

Rule:

> Each lecturer supervises many students. Each student is supervised by one lecturer.

Entities:

- Lecturer
- Student

Relationship:

- supervises

Cardinality:

- Lecturer 1:M Student

Relational implementation:

- FK 放在 many side：`Student(LecID FK)`

## 易错点

- Entity 是要存很多 instances 的类别，不是单个值。
- Attribute 不是 table，attribute 是 column。
- Relationship 是 association，不是一定要变成 table；只有 M:N 常常需要 bridge table。
- Business rule 不是随便一句说明，它要能支持设计 decision。


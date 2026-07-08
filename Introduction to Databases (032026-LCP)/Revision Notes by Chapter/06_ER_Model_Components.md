# Lecture 6 - ER Model Components

## 本章要会

这一章考 ERD components：entity、attribute types、identifier、connectivity/cardinality、weak entity。画 ERD 时这些都要用。

## Entity

Entity = thing/object/concept about which data is stored。

ERD 中 entity 通常用 rectangle。

例子：

- STUDENT
- COURSE
- SUBJECT
- TEACHER

Entity name 通常用 noun，并可写 capital letters。

## Strong Entity vs Weak Entity

| Type | 中文理解 |
|---|---|
| Strong entity | 有自己的 PK，可独立存在 |
| Weak entity | 依赖 owner entity，通常需要 owner PK 才能识别 |

例子：

- Strong: `Employee`
- Weak: `Dependent`，因为 dependent 依赖 employee。

## Attribute

Attribute = characteristic of an entity。

ERD Chen notation 用 oval；Crow's Foot 通常写在 entity box 里。

## Attribute Types

| Type | 中文 | Example |
|---|---|---|
| Simple attribute | 不可再拆 | Gender |
| Composite attribute | 可再拆 | Name -> FirstName, LastName |
| Single-valued attribute | 一个 entity instance 只有一个值 | DOB |
| Multivalued attribute | 可能多个值 | PhoneNumber |
| Derived attribute | 可由其他属性算出 | Age from DOB |

SQL implementation 提醒：

- Composite attribute 通常拆成多个 columns。
- Multivalued attribute 通常拆成新 table。
- Derived attribute 通常不直接存，除非有特别需要。

## Identifier / Primary Key

Identifier 在 ERD 中常常 underlined。

```text
STUDENT(StudentID, Name, DOB)
PK: StudentID
```

## Domain

Domain = set of possible values for attribute。

例子：

- Gender: Male/Female
- Grade: A/B/C/D/F
- Salary: positive decimal

## Connectivity and Cardinality

Connectivity:

- 1:1
- 1:M
- M:N

Cardinality:

- minimum number
- maximum number

例子：

> Each student enrolls in one or more subjects.

Student to Subject:

- minimum: 1
- maximum: many

## 画 ERD Checklist

1. 每个 entity 有 PK。
2. Attribute 放在正确 entity 下。
3. Relationship 名称用动词。
4. Cardinality 根据 business rules 标。
5. Optional/mandatory 根据 `may/must/exactly/at least` 标。
6. M:N 关系如果要实现成 tables，要加 bridge entity。

## 易错点

- Age 通常是 derived attribute，因为可由 DOB 算。
- Full name 可能是 composite attribute。
- Multivalued attribute 不应该塞进一个 column 里，例如 `Phone1, Phone2, Phone3` 不理想。
- PK 不允许 NULL。


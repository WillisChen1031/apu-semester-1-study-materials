# Lecture 9 - SQL Part 1: Basic Commands

## 本章要会

SQL 是必考。Lecture 9 覆盖 DDL/DML、`CREATE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`。Lab 1-5 都在练这些。

## SQL Categories

| Category | Meaning | Commands |
|---|---|---|
| DDL | Data Definition Language | `CREATE`, `ALTER`, `DROP` |
| DML | Data Manipulation Language | `INSERT`, `UPDATE`, `DELETE`, `SELECT` |

Mock:

> SQL is structured query language.

## CREATE DATABASE

```sql
CREATE DATABASE Lab1;
```

SQL Server 使用：

```sql
USE Lab1;
```

## CREATE TABLE

Lab 1 Student table:

```sql
CREATE TABLE Student (
    StudentID nvarchar(50) PRIMARY KEY,
    Name nvarchar(50),
    Gender nvarchar(50),
    DOB date,
    Address nvarchar(50)
);
```

With foreign key:

```sql
CREATE TABLE Book (
    BookID nvarchar(50) PRIMARY KEY,
    Name nvarchar(50),
    Author nvarchar(50),
    Price decimal(10,2),
    PublishedDate date,
    PublisherID nvarchar(50),
    FOREIGN KEY (PublisherID) REFERENCES Publisher(PublisherID)
);
```

Mock style:

```sql
CREATE TABLE Teacher (
    TeacherID char(4) PRIMARY KEY,
    Name varchar(50) NOT NULL,
    Gender varchar(10) NOT NULL,
    Salary decimal(8,2) NOT NULL
);
```

```sql
CREATE TABLE Subject (
    SubjectID char(5) PRIMARY KEY,
    TeacherID char(4) NOT NULL,
    Name varchar(50) NOT NULL,
    ClassDay varchar(10) NOT NULL,
    Level varchar(10) NOT NULL,
    FOREIGN KEY (TeacherID) REFERENCES Teacher(TeacherID)
);
```

## INSERT

Insert all columns:

```sql
INSERT INTO Student
VALUES ('S01', 'Ali', 'Male', '2000-02-20', 'Kuala Lumpur');
```

Insert selected columns:

```sql
INSERT INTO Student (StudentID, Name, Gender)
VALUES ('S05', 'John', 'Male');
```

Insert multiple rows:

```sql
INSERT INTO Publisher
VALUES
('P01', 'Pearson', 'Bukit Jalil'),
('P02', 'Deitel', 'Puchong');
```

## SELECT

All columns:

```sql
SELECT *
FROM Supplier;
```

Selected columns:

```sql
SELECT Name, Price_RM
FROM Product;
```

Distinct:

```sql
SELECT DISTINCT Address
FROM Supplier;
```

## WHERE

```sql
SELECT *
FROM Book
WHERE Author = 'K.Vince';
```

Comparison:

```sql
SELECT *
FROM Book
WHERE Price > 100;
```

## BETWEEN / NOT BETWEEN

```sql
SELECT *
FROM Book
WHERE Price BETWEEN 100 AND 200;
```

```sql
SELECT *
FROM Book
WHERE Price NOT BETWEEN 100 AND 200;
```

## AND / OR / NOT

```sql
SELECT *
FROM Book
WHERE Author = 'S.Hanson' AND Price = 100;
```

```sql
SELECT *
FROM Book
WHERE Author = 'K.Vince' OR Price BETWEEN 50 AND 100;
```

```sql
SELECT *
FROM Subject
WHERE ClassDay = 'Monday' AND Level <> 'Form 1';
```

`<>` means not equal。

## IN

```sql
SELECT *
FROM Publisher
WHERE Address IN ('Puchong', 'Subang');
```

Mock:

```sql
SELECT *
FROM Subject
WHERE Level IN ('Form 1', 'Form 4')
  AND ClassDay = 'Wednesday';
```

## LIKE

| Pattern | Meaning |
|---|---|
| `'r%'` | starts with r |
| `'%n'` | ends with n |
| `'%i%'` | contains i |
| `'_a%'` | second character is a |
| `'b_%'` | starts with b and at least 2 chars |

Examples:

```sql
SELECT *
FROM Publisher
WHERE Name LIKE 'r%';
```

```sql
SELECT *
FROM Book
WHERE Name LIKE '_a%';
```

## IS NULL / IS NOT NULL

不能用 `= NULL`。

```sql
SELECT *
FROM Supplies
WHERE SuppliedDate IS NULL;
```

```sql
SELECT *
FROM Supplies
WHERE SuppliedDate IS NOT NULL;
```

## ORDER BY

```sql
SELECT *
FROM Publisher
ORDER BY Name ASC;
```

```sql
SELECT *
FROM Book
ORDER BY Name DESC;
```

Multiple columns:

```sql
SELECT *
FROM Employee
WHERE Country = 'Malaysia'
ORDER BY Name DESC, Country;
```

Mock 注意：排序先按第一个 column，再按第二个 column。

## UPDATE

```sql
UPDATE Publisher
SET Address = 'Serdang'
WHERE Name = 'Pearson';
```

多个 column:

```sql
UPDATE Book
SET Price = 98,
    PublishedDate = '2019-04-29'
WHERE Name = 'English';
```

一定要写 `WHERE`，否则全表都会改。

## DELETE

```sql
DELETE FROM Book
WHERE Name = 'Biology' AND Author = 'K.Vince';
```

注意：`DELETE FROM table` 删除 rows；`DROP TABLE table` 删除整张表。

## TOP

SQL Server:

```sql
SELECT TOP 2 *
FROM Publisher;
```

## 易错点

- Table name 不建议有空格。`Create Member Detail table` 是错的。
- String/date values 用 quotes。
- `DELETE Item WHERE...` 少了 `FROM`。
- `INSERT INTO Staff ('S01',...)` 是错的，缺 `VALUES`。
- `ORDER BY name desc, country` 合法。


# SQL Command Notes - 从理解到会写

这份不是普通 cheatsheet，而是专门给考试写 SQL 用的理解版。目标是：看到英文题目，知道它在要你用哪个 SQL command，并且能一步步写出来。

适用范围：Lecture 9, Lecture 10, Lab 1-10, Mock SQL 大题。

## 0. 先建立 SQL 思维

SQL 不是按程序一步一步跑的语言，它更像你在问数据库：

> From which table? Show which columns? Under what condition? In what order? Need grouping/join/subquery?

所以写 `SELECT` 题时永远按这个顺序想：

```text
1. 要显示什么 columns?         -> SELECT
2. 数据来自哪张 table?          -> FROM
3. 有没有条件?                 -> WHERE
4. 有没有 join 多张表?          -> JOIN ... ON
5. 有没有 group/aggregate?      -> GROUP BY / COUNT / SUM / AVG
6. group 后有没有条件?          -> HAVING
7. 要不要排序?                 -> ORDER BY
```

SQL 语句常见顺序：

```sql
SELECT column_name
FROM table_name
JOIN another_table
ON table_name.key = another_table.key
WHERE row_condition
GROUP BY grouped_column
HAVING group_condition
ORDER BY column_name ASC;
```

注意：实际执行顺序和写法顺序不完全一样，但考试先按这个写法顺序最稳。

## 1. SQL 分类：DDL vs DML

| Category | Full name | 中文理解 | Commands |
|---|---|---|---|
| DDL | Data Definition Language | 改 database/table 结构 | `CREATE`, `ALTER`, `DROP` |
| DML | Data Manipulation Language | 改/查 table 里的数据 | `INSERT`, `SELECT`, `UPDATE`, `DELETE` |

考试判断：

- 题目说 create table, add column, drop table -> DDL。
- 题目说 insert row, update data, delete record, display/list/show -> DML。

## 2. CREATE DATABASE / USE

### 用途

创建 database，并告诉 SQL Server 接下来在哪个 database 里工作。

### 语法

```sql
CREATE DATABASE Lab1;
USE Lab1;
```

### 中文理解

`CREATE DATABASE` 像新建一个文件夹；`USE` 像进入这个文件夹。

### 易错点

- 创建 table 前要确认已经 `USE database_name;`
- SQL Server 里 database 和 table 是不同层级。

## 3. CREATE TABLE

### 用途

创建表结构，包括 columns、data types、primary key、foreign key、constraints。

### 基本语法骨架

```sql
CREATE TABLE TableName (
    Column1 datatype constraint,
    Column2 datatype constraint,
    Column3 datatype constraint
);
```

### 常见 data types

| Data type | 用途 | Example |
|---|---|---|
| `nvarchar(50)` | 文字，可存 Unicode | Name, Address |
| `varchar(50)` | 文字 | Name |
| `char(4)` | 固定长度文字 | TeacherID like T001 |
| `int` | 整数 | Quantity, Salary if no decimal |
| `decimal(10,2)` | 小数/金额 | Price, Salary |
| `date` | 日期 | DOB, PublishedDate |

`decimal(10,2)` 的意思：总共最多 10 位数字，小数点后 2 位。

### Primary Key 写法

Inline 写法：

```sql
CREATE TABLE Student (
    StudentID nvarchar(50) PRIMARY KEY,
    Name nvarchar(50),
    Gender nvarchar(50),
    DOB date,
    Address nvarchar(50)
);
```

Table-level 写法：

```sql
CREATE TABLE Student (
    StudentID nvarchar(50),
    Name nvarchar(50),
    Gender nvarchar(50),
    DOB date,
    Address nvarchar(50),
    PRIMARY KEY (StudentID)
);
```

两种都可以。考试推荐 inline，简单。

### Foreign Key 写法

先创建 parent table，再创建 child table。

```sql
CREATE TABLE Publisher (
    PublisherID nvarchar(50) PRIMARY KEY,
    Name nvarchar(50),
    Address nvarchar(50)
);

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

### 中文理解

`Publisher` 是 parent table。`Book` 是 child table。一本书属于一个 publisher，所以 `PublisherID` 放在 `Book` 表里当 foreign key。

### Mock 风格题

Create `Teacher` and `Subject` table:

```sql
CREATE TABLE Teacher (
    TeacherID char(4) PRIMARY KEY,
    Name varchar(50) NOT NULL,
    Gender varchar(10) NOT NULL,
    Salary decimal(8,2) NOT NULL
);

CREATE TABLE Subject (
    SubjectID char(5) PRIMARY KEY,
    TeacherID char(4) NOT NULL,
    Name varchar(50) NOT NULL,
    ClassDay varchar(10) NOT NULL,
    Level varchar(10) NOT NULL,
    FOREIGN KEY (TeacherID) REFERENCES Teacher(TeacherID)
);
```

### NOT NULL

`NOT NULL` means column cannot be empty。

```sql
Name varchar(50) NOT NULL
```

Mock 问：

> NOT NULL constraint ensures that a column cannot have a null value.

### Composite Primary Key

Bridge table 常用 composite primary key。

```sql
CREATE TABLE StudentMark (
    StudentID nvarchar(50),
    SubjectID nvarchar(50),
    Mark int,
    PRIMARY KEY (StudentID, SubjectID),
    FOREIGN KEY (StudentID) REFERENCES Student(StudentID),
    FOREIGN KEY (SubjectID) REFERENCES Subject(SubjectID)
);
```

### 常见错误

错误：

```sql
Create Member Detail table (MemberID nvarchar(20));
```

原因：语法顺序错，table name 有空格也麻烦。

正确：

```sql
CREATE TABLE MemberDetail (
    MemberID nvarchar(20)
);
```

## 4. INSERT INTO

### 用途

把 row 加进 table。

### 全部 columns 都插入

```sql
INSERT INTO Student
VALUES ('S01', 'Ali', 'Male', '2000-02-20', 'Kuala Lumpur');
```

必须和 table columns 顺序一样。

### 指定 columns 插入

```sql
INSERT INTO Student (StudentID, Name, Gender)
VALUES ('S05', 'John', 'Male');
```

没写的 columns 会是 `NULL`，除非该 column 是 `NOT NULL`。

### 多行插入

```sql
INSERT INTO Publisher
VALUES
('P01', 'Pearson', 'Bukit Jalil'),
('P02', 'Deitel', 'Puchong'),
('P03', 'Rainbow', 'Subang');
```

### NULL 怎么插

```sql
INSERT INTO Book
VALUES ('B05', 'Computing', 'J.Denzin', NULL, NULL, NULL);
```

`NULL` 不加 quotes。`'NULL'` 是文字，不是真的 NULL。

### 常见错误

错误：

```sql
INSERT INTO Staff ('S01', 'John', 'Male');
```

正确：

```sql
INSERT INTO Staff
VALUES ('S01', 'John', 'Male');
```

## 5. SELECT 基础

### 用途

显示/查询数据。题目里出现 `show`, `display`, `list`, `find`，多数用 `SELECT`。

### 显示全部 columns

```sql
SELECT *
FROM Book;
```

`*` means all columns。

### 显示指定 columns

```sql
SELECT Name, Author
FROM Book;
```

题目说：

> Display a list of books showing only name and author.

就不要写 `SELECT *`。

### DISTINCT

去重复。

```sql
SELECT DISTINCT Address
FROM Supplier;
```

题目说 only distinct values，就用 `DISTINCT`。

## 6. WHERE 条件

### 用途

过滤 rows。

```sql
SELECT *
FROM Book
WHERE Author = 'K.Vince';
```

### 比较运算符

| Operator | Meaning |
|---|---|
| `=` | equal |
| `<>` | not equal |
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal |
| `<=` | less than or equal |

Examples:

```sql
SELECT *
FROM Book
WHERE Price > 100;
```

```sql
SELECT *
FROM Book
WHERE Price <= 100;
```

### 文字和日期要 quotes

```sql
WHERE Author = 'K.Vince'
WHERE PublishedDate > '2016-03-01'
```

数字不用 quotes：

```sql
WHERE Price > 100
```

## 7. AND / OR / NOT

### AND

两个条件都要成立。

```sql
SELECT *
FROM Book
WHERE Author = 'S.Hanson' AND Price = 100;
```

中文：作者必须是 S.Hanson，而且价格必须是 100。

### OR

其中一个条件成立即可。

```sql
SELECT *
FROM Book
WHERE Author = 'K.Vince' OR Price BETWEEN 50 AND 100;
```

### NOT

取反。

```sql
SELECT *
FROM Subject
WHERE ClassDay = 'Monday' AND NOT Level = 'Form 1';
```

更常见：

```sql
SELECT *
FROM Subject
WHERE ClassDay = 'Monday' AND Level <> 'Form 1';
```

### 括号很重要

题目：

> Level is Form 1 or Form 4, and class day is Wednesday.

正确：

```sql
SELECT *
FROM Subject
WHERE (Level = 'Form 1' OR Level = 'Form 4')
  AND ClassDay = 'Wednesday';
```

更干净：

```sql
SELECT *
FROM Subject
WHERE Level IN ('Form 1', 'Form 4')
  AND ClassDay = 'Wednesday';
```

如果不加括号，可能变成：

```text
Level = Form 1 OR (Level = Form 4 AND Wednesday)
```

逻辑就错了。

## 8. BETWEEN

### 用途

检查范围，包含边界。

```sql
SELECT *
FROM Teacher
WHERE Salary BETWEEN 3000 AND 4000;
```

等价于：

```sql
WHERE Salary >= 3000 AND Salary <= 4000
```

### NOT BETWEEN

```sql
SELECT *
FROM Book
WHERE Price NOT BETWEEN 100 AND 200;
```

### 考试例题

> Show all details for male teacher whose salary is between 3000 to 4000.

```sql
SELECT *
FROM Teacher
WHERE Gender = 'Male'
  AND Salary BETWEEN 3000 AND 4000;
```

## 9. IN

### 用途

一个 column 可以等于多个指定值之一。

```sql
SELECT *
FROM Publisher
WHERE Address IN ('Puchong', 'Subang');
```

等价于：

```sql
WHERE Address = 'Puchong' OR Address = 'Subang'
```

### 什么时候用

题目出现：

- is A or B
- belongs to Degree or Master
- level is Form 1 or Form 4

就考虑 `IN`。

```sql
SELECT *
FROM Course
WHERE Name IN ('Degree', 'Master');
```

## 10. LIKE

### 用途

模糊匹配文字。

| Pattern | 中文理解 | Example |
|---|---|---|
| `'r%'` | r 开头 | Rainbow |
| `'%n'` | n 结尾 | Pearson |
| `'%i%'` | 包含 i | Biology |
| `'_a%'` | 第二个字母是 a | Maths |
| `'b_%'` | b 开头且至少 2 个字符 | Biology |

`%` = any number of characters。

`_` = exactly one character。

### Lab 5 例题

Publisher name starts with r:

```sql
SELECT *
FROM Publisher
WHERE Name LIKE 'r%';
```

Publisher name ends with n:

```sql
SELECT *
FROM Publisher
WHERE Name LIKE '%n';
```

Book name contains `a` in the second position:

```sql
SELECT *
FROM Book
WHERE Name LIKE '_a%';
```

Book name contains `i` in any position:

```sql
SELECT *
FROM Book
WHERE Name LIKE '%i%';
```

Book name begins with `e` and ends with `h`:

```sql
SELECT *
FROM Book
WHERE Name LIKE 'e%h';
```

## 11. IS NULL / IS NOT NULL

### 用途

检查空值。

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

### 为什么不能写 `= NULL`

`NULL` means unknown。Unknown 不能用 `=` 比较。

错误：

```sql
WHERE SuppliedDate = NULL
```

正确：

```sql
WHERE SuppliedDate IS NULL
```

## 12. ORDER BY

### 用途

排序结果。

```sql
SELECT *
FROM Book
ORDER BY Name ASC;
```

`ASC` = ascending, 默认就是 ascending。

```sql
SELECT *
FROM Book
ORDER BY Name DESC;
```

`DESC` = descending。

### 多字段排序

```sql
SELECT *
FROM Employee
ORDER BY Salary DESC, Name DESC;
```

中文理解：先按 Salary 从高到低排；如果 Salary 一样，再按 Name 从 Z 到 A 排。

Mock 里类似题：

```sql
ORDER BY Salary DESC, Name DESC;
```

如果选成 `Salary DESC, Name ASC`，同薪水的人名字顺序会不一样。

### WHERE + ORDER BY

```sql
SELECT *
FROM Book
WHERE Author = 'K.Vince'
ORDER BY Name DESC;
```

顺序是 `WHERE` 在前，`ORDER BY` 在后。

## 13. UPDATE

### 用途

修改已有 rows。

### 单 column

```sql
UPDATE Publisher
SET Address = 'Serdang'
WHERE Name = 'Pearson';
```

### 多 columns

```sql
UPDATE Book
SET Price = 98,
    PublishedDate = '2019-04-29'
WHERE Name = 'English';
```

### 用 subquery update

题目：

> Change the price of the book to 93.50, for the book published by publisher from Puchong.

```sql
UPDATE Book
SET Price = 93.50
WHERE PublisherID IN (
    SELECT PublisherID
    FROM Publisher
    WHERE Address = 'Puchong'
);
```

### 最大陷阱

没有 `WHERE` 会更新整张表。

```sql
UPDATE Book
SET Price = 100;
```

这会把所有书价格变成 100。

## 14. DELETE

### 用途

删除 rows。

```sql
DELETE FROM Book
WHERE Name = 'Biology' AND Author = 'K.Vince';
```

### DELETE vs DROP

| Command | 删除什么 |
|---|---|
| `DELETE FROM Book WHERE ...` | 删除符合条件的 rows |
| `DELETE FROM Book` | 删除 Book 里所有 rows，table 还在 |
| `DROP TABLE Book` | 删除整张 table，结构也没了 |

### 常见错误

错误：

```sql
DELETE Item WHERE Name = 'Keyboard';
```

正确：

```sql
DELETE FROM Item
WHERE Name = 'Keyboard';
```

## 15. TOP

SQL Server 用 `TOP` 限制显示前几行。

```sql
SELECT TOP 2 *
FROM Publisher;
```

如果题目要 highest/lowest top 2，通常配 `ORDER BY`：

```sql
SELECT TOP 2 *
FROM Book
ORDER BY Price DESC;
```

中文：先按价格从高到低排，再拿前 2 个。

## 16. Aggregate Functions

### 用途

对一组 rows 做统计。

| Function | 中文 | Example |
|---|---|---|
| `MIN()` | 最小值 | lowest price |
| `MAX()` | 最大值 | highest salary |
| `SUM()` | 总和 | total price |
| `AVG()` | 平均 | average salary |
| `COUNT()` | 数量 | number of books |

### 基本写法

```sql
SELECT MIN(Price) AS LowestPrice
FROM Book;
```

```sql
SELECT MAX(Price) AS HighestPrice
FROM Book;
```

```sql
SELECT SUM(Price) AS TotalPrice
FROM Book;
```

```sql
SELECT AVG(Price) AS AveragePrice
FROM Book;
```

```sql
SELECT COUNT(*) AS TotalBooks
FROM Book;
```

### With WHERE

```sql
SELECT COUNT(*) AS NumOfBook
FROM Book
WHERE Author = 'K.Vince';
```

```sql
SELECT SUM(Price) AS TotalPriceForKVince
FROM Book
WHERE Author = 'K.Vince';
```

### COUNT(*) vs COUNT(column)

```sql
COUNT(*)
```

counts rows。

```sql
COUNT(Price)
```

counts non-null prices。

如果 `Price` 有 NULL，`COUNT(Price)` 不会数那些 NULL。

## 17. Subquery / Nested Query

### 用途

当题目条件需要另一张表或另一次查询的结果。

中文理解：先查里面的小问题，再把结果给外面的大问题用。

### 例 1：Book published by Deitel

题目要求不能直接写 `PublisherID = 'P02'`，要通过 publisher name 找。

```sql
SELECT *
FROM Book
WHERE PublisherID = (
    SELECT PublisherID
    FROM Publisher
    WHERE Name = 'Deitel'
);
```

里面先找：

```sql
SELECT PublisherID FROM Publisher WHERE Name = 'Deitel'
```

得到 `P02`。外面再找 `Book.PublisherID = P02`。

### 例 2：Books more expensive than average

```sql
SELECT Name, Price
FROM Book
WHERE Price > (
    SELECT AVG(Price)
    FROM Book
);
```

### 例 3：Publisher address is Puchong

如果 subquery 可能返回多个 ID，用 `IN`。

```sql
SELECT *
FROM Book
WHERE PublisherID IN (
    SELECT PublisherID
    FROM Publisher
    WHERE Address = 'Puchong'
);
```

### `=` vs `IN`

| Use | Meaning |
|---|---|
| `=` | subquery returns one value |
| `IN` | subquery may return many values |

如果 subquery 返回多个值，用 `=` 会 error。

## 18. GROUP BY

### 用途

按某个 column 分组，然后每组做统计。

题目关键词：

- for each author
- for each course
- group by each PublisherID
- total number of students for each course

### Count books by author

```sql
SELECT Author, COUNT(*) AS TotalBooksByAuthor
FROM Book
GROUP BY Author;
```

中文：每个 author 一组，每组数有几本书。

### Sum price by publisher

```sql
SELECT PublisherID, SUM(Price) AS BookPriceByPublisher
FROM Book
GROUP BY PublisherID;
```

### Order grouped result

```sql
SELECT Author, COUNT(*) AS TotalBooksByAuthor
FROM Book
GROUP BY Author
ORDER BY COUNT(*) DESC;
```

### GROUP BY 的硬规则

如果 `SELECT` 里有普通 column 和 aggregate function，普通 column 必须出现在 `GROUP BY` 里。

正确：

```sql
SELECT Author, COUNT(*)
FROM Book
GROUP BY Author;
```

错误：

```sql
SELECT Author, Name, COUNT(*)
FROM Book
GROUP BY Author;
```

`Name` 既没有 aggregate，也不在 `GROUP BY`，通常会错。

## 19. HAVING

### 用途

过滤 group。

`WHERE` 过滤 row；`HAVING` 过滤 group。

### Course with more than 1 student

```sql
SELECT CourseID, COUNT(*) AS TotalStudents
FROM Student
GROUP BY CourseID
HAVING COUNT(*) > 1;
```

中文：先按 course 分组，数每组学生数量，再保留数量大于 1 的组。

### Course with exactly 1 subject

```sql
SELECT CourseID, COUNT(*) AS TotalSubjects
FROM Subject
GROUP BY CourseID
HAVING COUNT(*) = 1;
```

### WHERE + GROUP BY + HAVING

题目：

> Count books written after 2016 for each author, only show authors with more than 1 book.

```sql
SELECT Author, COUNT(*) AS TotalBooks
FROM Book
WHERE PublishedDate > '2016-01-01'
GROUP BY Author
HAVING COUNT(*) > 1;
```

## 20. JOIN 基础

### 为什么要 JOIN

数据分在多张表，要一起显示，就要 join。

例子：

- `Book` 只有 `PublisherID`
- `Publisher` 才有 publisher name/address

要显示 book + publisher details，就 join。

### INNER JOIN

只显示两边匹配的 rows。

```sql
SELECT *
FROM Publisher
INNER JOIN Book
ON Publisher.PublisherID = Book.PublisherID;
```

中文：只显示有 publisher 且有 matching book 的记录。

### 不用 JOIN keyword 的旧写法

```sql
SELECT *
FROM Publisher, Book
WHERE Publisher.PublisherID = Book.PublisherID;
```

Lab 9 要求过 without using keyword `JOIN`。

### LEFT JOIN

显示 left table 全部 rows，right table 没匹配就显示 NULL。

```sql
SELECT *
FROM Publisher
LEFT JOIN Book
ON Publisher.PublisherID = Book.PublisherID;
```

中文：所有 publisher 都显示，就算它没有 book。

### RIGHT JOIN

显示 right table 全部 rows。

```sql
SELECT *
FROM Publisher
RIGHT JOIN Book
ON Publisher.PublisherID = Book.PublisherID;
```

中文：所有 book 都显示，就算某本书没有 publisher。

### FULL OUTER JOIN

两边全部显示，没匹配的地方是 NULL。

```sql
SELECT *
FROM Publisher
FULL OUTER JOIN Book
ON Publisher.PublisherID = Book.PublisherID;
```

## 21. 用 JOIN 找“没有 child 的 parent”

题目：

> Show the course where no student enrolled in.

方法：Course LEFT JOIN Student，然后找 Student 那边是 NULL。

```sql
SELECT Course.*
FROM Course
LEFT JOIN Student
ON Course.CourseID = Student.CourseID
WHERE Student.StudentID IS NULL;
```

题目：

> Show the publisher who had not published any book.

```sql
SELECT Publisher.*
FROM Publisher
LEFT JOIN Book
ON Publisher.PublisherID = Book.PublisherID
WHERE Book.BookID IS NULL;
```

## 22. JOIN + WHERE

### Book published by Deitel

```sql
SELECT Book.*
FROM Publisher
INNER JOIN Book
ON Publisher.PublisherID = Book.PublisherID
WHERE Publisher.Name = 'Deitel';
```

### Pearson + S.Hanson

```sql
SELECT *
FROM Publisher
INNER JOIN Book
ON Publisher.PublisherID = Book.PublisherID
WHERE Publisher.Name = 'Pearson'
  AND Book.Author = 'S.Hanson';
```

### Publisher address Bukit Jalil

```sql
SELECT *
FROM Publisher
INNER JOIN Book
ON Publisher.PublisherID = Book.PublisherID
WHERE Publisher.Address = 'Bukit Jalil';
```

## 23. Three-Table JOIN

Lab 9/10 常考 Course, Student, Subject。

Tables:

```text
Course(CourseID, Name, EntryQualification)
Student(StudentID, Name, Gender, DOB, CourseID)
Subject(SubjectID, Name, CourseID)
```

Course 和 Student 通过 `CourseID` 连。

Course 和 Subject 也通过 `CourseID` 连。

### Join all

```sql
SELECT *
FROM Course
INNER JOIN Student
ON Course.CourseID = Student.CourseID
INNER JOIN Subject
ON Course.CourseID = Subject.CourseID;
```

### Degree students studying ISWE

```sql
SELECT Student.*
FROM Student
INNER JOIN Course
ON Student.CourseID = Course.CourseID
INNER JOIN Subject
ON Course.CourseID = Subject.CourseID
WHERE Course.Name = 'Degree'
  AND Subject.Name = 'ISWE';
```

### Female students enrolled in Degree, order by student name desc

```sql
SELECT Student.*
FROM Student
INNER JOIN Course
ON Student.CourseID = Course.CourseID
WHERE Student.Gender = 'Female'
  AND Course.Name = 'Degree'
ORDER BY Student.Name DESC;
```

## 24. UNION

### 用途

把两个 SELECT 的结果上下合并。

要求：

- 两个 SELECT column 数量一样。
- 对应 columns data type compatible。

```sql
SELECT PublisherID, Name
FROM Publisher
UNION
SELECT BookID, Name
FROM Book;
```

`UNION` 会去重。`UNION ALL` 不去重。

## 25. ALTER TABLE

### 用途

修改 table structure。

### Add column

```sql
ALTER TABLE Publisher
ADD Telephone int;
```

### Change data type in SQL Server

```sql
ALTER TABLE Book
ALTER COLUMN Name varchar(50);
```

### Rename column in SQL Server

```sql
EXEC sp_rename 'Publisher.Telephone', 'ContactNumber', 'COLUMN';
```

### Drop column

```sql
ALTER TABLE Publisher
DROP COLUMN ContactNumber;
```

### Add primary key later

```sql
ALTER TABLE Product
ADD PRIMARY KEY (ProductID);
```

### Add foreign key later

```sql
ALTER TABLE Book
ADD FOREIGN KEY (PublisherID) REFERENCES Publisher(PublisherID);
```

## 26. DROP TABLE

### 用途

删除整张表。

```sql
DROP TABLE Book;
```

危险点：table structure 和 data 都没了。

## 27. Date / Age 常见写法

SQL Server 当前日期：

```sql
GETDATE()
```

年龄：

```sql
SELECT StudentID,
       Name,
       DATEDIFF(YEAR, DOB, GETDATE()) AS Age
FROM Student;
```

学生年龄大于 18：

```sql
SELECT *
FROM Student
WHERE DATEDIFF(YEAR, DOB, GETDATE()) > 18;
```

年龄大于平均年龄：

```sql
SELECT *
FROM Student
WHERE DATEDIFF(YEAR, DOB, GETDATE()) >
      (SELECT AVG(DATEDIFF(YEAR, DOB, GETDATE())) FROM Student);
```

## 28. 读题翻译训练

### Display all books written by K.Vince

关键词：display all -> `SELECT *`; books -> `FROM Book`; written by -> `WHERE Author`

```sql
SELECT *
FROM Book
WHERE Author = 'K.Vince';
```

### Display books that cost between 100 and 200

```sql
SELECT *
FROM Book
WHERE Price BETWEEN 100 AND 200;
```

### Display all books except Science, order by Author asc and Price desc

```sql
SELECT *
FROM Book
WHERE Name <> 'Science'
ORDER BY Author ASC, Price DESC;
```

### Count total subjects for each course

关键词：for each course -> `GROUP BY CourseID`; count -> `COUNT(*)`

```sql
SELECT CourseID, COUNT(*) AS TotalSubjects
FROM Subject
GROUP BY CourseID;
```

### Show course which has more than 1 student

关键词：more than 1 after count -> `HAVING`

```sql
SELECT CourseID, COUNT(*) AS TotalStudents
FROM Student
GROUP BY CourseID
HAVING COUNT(*) > 1;
```

### List all subjects where entry qualification is 5 credits in O Level

Need Course + Subject because `EntryQualification` is in Course。

```sql
SELECT Subject.*
FROM Subject
INNER JOIN Course
ON Subject.CourseID = Course.CourseID
WHERE Course.EntryQualification = '5 credits in O Level'
ORDER BY Subject.Name ASC;
```

## 29. 考试最常见错误总表

| 错误 | 为什么错 | 正确 |
|---|---|---|
| `WHERE column = NULL` | NULL 不能用 `=` | `WHERE column IS NULL` |
| `DELETE Book WHERE ...` | 少 `FROM` | `DELETE FROM Book WHERE ...` |
| `INSERT INTO Staff ('S01')` | 少 `VALUES` | `INSERT INTO Staff VALUES ('S01')` |
| `CREATE Member Detail table` | 语法错/table name 空格麻烦 | `CREATE TABLE MemberDetail (...)` |
| `WHERE Level = 'Form 1' OR 'Form 4'` | 第二个条件不完整 | `WHERE Level IN ('Form 1','Form 4')` |
| `WHERE Price = BETWEEN 100 AND 200` | `BETWEEN` 前不写 `=` | `WHERE Price BETWEEN 100 AND 200` |
| `GROUP BY` 乱选 column | 普通 column 必须分组 | `SELECT Author, COUNT(*) ... GROUP BY Author` |
| 用 `WHERE COUNT(*) > 1` | group 后条件要 HAVING | `HAVING COUNT(*) > 1` |
| Join 忘记 `ON` | 不知道两表怎么连 | `ON A.ID = B.ID` |
| `UPDATE` 忘记 `WHERE` | 会改全表 | `UPDATE ... WHERE ...` |

## 30. 最短背诵版

```sql
-- Create
CREATE TABLE T (
    ID nvarchar(50) PRIMARY KEY,
    Name nvarchar(50) NOT NULL
);

-- Insert
INSERT INTO T VALUES ('ID01', 'Ali');

-- Select
SELECT * FROM T WHERE Name = 'Ali';

-- Like
SELECT * FROM T WHERE Name LIKE 'A%';

-- Null
SELECT * FROM T WHERE Name IS NULL;

-- Sort
SELECT * FROM T ORDER BY Name DESC;

-- Update
UPDATE T SET Name = 'Abu' WHERE ID = 'ID01';

-- Delete row
DELETE FROM T WHERE ID = 'ID01';

-- Aggregate
SELECT COUNT(*) AS Total FROM T;

-- Group
SELECT Name, COUNT(*) AS Total
FROM T
GROUP BY Name
HAVING COUNT(*) > 1;

-- Join
SELECT *
FROM A
INNER JOIN B
ON A.ID = B.ID;

-- Subquery
SELECT *
FROM Book
WHERE Price > (SELECT AVG(Price) FROM Book);
```


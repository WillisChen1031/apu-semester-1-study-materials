# Lecture 10 - SQL Part 2: Advanced Queries

## 本章要会

Lecture 10 和 Lab 6-10 覆盖 aggregate functions、`GROUP BY`, `HAVING`, subquery, joins, `ALTER`, `DROP`。这些很容易出写 SQL。

## ALTER TABLE

Add column:

```sql
ALTER TABLE Publisher
ADD Telephone int;
```

Alter data type in SQL Server:

```sql
ALTER TABLE Book
ALTER COLUMN Name varchar(50);
```

Drop column:

```sql
ALTER TABLE Publisher
DROP COLUMN ContactNumber;
```

Rename column in SQL Server:

```sql
EXEC sp_rename 'Publisher.Telephone', 'ContactNumber', 'COLUMN';
```

## DROP TABLE

```sql
DROP TABLE Book;
```

`DROP` deletes table structure and data。`DELETE` deletes rows。

## Aggregate Functions

| Function | Meaning |
|---|---|
| `MIN()` | minimum |
| `MAX()` | maximum |
| `SUM()` | total |
| `AVG()` | average |
| `COUNT()` | count |

Examples:

```sql
SELECT MIN(Price) AS LowestPrice
FROM Book;
```

```sql
SELECT COUNT(*) AS TotalBooks
FROM Book;
```

```sql
SELECT AVG(Price) AS AveragePrice
FROM Book;
```

## Aggregate with WHERE

```sql
SELECT SUM(Price) AS TotalPriceForKVince
FROM Book
WHERE Author = 'K.Vince';
```

```sql
SELECT COUNT(*) AS BooksCostMoreThanRM60
FROM Book
WHERE Price > 60;
```

## Subquery

Find books more expensive than average:

```sql
SELECT Name, Price
FROM Book
WHERE Price > (SELECT AVG(Price) FROM Book);
```

Find books published by Deitel:

```sql
SELECT *
FROM Book
WHERE PublisherID = (
    SELECT PublisherID
    FROM Publisher
    WHERE Name = 'Deitel'
);
```

Subquery with `IN`:

```sql
SELECT *
FROM Book
WHERE PublisherID IN (
    SELECT PublisherID
    FROM Publisher
    WHERE Address = 'Puchong'
);
```

## GROUP BY

Group rows and calculate aggregate per group。

```sql
SELECT Author, COUNT(*) AS TotalBooksByAuthor
FROM Book
GROUP BY Author;
```

```sql
SELECT PublisherID, SUM(Price) AS BookPriceByPublisher
FROM Book
GROUP BY PublisherID;
```

With order:

```sql
SELECT Author, COUNT(*) AS TotalBooksByAuthor
FROM Book
GROUP BY Author
ORDER BY COUNT(*) DESC;
```

## HAVING

`WHERE` filters rows before grouping。`HAVING` filters groups after grouping。

Course with more than 1 student:

```sql
SELECT CourseID, COUNT(*) AS TotalStudents
FROM Student
GROUP BY CourseID
HAVING COUNT(*) > 1;
```

Publisher who published more than 1 book:

```sql
SELECT PublisherID, COUNT(*) AS NumOfBook
FROM Book
GROUP BY PublisherID
HAVING COUNT(*) > 1;
```

## INNER JOIN

Returns matching rows from both tables。

```sql
SELECT *
FROM Publisher
INNER JOIN Book
ON Publisher.PublisherID = Book.PublisherID;
```

Without keyword `JOIN`:

```sql
SELECT *
FROM Publisher, Book
WHERE Publisher.PublisherID = Book.PublisherID;
```

## LEFT JOIN

Return all rows from left table, matching rows from right table。

```sql
SELECT *
FROM Publisher
LEFT JOIN Book
ON Publisher.PublisherID = Book.PublisherID
ORDER BY Publisher.Name;
```

Useful for finding parent with no child:

```sql
SELECT Publisher.*
FROM Publisher
LEFT JOIN Book
ON Publisher.PublisherID = Book.PublisherID
WHERE Book.BookID IS NULL;
```

## RIGHT JOIN

Return all rows from right table。

```sql
SELECT *
FROM Publisher
RIGHT JOIN Book
ON Publisher.PublisherID = Book.PublisherID
ORDER BY Book.Name;
```

## FULL OUTER JOIN

Return all rows from both sides。

```sql
SELECT *
FROM Publisher
FULL OUTER JOIN Book
ON Publisher.PublisherID = Book.PublisherID;
```

## UNION

Combine results with same number of columns and compatible data types。

```sql
SELECT PublisherID, Name
FROM Publisher
UNION
SELECT BookID, Name
FROM Book;
```

## Three-Table Join

Lab 9:

```sql
SELECT *
FROM Course
INNER JOIN Student
ON Course.CourseID = Student.CourseID
INNER JOIN Subject
ON Course.CourseID = Subject.CourseID;
```

Student enrolled in Degree course and studied ISWE:

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

## Age from DOB in SQL Server

```sql
SELECT StudentID,
       Name,
       DATEDIFF(YEAR, DOB, GETDATE()) AS Age
FROM Student;
```

Age more than average age:

```sql
SELECT *
FROM Student
WHERE DATEDIFF(YEAR, DOB, GETDATE()) >
      (SELECT AVG(DATEDIFF(YEAR, DOB, GETDATE())) FROM Student);
```

## 易错点

- Aggregate column alias 用 `AS`：`COUNT(*) AS TotalBooks`。
- `GROUP BY` 里要放非 aggregate selected columns。
- 用 aggregate 条件过滤 group 时写 `HAVING`，不是 `WHERE`。
- Join 时 column 名相同要加 table prefix，例如 `Student.Name`, `Course.Name`。
- `LEFT JOIN ... WHERE right_table.PK IS NULL` 可以找没有 child 的 parent。


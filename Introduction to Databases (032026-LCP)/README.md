## Introduction to Databases (032026-LCP)

[返回总 README](../README.md)

Database 有 mock test 截图，重点非常集中：概念、ERD、normalization、SQL。

### 补充资料

- [3 types of relationship between entities-PDF version.pdf](Additional%20Materials/3%20types%20of%20relationship%20between%20entities-PDF%20version.pdf)
- [Database Normalization-step by step guide-PDF version.pdf](Additional%20Materials/Database%20Normalization-step%20by%20step%20guide-PDF%20version.pdf)
- [Database Normalization-step by step guide - Copy.docx](Additional%20Materials/Database%20Normalization-step%20by%20step%20guide%20-%20Copy.docx)
- [Normalization Example.pdf](Additional%20Materials/Normalization%20Example.pdf)
- [Normalization Example.docx](Additional%20Materials/Normalization%20Example.docx)

### 高频考点：Mock Test 已覆盖/高度相关

- database / DBMS / data / information 的定义与区别。
- file system problems：
  - data redundancy
  - data inconsistency
  - update anomaly
  - insertion anomaly
  - deletion anomaly
- data model / business rules / ERD。
- entity、attribute、relationship、constraint。
- relationship types：
  - 1:1
  - 1:M
  - M:N
- cardinality and optional/mandatory participation。
- primary key、foreign key、candidate key、secondary key、composite key。
- referential integrity。
- relational schema conversion：
  - entity -> table
  - attribute -> column
  - relationship -> FK 或 bridge/composite table
- normalization：
  - UNF, 1NF, 2NF, 3NF
  - repeating group
  - partial dependency
  - transitive dependency
- SQL：
  - DDL vs DML
  - `CREATE TABLE`
  - `INSERT`
  - `SELECT`
  - `WHERE`
  - `UPDATE`
  - `DELETE`
  - `ORDER BY`
  - `GROUP BY`
  - aggregate functions
  - joins
  - constraints
- 能根据表格写 SQL query，或根据 SQL 判断输出。
- 能根据 case study 画/读 ERD，并转换成 relational tables。

### Lecture-by-Lecture 考点

#### Lecture 1: Introduction to Database

- data vs information：
  - data 是 raw facts。
  - information 是 processed data with meaning。
- database：
  - shared, integrated structure storing end-user data and metadata。
- DBMS：
  - manages database structure and controls access。
- database value：
  - shared access
  - integrated view
  - reduced inconsistency
  - quick ad hoc queries
- types of databases：
  - single-user
  - desktop
  - multi-user
  - workgroup
  - enterprise
  - centralized
  - distributed
  - transactional/production
  - data warehouse

#### Lecture 2: File System and DBMS Functions

- file system limitations：
  - difficult administration
  - hard to change file structure
  - weak security
  - redundant and inconsistent data
- anomalies：
  - update anomaly
  - insertion anomaly
  - deletion anomaly
- database system environment components：
  - hardware
  - software
  - people
  - procedures
  - data
- DBMS functions：
  - data dictionary management
  - data storage management
  - data transformation and presentation
  - security management
  - multiuser access control
  - backup and recovery
  - data integrity management
  - database access languages/API
  - communication interfaces

#### Lecture 3: Data Model and Business Rules

- data model：graphical/simple representation of real-world data structures。
- business rules：
  - precise and unambiguous descriptions of policies/procedures。
  - nouns often become entities。
  - verbs often become relationships。
- data model building blocks：
  - entity
  - attribute
  - relationship
  - constraint
- models：
  - hierarchical
  - network
  - relational
  - entity relationship
  - object oriented
- ERD：
  - entity set
  - entity instance
  - connectivity
  - relationship lines

#### Lecture 4: Relational Database Part 1

- relation/table, row/tuple, column/attribute。
- relational table characteristics。
- keys：
  - superkey
  - candidate key
  - primary key
  - foreign key
  - secondary key
  - composite key
- null：
  - not allowed in PK。
  - may cause issues in `COUNT`, `AVG`, `SUM` and joins。
- entity integrity：
  - PK must be unique and not null。
- referential integrity：
  - FK must match existing PK or be valid null when allowed。
- data dictionary / system catalog / metadata。

#### Lecture 5: Relational Model and Relationships

- relationship in relational model。
- 1:1、1:M、M:N。
- resolving M:N：
  - create bridge/composite entity/table。
  - bridge table usually contains FKs from both parent tables。
  - bridge table may have its own attributes。
- common schema reading:
  - underline PK
  - mark FK
  - identify parent/child table

#### Lecture 6: ER Model Components

- entity：
  - strong entity
  - weak entity
- attributes：
  - simple
  - composite
  - single-valued
  - multivalued
  - derived
- relationship：
  - participants
  - connectivity
  - cardinality
  - business rules determine cardinality。
- identifier / primary key in ERD。
- mandatory vs optional participation。

#### Lecture 7: ERD Notation and Advanced Relationships

- Chen notation and Crow's Foot notation。
- relationship degree：
  - unary / recursive
  - binary
  - ternary
  - quaternary
- composite entities。
- M:N relationship valid in conceptual ERM, but must be resolved in relational implementation。
- 能根据 case study 找：
  - entities
  - attributes
  - PKs
  - relationships
  - cardinalities
  - optional/mandatory participation

#### Lecture 8: Normalization

- normalization purpose：
  - reduce redundancy
  - reduce anomalies
  - improve table structure
- functional dependency：
  - attribute A determines attribute B。
- determinant：
  - attribute whose value determines another value。
- UNF：
  - may contain repeating groups / multiple values in one cell。
- 1NF：
  - no repeating groups。
  - each cell contains atomic value。
  - key attributes identified。
- 2NF：
  - in 1NF。
  - no partial dependency。
  - especially relevant when PK is composite。
- 3NF：
  - in 2NF。
  - no transitive dependency。
- exam skill：
  - identify repeating groups。
  - identify composite PK。
  - separate partial dependencies into new tables。
  - separate transitive dependencies into lookup tables。
  - draw dependency diagram。

#### Lecture 9: SQL Part 1

- SQL categories：
  - DDL: create/alter/drop database objects。
  - DML: insert/update/delete/select data。
- `CREATE TABLE` syntax and data types。
- constraints：
  - `NOT NULL`
  - `UNIQUE`
  - `DEFAULT`
  - `CHECK`
  - `PRIMARY KEY`
  - `FOREIGN KEY`
- `INSERT INTO ... VALUES (...)`
- `COMMIT` and `ROLLBACK`。
- `SELECT columnlist FROM tablename;`
- `SELECT *`
- `WHERE` condition。
- `UPDATE ... SET ... WHERE ...`
- `DELETE FROM ... WHERE ...`
- special operators：
  - `BETWEEN`
  - `IS NULL`
  - `LIKE`
  - `IN`
  - `EXISTS`
- logical operators：`AND`, `OR`, `NOT`。
- arithmetic operator precedence。

#### Lecture 10: SQL Part 2

- `ALTER TABLE`：
  - `ADD`
  - `MODIFY`
  - `DROP`
- adding PK/FK after table copy。
- `DROP TABLE`。
- aggregate functions：
  - `COUNT`
  - `SUM`
  - `AVG`
  - `MIN`
  - `MAX`
- `DISTINCT` for unique values。
- `ORDER BY` ascending/descending。
- `GROUP BY` for grouped aggregate output。
- joins：
  - inner join
  - left outer join
  - right outer join
  - full outer join
  - recursive/self join
- aliases in joins。
- view：
  - virtual table based on `SELECT` query。
  - `CREATE VIEW`。

### SQL 必背模板

```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column1 ASC;
```

```sql
SELECT column, COUNT(*) AS total
FROM table_name
GROUP BY column;
```

```sql
SELECT a.col1, b.col2
FROM table_a a
JOIN table_b b
  ON a.id = b.a_id;
```

```sql
INSERT INTO table_name (col1, col2)
VALUES ('value1', 123);
```

```sql
UPDATE table_name
SET col1 = 'new value'
WHERE id = 1;
```

```sql
DELETE FROM table_name
WHERE id = 1;
```

## 推荐教程与覆盖判断

### 结论

Database 的外部教程可以很好覆盖 SQL、ERD、normalization，但你必须按 mock test 的题型练：看表写 SQL、看 case 画 ERD、把 UNF/1NF/2NF/3NF 拆表。

### B站视频

- [数据库系统 概论 速成 SQL 范式 ER图](https://search.bilibili.com/all?keyword=%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B3%BB%E7%BB%9F%20%E6%A6%82%E8%AE%BA%20%E9%80%9F%E6%88%90%20SQL%20%E8%8C%83%E5%BC%8F%20ER%E5%9B%BE)：适合期末复习概念、ERD、范式。
- [尚硅谷 MySQL 基础 SQL](https://search.bilibili.com/all?keyword=%E5%B0%9A%E7%A1%85%E8%B0%B7%20MySQL%20%E5%9F%BA%E7%A1%80%20SQL)：适合补 `SELECT`、`WHERE`、`JOIN`、`GROUP BY`、aggregate functions。
- [数据库 ER图 范式 期末复习](https://search.bilibili.com/all?keyword=%E6%95%B0%E6%8D%AE%E5%BA%93%20ER%E5%9B%BE%20%E8%8C%83%E5%BC%8F%20%E6%9C%9F%E6%9C%AB%E5%A4%8D%E4%B9%A0)：专门对准考试题型。

### YouTube 视频

- [Database Design ERD Normalization SQL full course](https://www.youtube.com/results?search_query=database+design+ERD+normalization+SQL+full+course)：系统补数据库设计。
- [SQL full course for beginners freeCodeCamp](https://www.youtube.com/results?search_query=SQL+full+course+for+beginners+freeCodeCamp)：适合 SQL 实战。
- [Database normalization 1NF 2NF 3NF tutorial](https://www.youtube.com/results?search_query=database+normalization+1NF+2NF+3NF+tutorial)：专攻范式。

### 文字教程/博客

- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)：最适合快速查 `SELECT`、`WHERE`、`JOIN`、`GROUP BY`、constraints、views。
- [GeeksforGeeks DBMS Tutorial](https://www.geeksforgeeks.org/dbms/)：覆盖 DBMS 概念、keys、ER model、normalization。
- [Database Normalization - Wikipedia](https://en.wikipedia.org/wiki/Database_normalization)：查 1NF/2NF/3NF 定义。

### 最短学习路线

1. 先练 SQL：`SELECT`、`WHERE`、`ORDER BY`、`GROUP BY`、aggregate、`JOIN`。
2. 再练 ERD：entity、attribute、relationship、cardinality、mandatory/optional participation。
3. 然后练 normalization：UNF -> 1NF -> 2NF -> 3NF。
4. 最后背概念：DBMS、file system problems、data redundancy、anomalies、keys、integrity。
5. mock test 中的 SQL/ERD/normalization 题要反复重做。

# Introduction to Databases — Mock Exam 1 & 2 全解析

> 适用课程：Introduction to Databases (032026-LCP)  
> 整理原则：题目与标准答案来自两份 Moodle Mock Review；解析使用中文，关键术语和 SQL 保留英文。大题答案经过语法和约束补全，适合作为考试书写模板。

## 先看这张速查表

| 主题 | 必背判断 |
|---|---|
| Primary key | 唯一且不可为 `NULL`；多个字段组成时叫 composite key |
| Candidate key | 所有能够唯一识别记录的最小属性集；其中一个被选为 primary key |
| Foreign key | 引用相关表的 primary/candidate key；可重复，是否可空取决于 participation |
| Entity integrity | Primary key 每个值唯一且非空 |
| Referential integrity | 每个非空 FK 必须匹配被引用表中已有的 key |
| 1NF | 原子值、无 repeating group |
| 2NF | 1NF，并消除对复合键的 partial dependency |
| 3NF | 2NF，并消除 transitive dependency |
| M:N | 一定要增加 associative/bridge table |
| Derived attribute | 通常不存，节省空间并避免维护不一致；需要时计算 |

---

# Mock Exam 1

## Q1 Primary key

**题目：** A primary key ____.

- a. may consist of null
- b. is always the first field in the table
- c. must be numeric
- d. must be unique

**答案：must be unique。**

Primary key 用来唯一识别每一行，因此不能重复，也不能为 `NULL`。它不一定是表中第一个字段，也不一定是数字。

## Q2 Metadata

**题目：** Which statement about metadata is accurate?

- a. It stores outdated transactional data about previous records in the database.
- b. It includes encrypted backup copies of confidential information in the database.
- c. It is used only during query processing between different databases.
- d. It describes the data types, table structures, and constraints.

**答案：It describes the data types, table structures, and constraints。**

Metadata 是“描述数据的数据”，例如表名、列名、数据类型、长度、PK/FK、`NOT NULL` 等约束；实际客户、订单等内容才是 user data。

## Q3 Normalization：Student–Subject–Teacher（20 分）

**题目：** Given the following un-normalized student result data, normalize it into Third Normal Form (3NF). Clearly show all functional dependencies and every step in the normalization process.

原始资料包含以下 attributes：

```text
StudentID, StudentFirstName, StudentLastName, StudentEnrollYear,
SubjectID, SubjectName, Mark,
TeacherID, TeacherFirstName, TeacherLastName
```

截图中的记录包括：

| StudentID | SubjectID | SubjectName | Mark | Student | EnrollYear | TeacherID | Teacher |
|---|---|---:|---:|---|---:|---|---|
| Stu_001 | Sub_001 | English | 83 | Joel Murphy | 2022 | teach_001 | Neha Khaushik |
| Stu_002 | Sub_001 | English | 79 | Kadhijah Qureshi | 2022 | teach_001 | Neha Khaushik |
| Stu_003 | Sub_001 | English | 88 | Mary George | 2022 | teach_001 | Neha Khaushik |
| Stu_004 | Sub_002 | Mathematic | 75 | Yu Hong | 2021 | teach_002 | Kavitha Shanmugam |
| Stu_005 | Sub_002 | Mathematic | 98 | Salleh Samsuddin | 2021 | teach_002 | Kavitha Shanmugam |
| Stu_006 | Sub_002 | Mathematic | 98 | Anishah Raizal | 2021 | teach_002 | Kavitha Shanmugam |
| Stu_007 | Sub_003 | Bahasa Melayu | 34 | Joel Murphy | 2022 | teach_002 | Kavitha Shanmugam |

Additional information and assumptions:

- A student can take multiple subjects.
- Each subject is taught by one teacher.
- A teacher can teach multiple subjects.

### 业务规则

- Student 可修读多个 Subject。
- 每个 Subject 由一个 Teacher 教授。
- 一个 Teacher 可教授多个 Subject。

### UNF → 1NF

先把重复组展开，保证每格只有一个原子值。1NF relation 可写成：

```text
ENROLMENT_UNF(
  StudentID, SubjectID, SubjectName, Mark,
  StuFirstName, StuLastName, StuEnrollYear,
  TeacherID, TeacherFirstName, TeacherLastName
)
```

最合理的行标识是 `(StudentID, SubjectID)`：同一学生对同一科目只有一条成绩。Mock suggested answer 把 `TeacherID` 也列入 composite key，但按“每科仅一名教师”的业务规则，`SubjectID → TeacherID`，所以 `TeacherID` 不需要成为主键的一部分。

### Functional dependencies

```text
StudentID → StuFirstName, StuLastName, StuEnrollYear
SubjectID → SubjectName, TeacherID
TeacherID → TeacherFirstName, TeacherLastName
(StudentID, SubjectID) → Mark
```

### 1NF → 2NF

原表主键为 `(StudentID, SubjectID)`。学生资料只依赖 `StudentID`，科目资料只依赖 `SubjectID`，都是 partial dependencies，必须拆开：

```text
STUDENT(StudentID PK, StuFirstName, StuLastName, StuEnrollYear)
SUBJECT(SubjectID PK, SubjectName, TeacherID, TeacherFirstName, TeacherLastName)
ENROLMENT(StudentID PK/FK, SubjectID PK/FK, Mark)
```

### 2NF → 3NF

在 `SUBJECT` 中有：

```text
SubjectID → TeacherID → TeacherFirstName, TeacherLastName
```

这是 transitive dependency，因此再拆出 `TEACHER`：

```text
STUDENT(StudentID PK, StuFirstName, StuLastName, StuEnrollYear)
TEACHER(TeacherID PK, TeacherFirstName, TeacherLastName)
SUBJECT(SubjectID PK, SubjectName, TeacherID FK)
ENROLMENT(StudentID PK/FK, SubjectID PK/FK, Mark)
```

此时每个非键属性只依赖“键、整个键、且只依赖键”，达到 3NF。

## Q4 Data vs information

**题目：** A raw fact, such as a customer's address, is known as ____.

- a. data
- b. information
- c. record
- d. relationship

**答案：data。**

客户地址这种未经加工的事实是 data；经过组织、分析并具有语境的结果才是 information。

## Q5 `NOT NULL`

**题目：** Which of the following defines the `NOT NULL` constraint?

- a. Ensures that all values in a column are different.
- b. Uniquely identifies a row/record in another table.
- c. Ensures that a column cannot have a null value.
- d. Allows the column to have an empty value.

**答案：Ensures that a column cannot have a null value。**

`NULL` 表示未知或缺失，不等于空字符串或数字 0。`NOT NULL` 只禁止空值，并不自动保证唯一。

## Q6 可成功执行的 SQL

**题目：** Which query will execute successfully?

- a. `INSERT INTO Staff ('S01', 'John', 'Male');`
- b. `SELECT * FROM Employee WHERE Country = 'Malaysia' ORDER BY Name DESC, Country;`
- c. `DELETE Item WHERE Name = 'Keyboard' ORDER BY Name;`
- d. `CREATE Member Detail TABLE (MemberID NVARCHAR(20), DOB DATE, Gender NVARCHAR(10));`

**答案：**

```sql
SELECT *
FROM Employee
WHERE Country = 'Malaysia'
ORDER BY Name DESC, Country;
```

其余选项分别缺少列清单/`VALUES`、`DELETE FROM` 语法错误、表名含空格却未转义。`ORDER BY` 可按多个列排序。

## Q7 Database 的错误描述

**题目：** All of these are true about a database **except**:

- a. It is a shared, integrated structure.
- b. It stores metadata.
- c. It must contain multiple tables.
- d. It stores user data.

**答案：it must contain multiple tables。**

数据库通常含多表，但定义上并非必须；它可以只有一张表。数据库是 shared、integrated structure，并保存 user data 与 metadata。

## Q8 Business rule

**题目：** Which of the following is TRUE about business rules?

1. It allows the designer to develop appropriate relationships, participation rules and constraints, and to create an accurate data model.
2. It allows the designer to understand the nature, role and scope of the data.
3. It could be an elaborate and ambiguous description of a policy, procedure or principle within a specific organization.
4. It must be updated to reflect any change in the organization's operational environment.

- a. iii only
- b. iv only
- c. i, ii, iii, iv
- d. i, ii, iv

**答案：i, ii, iv。**

- i 正确：业务规则帮助确定 relationship、participation 和 constraint。
- ii 正确：它帮助理解数据的 nature、role、scope。
- iii 错误：好的业务规则必须清楚、明确、可验证，不能 ambiguous。
- iv 正确：运营环境变化时规则也必须更新。

## Q9 ERD：HitRock Records（20 分）

**题目：** HitRock Records wants to store information about musicians who perform on its albums. Design an ERD based on these business rules. In the real exam, draw the ERD in the provided exam booklet.

- Each musician has an SSN, name, address and phone number.
- Each instrument has a name (for example guitar, synthesizer or flute) and a musical key (for example C, B-flat or E-flat).
- Each album has a title, copyright date, format (for example CD or MC) and album identifier.
- Each song has a title and an author.
- Each musician may play several instruments, and an instrument may be played by several musicians.
- Each album contains a number of songs, but no song may appear on more than one album.
- Each song is performed by one or more musicians, and a musician may perform a number of songs.
- Each album has exactly one musician as producer; a musician may produce several albums.

### Entities

```text
MUSICIAN(SSN PK, Name, Address, Phone)
INSTRUMENT(InstrumentID PK, Name, MusicalKey)
ALBUM(AlbumID PK, Title, CopyrightDate, Format, ProducerSSN FK)
SONG(SongID PK, Title, Author, AlbumID FK)
MUSICIAN_INSTRUMENT(SSN PK/FK, InstrumentID PK/FK)
PERFORMANCE(SSN PK/FK, SongID PK/FK)
```

### Relationships 与 cardinality

- `MUSICIAN M:N INSTRUMENT`：双方都可多个，因此用 `MUSICIAN_INSTRUMENT` bridge table。
- `ALBUM 1:M SONG`：每张 album 有多首 song；每首 song 最多属于一张 album。若题意要求每首歌必属于 album，则 `SONG.AlbumID NOT NULL`。
- `MUSICIAN M:N SONG`：song 至少由一位 musician 演奏；musician 可演奏多首 song，用 `PERFORMANCE`。
- `MUSICIAN 1:M ALBUM`（produces）：每张 album **exactly one** producer，所以 `ProducerSSN NOT NULL`；musician 可制作 0..N 张 album。

作图得分点：标出 PK/FK、M:N 的 associative entities、album producer 的 mandatory one，以及 song performer 的 minimum one。

## Q10 Project–Employee ERD

**题目：** Based on the Project–Employee ERD shown in the Mock, which statement depicts the relationship?

```text
PROJECT(ProjectID, Name, Budget, EmpID FK)
EMPLOYEE(EmpID, Name, Address, ContactNo)
Relationship: Employee handles Project
```

- a. A project is handled by many employees.
- b. Project is optional to employee.
- c. Project is mandatory to employee.
- d. Employee handles at least one project.

**答案：Project is optional to employee。**

意思是 Employee 可以暂时没有 Project，即 Employee 对 Project 的最小 cardinality 为 0。不要只看 “many” 端；optional/mandatory 看的是最小值 0 或 1。

## Q11 `ORDER BY`

**题目：** Which `ORDER BY` statement will produce the displayed result, where salary is ordered `5000, 4000, 3000, 2500`, and names with equal salary are in descending name order?

- a. `ORDER BY Name ASC, Salary DESC;`
- b. `ORDER BY Salary DESC, Name DESC;`
- c. `ORDER BY Salary DESC, Name ASC;`
- d. `ORDER BY Salary ASC, Name ASC;`

**答案：**

```sql
ORDER BY Salary DESC, Name DESC;
```

SQL 先按第一个排序键 Salary 从高到低；只有 salary 相同才用 Name 从 Z 到 A 决定顺序。

## Q12 SQL 全称

**题目：** SQL is:

- a. Structured Query Language
- b. Sequencing Query Listing
- c. Sequencing Query Language
- d. Structured Query Listing

**答案：Structured Query Language。**

## Q13 Teacher / Subject SQL（20 分）

**题目：** Consider the following tables from a tuition centre that provides classes for Form 1–Form 5 students.

**Teacher**

| TeacherID | Name | Gender | Salary |
|---|---|---|---:|
| T001 | Sandra | Female | 3500 |
| T002 | Xavier | Male | 4000 |
| T003 | Jack | Male | 4100 |
| T004 | Lisa | Female | 4250 |

**Subject**

| SubjectID | TeacherID | Name | ClassDay | Level |
|---|---|---|---|---|
| SC111 | T001 | Mathematics | Monday | Form 1 |
| SC411 | T003 | Physics | Monday | Form 4 |
| SC511 | T002 | Physics | Tuesday | Form 5 |
| SC412 | T003 | Chemistry | Wednesday | Form 4 |
| SC211 | T004 | Mathematics | Thursday | Form 2 |
| SC311 | T001 | Mathematics | Friday | Form 3 |

Write SQL to:

1. Create `Teacher` using suitable data types and relevant constraints.
2. Create `Subject` using suitable data types and relevant constraints.
3. Show all Subject details where Level is Form 1 or Form 4, and ClassDay is Wednesday.
4. Show all male teachers whose salary is between 3000 and 4000.
5. Show all Subject details where ClassDay is Monday but Level is not Form 1.

### (a) 建立 Teacher

```sql
CREATE TABLE Teacher (
    TeacherID CHAR(4) PRIMARY KEY,
    Name      VARCHAR(50) NOT NULL,
    Gender    VARCHAR(10) NOT NULL,
    Salary    DECIMAL(8,2) NOT NULL CHECK (Salary >= 0)
);
```

### (b) 建立 Subject

```sql
CREATE TABLE Subject (
    SubjectID CHAR(5) PRIMARY KEY,
    TeacherID CHAR(4) NOT NULL,
    Name      VARCHAR(50) NOT NULL,
    ClassDay  VARCHAR(10) NOT NULL,
    Level     VARCHAR(10) NOT NULL,
    CONSTRAINT FK_Subject_Teacher
      FOREIGN KEY (TeacherID) REFERENCES Teacher(TeacherID)
);
```

FK 两端的数据类型与长度应一致，而且必须先建立被引用的 `Teacher`。

### (c) Level 为 Form 1 或 Form 4，且星期三

```sql
SELECT *
FROM Subject
WHERE Level IN ('Form 1', 'Form 4')
  AND ClassDay = 'Wednesday';
```

注意括号逻辑：若用 `OR`，应写 `(Level='Form 1' OR Level='Form 4') AND ...`。

### (d) 男教师，工资 3000–4000

```sql
SELECT *
FROM Teacher
WHERE Gender = 'Male'
  AND Salary BETWEEN 3000 AND 4000;
```

`BETWEEN` 包含上下界。

### (e) 星期一但不是 Form 1

```sql
SELECT *
FROM Subject
WHERE ClassDay = 'Monday'
  AND Level <> 'Form 1';
```

## Q14 Functional dependency

**题目：** In a database table, the statement “A determines B” indicates that:

- a. Knowing A, you cannot look up B.
- b. You do not need to know A in order to look up B.
- c. Knowing A, you can look up B.
- d. Knowing B, you can look up A.

**答案：knowing A, you can look up B。**

`A → B` 表示每个 A 值只对应一个确定的 B 值；反向 `B → A` 不一定成立。

## Q15 Single entity 内的 relationship

**题目：** A ____ relationship exists when an association is maintained within a single entity.

- a. ternary
- b. quaternary
- c. binary
- d. unary

**答案：unary relationship。**

也叫 recursive relationship，例如 Employee supervises Employee。

## Q16 DBMS 保存数据定义的位置

**题目：** The DBMS stores definitions of data elements and their relationships in a:

- a. fixed-length field
- b. fixed-length record
- c. information diary
- d. data dictionary

**答案：data dictionary。**

Data dictionary/system catalog 保存 metadata，如 schema、列、约束和权限。

## Q17 2NF 且无 transitive dependency

**题目：** A table that is in 2NF and includes no transitive dependencies is said to be in ____.

- a. 3NF
- b. 0NF
- c. 1NF
- d. 2NF

**答案：3NF。**

## Q18 表之间的逻辑连接

**题目：** A table can be logically connected to another table by defining a ____.

- a. secondary key
- b. logic key
- c. primary key
- d. (common attribute) foreign key

**答案：(common attribute) foreign key。**

FK 在子表中引用父表的 key，从而建立逻辑关系。

## Q19 不属于 data anomaly

**题目：** Which of the following is **not** a data anomaly?

- a. Insert
- b. Update
- c. Create
- d. Delete

**答案：create。**

经典 anomalies 是 insertion、update、deletion anomaly。

## Q20 Table 是 rows 与 columns 的矩阵

**题目：** A table is a matrix consisting of a series of row and column ____.

- a. intersections
- b. systems
- c. models
- d. links

**答案：intersections。**

每个 row-column intersection 是一个 cell，1NF 要求其中是单一原子值。

## Q21 Foreign key 必须满足

**题目：** A foreign key must:

- a. not consist of null
- b. be unique
- c. be defined in all tables within the database
- d. match the field value of a primary key in a related table

**答案：match the field value of a primary key in a related table。**

更严谨地说：每个**非空** FK 必须匹配被引用的 candidate/primary key。FK 可以重复，也可能允许 `NULL`。

## Q22 File system limitation

**题目：** Which of the following is a limitation of the file system environment?

- a. Security features are likely to be inadequate.
- b. It allows multi-user access.
- c. It does not allow deletion of data.
- d. It supports SQL.

**答案：security features are likely to be inadequate。**

传统文件系统常有数据冗余、不一致、共享困难、安全性和并发控制不足等问题；支持 SQL 和良好的多用户访问反而是 DBMS 优势。

## Q23 At most one related entity

**题目：** If an entity in a relationship will have at most one related entity, this is known as ____.

- a. Many-to-many relationship
- b. One-to-one relationship
- c. One-to-many relationship
- d. One-to-all relationship

**答案：One-to-one relationship。**

“At most one” 表示最大 cardinality 为 1；是否 optional 仍要看最小值是 0 还是 1。

---

# Mock Exam 2

## Q1 Candidate keys

**题目：** Given `Product(ProductID, Name, Description, SerialNumber)`, which attributes could be candidate keys based on these rules?

- Some products may have the same name.
- No products may have the same serial number.
- Product description may be null.
- ProductID must be unique.

Options:

- a. SerialNumber & Name
- b. SerialNumber & Description
- c. ProductID & SerialNumber
- d. ProductID & Name

**答案：ProductID & SerialNumber。**

题目说明 `ProductID` 必须唯一，`SerialNumber` 也不能重复，因此两者各自都是 candidate key。这里的 `&` 表示“两个都是候选键”，不是把两列合成 composite key。Name 可重复，Description 可空，不能可靠唯一识别记录。

## Q2 多字段 Primary key

**题目：** A primary key that consists of more than one field is called a ____ key.

- a. secondary
- b. composite
- c. candidate
- d. foreign

**答案：composite key。**

## Q3 Single entity 内的 relationship

**题目：** A ____ relationship exists when an association is maintained within a single entity.

- a. unary
- b. quaternary
- c. ternary
- d. binary

**答案：unary relationship。**

Unary/recursive relationship 的两个角色都来自同一 entity type。

## Q4 Hotel SQL（20 分）

**题目：** Consider the following hotel management tables.

**ROOM**

| RoomID | Name | Description | Price |
|---|---|---|---:|
| R1001 | Superior Twin | 2 single beds | 500 |
| R2002 | Deluxe Twin | 2 single beds | 550 |
| R2005 | Superior King | 1 king bed | 600 |
| R3006 | Deluxe King | 1 king bed | 650 |
| R5005 | Deluxe Suite | 1 super king bed, 1 king bed | 800 |

**GUEST**

| GuestID | GuestName | ContactNumber |
|---|---|---|
| C101 | J. Alan | 011-6738495 |
| C102 | P. Amos | 018-3927648 |
| C103 | S. John | 019-3442486 |
| C104 | K. William | 017-9387652 |
| C105 | J. Martin | 011-5326780 |
| C106 | K. Oscar | 016-2230087 |

**RESERVATION**

| ReservationID | RoomID | GuestID | CheckInDate | CheckOutDate |
|---|---|---|---|---|
| RS1001 | R1001 | C102 | 2019-12-02 | 2019-12-05 |
| RS1193 | R2005 | C105 | 2019-12-05 | 2019-12-06 |
| RS1208 | R3006 | C103 | 2020-01-15 | 2020-01-16 |
| RS1245 | R5005 | C101 | 2021-05-09 | 2021-05-12 |
| RS2501 | R2002 | C102 | 2021-08-10 | 2021-08-12 |
| RS2601 | R2005 | C103 | 2022-01-15 | 2022-01-17 |
| RS3002 | R2005 | C102 | 2022-04-08 | 2022-04-10 |

Write SQL statements to:

1. List guest names and contact numbers for guests who made reservations more than two times. (5 marks)
2. Increase the price of `Deluxe Twin` by 10%. (5 marks)
3. List guest names and contact numbers for guests who reserved a room with `1 king bed`. (5 marks)
4. Create the `RESERVATION` table with suitable data types and constraints. (5 marks)

### (a) 预订超过 2 次的客人姓名与电话

```sql
SELECT g.GuestName, g.ContactNumber
FROM Guest AS g
JOIN Reservation AS r ON r.GuestID = g.GuestID
GROUP BY g.GuestID, g.GuestName, g.ContactNumber
HAVING COUNT(*) > 2;
```

`WHERE` 过滤明细行，`HAVING` 过滤分组后的 aggregate result。选择了姓名和电话，就应把它们列入 `GROUP BY`（连同稳定的 GuestID）。

### (b) Deluxe Twin 加价 10%

```sql
UPDATE Room
SET Price = Price * 1.10
WHERE Name = 'Deluxe Twin';
```

### (c) 预订 “1 king bed” 房型的客人

```sql
SELECT DISTINCT g.GuestName, g.ContactNumber
FROM Guest AS g
JOIN Reservation AS r ON r.GuestID = g.GuestID
JOIN Room AS rm ON rm.RoomID = r.RoomID
WHERE rm.Description = '1 king bed';
```

`DISTINCT` 防止同一客人多次订到该房型时重复出现。若题意是 description **包含**该文字，可改用 `LIKE '%1 king bed%'`。

### (d) 建立 Reservation

```sql
CREATE TABLE Reservation (
    ReservationID CHAR(6) PRIMARY KEY,
    RoomID       CHAR(5) NOT NULL,
    GuestID      CHAR(4) NOT NULL,
    CheckInDate  DATE NOT NULL,
    CheckOutDate DATE NOT NULL,
    CONSTRAINT FK_Reservation_Room
      FOREIGN KEY (RoomID) REFERENCES Room(RoomID),
    CONSTRAINT FK_Reservation_Guest
      FOREIGN KEY (GuestID) REFERENCES Guest(GuestID),
    CONSTRAINT CK_Reservation_Dates
      CHECK (CheckOutDate > CheckInDate)
);
```

## Q5 Date 不允许的操作

**题目：** Which of the following is **not** an allowable operation for a date field?

- a. Compare two dates.
- b. Convert a date from its internal representation to a different presentation format.
- c. Multiply two dates.
- d. Create a date by adding or subtracting a number of days from a given date.

**答案：Multiply two dates。**

日期可以比较、格式化，也可加减天数；两个日期相减通常得到间隔，但相乘没有业务意义。

## Q6 不保存 derived attribute 的优势

**题目：** Which of the following is an advantage of **not storing** a derived attribute?

- a. The data value is readily available.
- b. Save storage space.
- c. Require constant maintenance to ensure the value is up to date.
- d. Add coding complexity to the query.

**答案：Save storage space。**

Derived attribute 可由其他数据算出，例如 `Total = Quantity × UnitPrice`。不保存它可节省空间，也减少源数据改变后 derived value 过期的问题；代价是查询时需要计算。

## Q7 Author–Book–Publisher 需要多少张表

**题目：** Based on the following description, how many tables will be created?

- An author can write many books, and a book can be written by different authors.
- A publisher can publish many books, and a book can be published by only one publisher.

Options:

- a. 2 tables
- b. 3 tables
- c. 4 tables
- d. 5 tables

**答案：4 tables。**

```text
AUTHOR
BOOK
PUBLISHER
AUTHOR_BOOK  ← 解决 Author 与 Book 的 M:N
```

Publisher–Book 是 1:M，只需把 `PublisherID` 放入 `BOOK` 作 FK，无需额外 bridge table。

## Q8 Normal form 层级

**题目：** From a structural point of view, in database normalization, 2NF is better than ____ and 3NF is better than ____.

- a. 2NF, UNF
- b. 1NF, 2NF
- c. 2NF, 1NF
- d. UNF, NF

**答案：1NF, 2NF。**

2NF 比 1NF 结构更好，3NF 比 2NF 更好；每一级都包含前一级条件再消除一种依赖问题。

## Q9 Weak entity

**题目：** Given these tables, which entity is most likely a weak entity?

```text
Employee(EmpID PK, Name, Gender, SupervisorID FK)
Dependent(DepID PK, EmpID PK/FK, DepName, DepDOB)
Project(ProID PK, Name, SupervisorID FK)
Supervisor(SupervisorID PK, Name)
```

- a. Supervisor
- b. Dependent
- c. Project
- d. Employee

**答案：Dependent。**

`DEPENDENT` 的 PK 是 `(DepID, EmpID)`，其中 `EmpID` 同时是 owner `EMPLOYEE` 的 FK。Dependent 的身份依赖 Employee，符合 weak entity 特征。

## Q10 表之间的逻辑连接

**题目：** A table can be logically connected to another table by defining a ____.

- a. foreign key
- b. primary key
- c. hyperlink
- d. candidate key

**答案：foreign key。**

## Q11 Entity integrity

**题目：** The entity integrity rule requires that ____.

- a. All primary key entries are unique.
- b. Foreign key values do not reference primary key values.
- c. A part of the key may be null.
- d. Duplicate primary key values are allowed.

**答案：all primary key entries are unique。**

完整规则还包括 PK 不得为 `NULL`。复合 PK 的任何组成部分也不能为 `NULL`。

## Q12 ERD：Car Manufacturing（20 分）

**题目：** Analyse the following case study and produce an ERD showing all relevant entities, attributes, relationships, participation and cardinality constraints. Crow's Foot or Chen notation may be used.

A car manufacturing company produces many cars each year. Every car has a model, manufacture year, colour and other details. To build cars, the company purchases parts from different suppliers. Each supplier may supply different parts. The company records supplier name, address and contact details, as well as which part was purchased from which supplier and on which day. Each part has a name, description and price. After construction, every car must be sent for testing before market launch. The company records which car was tested on which day and the test feedback. Each car must be tested at least once and at most five times.

### 推荐 entities

```text
CAR(CarID PK, Model, ManufactureYear, Colour)
PART(PartID PK, Name, Description, Price)
SUPPLIER(SupplierID PK, Name, Address, Contact)
PURCHASE(SupplierID PK/FK, PartID PK/FK, PurchaseDate PK, Quantity)
CAR_PART(CarID PK/FK, PartID PK/FK, QuantityUsed)
TEST(TestID PK, CarID FK, TestDate, Feedback)
```

### Relationship 分析

- Supplier 与 Part 是 M:N：一个 supplier 可供应多种 part；同一种 part 可来自不同 supplier。`PURCHASE` 记录 supplier、part、日期及数量，因此它是 associative entity。
- Car 与 Part 通常也是 M:N：一辆车使用多个 parts，同一种 part 可用于多辆 car，用 `CAR_PART`。
- Car 与 Test 是 1:M：每次 test 只属于一辆 car；每辆 car 必须测试 **1..5 次**。在 ERD 上标 `CAR 1 — TEST 1..5`。上限 5 一般需 application logic、trigger 或 assertion 才能严格实现。

作图时不要把 PurchaseDate 塞进 Supplier 或 Part；它描述的是一次“供应/采购”关系。

## Q13 Referential integrity

**题目：** The referential integrity rule requires that:

- a. Every null foreign key value must reference an existing primary key value.
- b. A foreign key cannot be null.
- c. Every non-null foreign key value references an existing primary key value.
- d. An attribute has a corresponding value.

**答案：every non-null foreign key value references an existing primary key value。**

FK 若允许 optional relationship 可以为 `NULL`；一旦非空，就必须能在父表找到对应 key。

## Q14 只能有一个值的 attribute

**题目：** A ____ attribute can have only one value.

- a. single-valued
- b. simple
- c. multi-valued
- d. composite

**答案：single-valued。**

Single-valued 讨论“值的数量”；simple attribute 讨论“能否继续拆分”，两者不要混淆。

## Q15 Numeric data

**题目：** Numeric data are data on which you can perform meaningful arithmetic procedures.

- True
- False

**答案：True。**

重点是能进行“有意义”的算术。电话号码虽然由数字组成，但加减乘除无意义，通常应存为字符类型。

## Q16 删除被 FK 引用的父记录

**题目：** Removing a row whose primary-key value is referenced by the foreign-key column of a related table is not permitted because ____.

- a. It violates the key constraint rule.
- b. It violates the domain constraint rule.
- c. It violates the referential integrity rule.
- d. It violates the entity integrity rule.

**答案：it violates the referential integrity rule。**

直接删除会留下 orphan record。解决方法包括拒绝删除、先处理子记录，或明确定义 `ON DELETE CASCADE/SET NULL`。

## Q17 历史数据与趋势预测

**题目：** Which database type stores company historical data and supports statistical analysis to predict future trends for strategic decisions?

- a. Hierarchical database
- b. Data warehouse
- c. Transactional database
- d. Network database

**答案：Data warehouse。**

Data warehouse 整合历史数据，服务分析、统计和战略决策；transactional database 主要处理日常即时交易。

## Q18 1NF 且无 partial dependency

**题目：** A table that is in 1NF and includes no partial dependencies is said to be in ____.

- a. 3NF
- b. UNF
- c. 2NF
- d. 1NF

**答案：2NF。**

Partial dependency 只会在 composite key 场景出现：非键属性只依赖复合键的一部分。

## Q19 Lecturer–Class participation

**题目：** A business rule states: “Each LecturerID is associated with a minimum of 1 and maximum of 3 classes. Each ClassID is associated with one and only one LecturerID.” This is best enforced by:

- a. Making the relationship between LECTURER and CLASS fully optional on both sides.
- b. Making it mandatory on the LECTURER side only.
- c. Making it fully mandatory on both sides.
- d. Making it mandatory on the CLASS side only.

**答案：fully mandatory on both sides。**

- 每个 Lecturer 对应 1..3 个 Class：Lecturer 端最小值为 1。
- 每个 Class 对应 exactly 1 Lecturer：Class 端最小值也为 1。

双方 minimum cardinality 都是 1，所以双方 mandatory。

## Q20 不可再拆分的 attribute

**题目：** A ____ attribute is one that cannot be subdivided.

- a. single-valued
- b. multi-valued
- c. simple
- d. composite

**答案：simple。**

例如 Age 可视为 simple；Address 若可拆成 Street、City、Postcode，则是 composite。

## Q21 Sales Order Normalization（20 分）

**题目：** Normalize the following UNF sales order to 3NF and clearly explain each normalization stage.

**Sales order header**

```text
Customer Number: 1001           Sales Order Number: 405
Customer Name: ABC Company      Sales Order Date: 2/1/2000
Customer Address: 100 Points,   Clerk Number: 210
Manhattan, KS 66502             Clerk Name: Martin Lawrence
```

**Repeating item group**

| Item Ordered | Description | Quantity | Unit Price | Total |
|---:|---|---:|---:|---:|
| 800 | Widget small | 40 | 60.00 | 2,400.00 |
| 801 | Thingimajigger | 20 | 20.00 | 400.00 |
| 805 | Thingibob | 10 | 100.00 | 1,000.00 |

`Order Total = 3,800.00`

Business rules:

- A customer can make many orders; each order belongs to one customer.
- An order can contain many items; an item can occur in many orders.
- Each order is handled by one clerk; a clerk can handle many orders.

### UNF → 1NF

原销售单中 Item Ordered 是 repeating group。将每个 item 展开成一行：

```text
SALES_UNF(
  CustomerNo, CustomerName, CustomerAddress,
  SalesOrderNo, SalesOrderDate,
  ClerkNo, ClerkName,
  ItemNo, ItemDescription, Quantity, UnitPrice,
  LineTotal, OrderTotal
)
```

1NF 的自然 composite key 是 `(SalesOrderNo, ItemNo)`；CustomerNo 和 ClerkNo 不必加入，因为它们由 SalesOrderNo 决定。

### Functional dependencies

```text
CustomerNo → CustomerName, CustomerAddress
ClerkNo → ClerkName
ItemNo → ItemDescription, UnitPrice
SalesOrderNo → SalesOrderDate, CustomerNo, ClerkNo, OrderTotal
(SalesOrderNo, ItemNo) → Quantity, LineTotal
```

并且：

```text
LineTotal = Quantity × UnitPrice
OrderTotal = SUM(LineTotal for the order)
```

后二者是 derived attributes，通常不建议存储。

### 1NF → 2NF

消除对复合键一部分的 partial dependencies：

```text
ITEM(ItemNo PK, ItemDescription, UnitPrice)
SALES_ORDER(SalesOrderNo PK, SalesOrderDate,
            CustomerNo, CustomerName, CustomerAddress,
            ClerkNo, ClerkName, OrderTotal)
SALES_ORDER_DETAIL(SalesOrderNo PK/FK, ItemNo PK/FK, Quantity, LineTotal)
```

### 2NF → 3NF

`SALES_ORDER` 仍有 transitive dependencies：

```text
SalesOrderNo → CustomerNo → CustomerName, CustomerAddress
SalesOrderNo → ClerkNo → ClerkName
```

拆分后的 3NF schema：

```text
CUSTOMER(CustomerNo PK, CustomerName, CustomerAddress)
CLERK(ClerkNo PK, ClerkName)
ITEM(ItemNo PK, ItemDescription, UnitPrice)
SALES_ORDER(SalesOrderNo PK, SalesOrderDate, CustomerNo FK, ClerkNo FK)
SALES_ORDER_DETAIL(SalesOrderNo PK/FK, ItemNo PK/FK, Quantity)
```

`LineTotal` 和 `OrderTotal` 可在查询时计算：

```sql
SELECT d.SalesOrderNo,
       SUM(d.Quantity * i.UnitPrice) AS OrderTotal
FROM SalesOrderDetail AS d
JOIN Item AS i ON i.ItemNo = d.ItemNo
GROUP BY d.SalesOrderNo;
```

Mock suggested answer 在 2NF 和 3NF 展示了相同五张表；考试解释时必须明确指出 Customer、Clerk 的 transitive dependencies，并说明为何拆表，才能稳拿过程分。

## Q22 Patient–Appointment ERD

**题目：** Given the following Patient–Appointment ERD, which statements are correct?

```text
PATIENT(PatientID PK, Name, Gender, ContactNumber)
APPOINTMENT(AppointmentID PK, Date, Time, PatientID FK)
Relationship: Patient makes Appointment
```

1. Appointment is optional to Patient.
2. Appointment is made by one and only one Patient.
3. Patient makes one or many Appointments.
4. Patient is mandatory to Appointment.

- a. ii and iii
- b. i and ii
- c. i, ii and iv
- d. all of the answers

**答案：i, ii, iv。**

- i：Appointment 对 Patient 是 optional——Patient 可以暂时没有 appointment。
- ii：每个 Appointment 由 one and only one Patient 创建。
- iii 错：Patient 是 zero or many appointments，不是 one or many。
- iv：Patient 对 Appointment 是 mandatory——appointment 不可脱离 patient 存在。

## Q23 最不像 data-model business rule

**题目：** Which of the following is least likely to be a business rule as it relates to data modelling?

- a. A machine operator may not work more than 10 hours in a 24-hour period.
- b. Casual Fridays take place in the summer.
- c. A training session cannot be scheduled for fewer than 10 or more than 30 employees.
- d. A customer may make many payments on an account.

**答案：Casual Fridays take place in the summer。**

其余规则都能影响数据库中的 entity、relationship 或 constraint，例如工时上限、培训人数范围、客户付款关系。Casual Friday 更像组织政策，无法自然映射为此题语境中的数据模型结构。

---

# 考前自测清单

1. 能否看到 M:N 就立即画 bridge table，并把两端 PK 带入成为 PK/FK？
2. 能否从业务规则写出 min/max cardinality，例如 `0..N`、`1..1`、`1..5`？
3. 能否先写 functional dependencies，再解释 partial 与 transitive dependency？
4. 会不会在 aggregate 条件中使用 `HAVING`，并正确写 `GROUP BY`？
5. 建表时是否写了 PK、FK、`NOT NULL`、匹配的数据类型，以及合理的 `CHECK`？
6. 是否分清 single-valued vs simple、candidate vs composite、entity vs referential integrity？

建议复习顺序：先闭卷做两套选择题，再重写 Mock 1 Q3/Q9/Q13 和 Mock 2 Q4/Q12/Q21；这些大题覆盖 normalization、ERD 和 SQL 三个核心板块。

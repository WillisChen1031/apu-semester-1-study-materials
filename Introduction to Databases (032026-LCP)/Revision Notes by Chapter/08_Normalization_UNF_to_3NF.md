# Lecture 8 - Normalization: UNF to 3NF

## 本章要会

这是 Database 最重要的大题之一。Mock 直接考了：给 UNF，要求 normalise into 3NF，并 clearly show functional dependencies and steps。

## Normalization 是什么

Normalization = process for evaluating and correcting table structures to minimize data redundancy and reduce data anomalies。

目标：

- reduce redundancy
- reduce update/insert/delete anomalies
- make each table represent one subject
- make attributes depend on the key

## Functional Dependency

`A -> B` means knowing A allows you to determine B。

Mock 题：

> A determines B means knowing A, you can look up B.

例子：

```text
StudentID -> StudentName, EnrollYear
SubjectID -> SubjectName
TeacherID -> TeacherName
StudentID, SubjectID -> Mark
```

## Determinant

Determinant = left side of functional dependency。

例子：

```text
TeacherID -> TeacherName
```

`TeacherID` is determinant。

## UNF

UNF = Un-Normalized Form。

特点：

- repeating groups
- multiple values in one cell/section
- report-like format
- may have blanks/nulls due to repeated group

做题第一步：flatten table。

## 1NF

1NF 要求：

- each cell has single value
- no repeating groups
- every row is complete
- identify primary key, often composite key

从 UNF 到 1NF：

1. 把 repeating group 展开成多行。
2. 补齐每一行重复出现的 parent data。
3. 每个 intersection 只有一个 value。
4. 找 composite primary key。

## 2NF

2NF 要求：

- already in 1NF
- no partial dependency

Partial dependency 只会在 composite primary key 时重点出现。

中文理解：如果 PK 是 `(A, B)`，但某个 non-key attribute 只依赖 A 或只依赖 B，就违反 2NF。

例子：

```text
PK: StudentID + SubjectID

StudentID -> StudentName
SubjectID -> SubjectName
StudentID + SubjectID -> Mark
```

`StudentName` 只依赖 `StudentID`，不是整个 composite PK，所以要拆。

## 3NF

3NF 要求：

- already in 2NF
- no transitive dependency

Transitive dependency:

```text
PK -> non-key attribute -> another non-key attribute
```

例子：

```text
EmpNum -> JobClass
JobClass -> ChgHour
```

所以：

```text
EmpNum -> ChgHour
```

这是 transitive dependency，需要拆出：

```text
JobRate(JobClass, ChgHour)
Employee(EmpNum, EmpName, JobClass)
```

## 考试答题模板

### Step 1: UNF to 1NF

写：

```text
Remove repeating groups. Ensure each cell contains a single value.
```

然后列出 1NF relation：

```text
R(StudentID, SubjectID, SubjectName, Mark, StuFirstName, StuLastName, StuEnrollYear, TeachID, TeachFirstName, TeachLastName)
PK: StudentID + SubjectID
```

如果题目/答案把 `TeachID` 也放进 composite PK，要跟题目数据逻辑解释清楚。但通常 mark 是由 student + subject 决定，teacher 是 subject 的属性。

### Step 2: Identify Functional Dependencies

```text
StudentID -> StuFirstName, StuLastName, StuEnrollYear
SubjectID -> SubjectName, TeachID
TeachID -> TeachFirstName, TeachLastName
StudentID, SubjectID -> Mark
```

### Step 3: 1NF to 2NF

Remove partial dependencies：

```text
Student(StudentID, StuFirstName, StuLastName, StuEnrollYear)
Subject(SubjectID, SubjectName, TeachID)
StudentMark(StudentID, SubjectID, Mark)
Teacher(TeachID, TeachFirstName, TeachLastName)
```

如果 `TeachID -> TeachName` 被当作 transitive dependency，也可以先在 2NF 保留在 Subject，然后 3NF 再拆。考试重点是最终 3NF 合理。

### Step 4: 2NF to 3NF

Remove transitive dependencies：

```text
SubjectID -> TeachID
TeachID -> TeachFirstName, TeachLastName
```

Final 3NF:

```text
Student(StudentID PK, StuFirstName, StuLastName, StuEnrollYear)
Teacher(TeachID PK, TeachFirstName, TeachLastName)
Subject(SubjectID PK, SubjectName, TeachID FK)
StudentMark(StudentID PK/FK, SubjectID PK/FK, Mark)
```

## Mock Normalization Example

Mock assumptions:

- Student can take multiple subjects.
- Each subject taught by one teacher.
- Teacher can teach multiple subjects.

Final 3NF answer:

```text
Student(StudentID PK, StuFirstName, StuLastName, StuEnrollYear)
Teacher(TeachID PK, TeachFirstName, TeachLastName)
Subject(SubjectID PK, SubjectName, TeachID FK)
StudentMark(StudentID PK/FK, SubjectID PK/FK, Mark)
```

Functional dependencies:

```text
StudentID -> StuFirstName, StuLastName, StuEnrollYear
SubjectID -> SubjectName, TeachID
TeachID -> TeachFirstName, TeachLastName
StudentID, SubjectID -> Mark
```

## Project Normalization Example

UNF/1NF attributes:

```text
ProNum, ProName, EmpNum, EmpName, JobClass, ChgHour, HourBill, TotChar, SubTot
```

Composite PK:

```text
ProNum + EmpNum
```

Dependencies:

```text
ProNum -> ProName, SubTot
EmpNum -> EmpName, JobClass
JobClass -> ChgHour
ProNum, EmpNum -> HourBill, TotChar
```

2NF after removing partial dependency:

```text
Project(ProNum PK, ProName, SubTot)
Employee(EmpNum PK, EmpName, JobClass, ChgHour)
ProjectWork(ProNum PK/FK, EmpNum PK/FK, HourBill, TotChar)
```

3NF after removing transitive dependency:

```text
Project(ProNum PK, ProName, SubTot)
Employee(EmpNum PK, EmpName, JobClass FK)
Rate(JobClass PK, ChgHour)
ProjectWork(ProNum PK/FK, EmpNum PK/FK, HourBill, TotChar)
```

## 口诀

- 1NF: 一格一个值，no repeating group。
- 2NF: 非主键属性必须依赖整个 composite key。
- 3NF: 非主键属性不能依赖另一个非主键属性。

## 易错点

- 不写 functional dependencies 会丢很多分。
- 2NF 不是随便拆表，是 remove partial dependency。
- 3NF 是 remove transitive dependency。
- 有些题没有 transitive dependency，可以写：No transitive dependency, therefore tables are already in 3NF。
- Bridge table / transaction table 常常有 composite PK。


# Lecture 2 - File System and DBMS Functions

## 本章要会

这一章考 file system problems、data redundancy、data anomalies、DBMS functions。Mock 已经考过 file system limitation 和 anomaly。

## File System Problems

File system 用文件分散存数据，问题很多：

- difficult administration
- hard to change file structure
- weak security
- data redundancy
- data inconsistency
- program-data dependence
- lack of data sharing

Mock 题：

> Which of the following is a limitation of the file system environment?

Answer: security features are likely to be inadequate

## Data Redundancy

Data redundancy = same data stored in many places。

中文理解：同一个顾客地址出现在多个文件里，一改要改很多地方。

坏处：

- waste storage
- harder update
- inconsistent data

## Data Anomalies

Anomaly = abnormal problem caused by poor table/file design。

| Anomaly | 中文理解 | Example |
|---|---|---|
| Update anomaly | 更新异常 | 一个地址要改多次，漏改导致不一致 |
| Insertion anomaly | 插入异常 | 没有订单就不能加入新客户 |
| Deletion anomaly | 删除异常 | 删除最后一个订单时把客户资料也删了 |

Mock 题：

> Which of the following is NOT a data anomaly?

Answer: create

因为常见 anomaly 是 update, insertion, deletion。

## Database System Environment

Components:

- hardware
- software
- people
- procedures
- data

## DBMS Functions

| Function | 中文理解 |
|---|---|
| Data dictionary management | 管 metadata |
| Data storage management | 管数据存储 |
| Data transformation and presentation | 数据转换/展示 |
| Security management | 权限和安全 |
| Multiuser access control | 多用户并发控制 |
| Backup and recovery | 备份和恢复 |
| Data integrity management | 数据完整性 |
| Database access languages/API | SQL/API |
| Communication interfaces | 通信接口 |

Mock 题：

> The DBMS stores definitions of the data elements and their relationships in a ___.

Answer: data dictionary

## 易错点

- Redundancy 不一定等于重复行，它指数据重复存放。
- Inconsistency 通常由 redundancy 引起。
- Delete anomaly 是删除不该丢的信息，不是 SQL `DELETE` 本身。
- Data dictionary 存的是 definitions/metadata，不是普通 business data。


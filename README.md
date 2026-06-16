# APU Semester 1 Study Materials

本仓库用于存放 APU Semester 1 的课程资料与复习重点。

> 说明：`Digital Thinking and Innovation (032026-SIM)` 资料保留在目录中，但本 README 的考点总结按要求不覆盖该科目。

## 目录结构

- `Programming with Python (032026-ANP)/`
  - `Lecture Slides/`
  - `Lab Exercises/`
  - `Tutorial Exercises/`
- `Introduction to Networking (032026-YWR)/`
  - `Lecture Slides/`
  - `MOCK TEST/`
- `Introduction to Databases (032026-LCP)/`
  - `Lecture Slides/`
  - `Lab Exercises/`
  - `MOCK_TEST/`
  - `Digital Thinking and Innovation (032026-SIM)/`

## 复习优先级

1. 先刷 mock test 中已经出现过的题型：Networking 和 Database。
2. Python 没有 mock test，优先按 lecture topics + lab/tutorial 练代码题。
3. 对每一科都要会“解释概念 + 看图/看表作答 + 写/读代码或 SQL”。

## Programming with Python (032026-ANP)

Python 没有模拟测试，因此以下考点按 lecture slides、lab exercises、tutorial MCQ 综合整理，越靠前越需要熟练。

### 1. Problem Solving, Algorithm, Pseudocode, Flowchart

- algorithm 的定义：输入、处理、输出，步骤必须清晰、无歧义、有正确顺序。
- 程序开发步骤：define problem、outline solution、develop algorithm、code、run/test、document/maintain。
- pseudocode 基本结构：`START` / `END`、`READ`/`INPUT`、`DISPLAY`/`PRINT`、assignment、calculation。
- flowchart 基本符号：terminal、input/output、process、decision、connector。
- 会追踪 trace table：给定输入，按流程图或 pseudocode 写出变量变化与输出。
- sequential structure：语句按顺序执行；常见题型是面积、周长、总价、平均值计算。
- selection 与 repetition 在算法中的表示：`IF...THEN...ELSE...ENDIF`、`WHILE...ENDWHILE`、`FOR...ENDFOR`。

### 2. Python Basics, Variables, Types, Expressions

- Python 是 interpreted language；会区分 compiler vs interpreter、IDE、source code、machine code。
- interactive mode / REPL 与 script mode 的区别。
- `print()`、`input()` 的用法；`input()` 读入默认是 string。
- variable assignment：右边 expression 先计算，再赋值给左边变量。
- variable naming：大小写敏感，不能用 reserved keywords，命名要有意义。
- reserved words：`if`、`else`、`elif`、`for`、`while`、`def`、`return`、`try`、`except`、`class` 等。
- 常见 types：`int`、`float`、`str`、`bool`、`list`、`tuple`、`set`、`dict`。
- type checking：`type(x)`。
- type casting：`int()`、`float()`、`str()`；要知道不能把无效字符串转数字，例如 `int("hello")`。
- arithmetic operators：`+`、`-`、`*`、`/`、`//`、`%`、`**`。
- precedence：parentheses、power、multiplication/division/modulus、addition/subtraction、left-to-right。
- comparison operators：`>`、`>=`、`<`、`<=`、`==`、`!=`。
- logical operators：`and`、`or`、`not`；会判断 truth table。

### 3. Conditional Statements

- one-way decision：`if condition:`
- two-way decision：`if...else`
- multi-way decision：`if...elif...else`
- nested if：linear nested 与 non-linear nested。
- indentation 是 Python block 的关键；考试很可能考输出或改错。
- `pass` 的作用：空 block 占位。
- 能写常见判断题：
  - odd/even：`num % 2 == 0`
  - positive/negative/zero
  - pass/fail grading
  - range checking
  - combined conditions：`and` / `or`
- 会读流程图并转换成 Python conditional code。

### 4. Repetition / Loops

- pre-test loop：Python 的 `while` 和 `for` 都是先检查条件再执行。
- Python 没有内建 post-test loop，但可用 `while` 模拟。
- `while` loop 必须有 initialization、condition、body、update。
- infinite loop 常见原因：
  - loop control 没有 update
  - update 方向让条件永远成立
- `for variable in sequence:` 用于遍历 sequence。
- `range(start, stop, step)`：stop 不包含在内；会写递增、递减、指定步长。
- sentinel loop：用特殊输入结束，例如输入负数或 `done`。
- nested loops：内层循环总执行次数通常是 outer times inner。
- `break`：直接结束当前 loop。
- `continue`：跳过本轮剩余语句，进入下一轮。
- `while...else` 的执行逻辑。
- 常见 loop pattern：
  - sum / total
  - count
  - average
  - max / min
  - filter values
  - validate input until legal
  - menu selection loop

### 5. Functions

- function definition：`def name(parameters):`
- function call / invocation。
- parameter 与 argument 的区别。
- no-parameter function、parameterized function。
- fruitful function：有 `return`，会返回结果。
- void / non-fruitful function：主要执行动作，例如 `print()`。
- `return` 会结束 function execution。
- scope：function 内的局部变量与外部变量的关系。
- mutable vs immutable passing behavior：
  - list 等 mutable object 在函数内修改会影响原对象。
  - int/string/tuple 等 immutable object 在函数内重新赋值通常不改变外部对象。
- built-in functions：`len()`、`range()`、`type()`、`int()`、`float()`、`str()`、`max()`、`min()`、`sum()`。
- 会把重复代码改写成 function。

### 6. Strings

- string 是 character sequence，可用 index 访问。
- forward index 从 `0` 开始；negative index 从 `-1` 开始。
- slicing：`s[start:end]`，end 不包含。
- 常见 slice：`s[:3]`、`s[3:]`、`s[:-1]`、`s[:]`。
- string immutable：不能 `s[0] = "x"`，只能创建新字符串。
- escape sequences：`\\`、`\'`、`\"`、`\n`、`\t`。
- string operators：
  - concatenation：`+`
  - repetition：`*`
  - membership：`in`
- loop through string：`for ch in s` 或 `for i in range(len(s))`。
- 常见 methods：
  - `upper()`、`lower()`、`capitalize()`、`swapcase()`
  - `strip()`、`lstrip()`、`rstrip()`
  - `find()`、`count()`
  - `startswith()`、`endswith()`
  - `replace()`
  - `split()`、`join()`
  - `isdigit()`、`isalpha()`、`isalnum()`、`isspace()`
- `find()` 找不到返回 `-1`；`index()` 找不到会报错。
- `format()` 或 formatted output 的基本用法。

### 7. Lists

- list 是 mutable sequence，用 square brackets：`[]`。
- 可混合存储不同类型，但考试题通常用同类型数字或字符串。
- indexing / negative indexing / slicing 与 string 类似。
- list mutable：可以修改元素。
- append vs concatenate：
  - `append(x)` 把一个元素加到末尾。
  - `+` 或 `extend()` 合并 list。
- 常见 methods：
  - `append()`、`insert()`、`remove()`、`pop()`
  - `extend()`、`count()`、`index()`
  - `sort()`、`reverse()`
- built-in functions：`len()`、`max()`、`min()`、`sum()`。
- list traversal：
  - `for item in list`
  - `for i in range(len(list))`
- string/list conversion：`split()` 把 string 分成 list；`join()` 把 list 合成 string。
- 常见题型：
  - search an item
  - count occurrence
  - compute average from user input
  - update every element
  - compare list and string mutability

### 8. Tuples, Sets, Dictionaries

- tuple：
  - 用 `()`，ordered，immutable。
  - 支持 indexing、slicing、loop、`len()`。
  - methods 少，主要是 `count()`、`index()`。
  - tuple 可比较，按元素顺序比较。
- tuple vs list：
  - list mutable，tuple immutable。
  - tuple 通常更适合固定数据。
- set：
  - 用 `{}` 或 `set()`；empty set 必须用 `set()`，`{}` 是 empty dict。
  - unordered、no duplicate、不支持 indexing。
  - element 必须 hashable，不能放 list。
  - operations：union `|`、intersection `&`、difference `-`、symmetric difference `^`。
  - 常见用途：去重、统计 unique characters。
- dictionary：
  - key-value pairs：`{key: value}`。
  - 通过 key 访问 value：`d[key]` 或 `d.get(key)`。
  - `d[key]` key 不存在会 `KeyError`；`get()` 默认返回 `None`。
  - add/update：`d[key] = value`。
  - delete：`pop()`、`popitem()`、`clear()`。
  - iteration：loop keys、`items()` loop key/value。
  - common methods：`keys()`、`values()`、`items()`、`update()`、`copy()`、`fromkeys()`。
  - 常见题型：frequency counting，例如 character count / word count。

### 9. File Handling and Exception Handling

- `open(filename, mode)`；default mode 是 read。
- modes：
  - `r` read only，file must exist。
  - `w` write only，会 overwrite existing data。
  - `a` append，写到文件末尾。
  - `w+`、`r+`、`a+` 读写模式。
  - binary mode：`rb`、`wb`、`ab`。
  - `x` exclusive creation，文件存在则报错。
- 写文件：`write()`，注意 newline `\n`。
- 读文件：
  - `read()` 全部读成 string。
  - `readline()` 读下一行。
  - `readlines()` 读成 list。
  - `for line in file:` 逐行处理。
- `close()` 的作用；也要知道 `with open(...) as f:` 更安全。
- line processing：
  - count lines
  - `rstrip()` 去掉换行
  - `startswith()`
  - `in` 检查 substring
  - `continue` 跳过不符合条件的行
- exception handling：
  - `try...except`
  - 处理文件不存在、输入转换错误等。
  - 常见错误：`IOError`/`FileNotFoundError`、`ValueError`、`TypeError`、`KeyError`。

## Introduction to Networking (032026-YWR)

Networking 有 mock test 截图，以下 “高频” 项目需要优先掌握。

### 高频考点：Mock Test 已覆盖/高度相关

- OSI model 与 TCP/IP model：
  - OSI 7 layers 顺序与功能。
  - TCP/IP model layers 与 OSI mapping。
  - PDU names：data、segment、packet、frame、bits。
  - encapsulation / de-encapsulation。
- protocols and standards：
  - protocol 的作用：addressing、reliability、flow control、sequencing、error detection。
  - standards bodies：IETF、ICANN、IEEE、IANA 等。
- IPv4 addressing and subnetting：
  - network portion / host portion。
  - subnet mask 与 prefix notation。
  - 给定 IP + mask，计算 network address、broadcast address、first/last usable host、number of hosts。
  - 判断两个 IP 是否在同一 subnet。
  - default gateway 的作用。
- Ethernet / MAC / ARP：
  - MAC address 长度、格式、作用。
  - frame basics。
  - ARP：IPv4 address 到 MAC address 的解析。
  - ARP table / ARP cache。
- switching basics：
  - switch 依据 MAC address table 转发。
  - unknown unicast / broadcast / flooding。
  - collision domain 与 broadcast domain。
- transport layer：
  - TCP vs UDP。
  - TCP reliable delivery、acknowledgement、sequence number、flow control。
  - UDP connectionless、low overhead、best effort。
  - port number 的作用。
- application layer protocols and ports：
  - HTTP 80、HTTPS 443。
  - FTP control 21 / data 20。
  - SMTP 25、POP3 110、IMAP 143。
  - DNS 53。
  - DHCP 67/68。
  - SSH 22、Telnet 23。
- DHCP：
  - DHCP Discover、Offer、Request、ACK。
  - DHCP 分配 IPv4 address、subnet mask、gateway、DNS。
  - static vs dynamic addressing。
- DNS：
  - FQDN 到 IP address 的解析。
  - records：A、AAAA、NS、MX。
  - `nslookup` 用途。
- small network troubleshooting：
  - `ping`、`tracert`/`traceroute`。
  - `ipconfig`/`ifconfig`。
  - `arp -a`。
  - Cisco show commands：`show running-config`、`show interfaces`、`show ip interface brief`、`show arp`、`show ip route`、`show protocols`、`show version`。
- network security basics：
  - 常见 threat：malware、unauthorized access、DoS、data theft。
  - security controls：firewall、ACL、authentication、encryption、patching、backup。

### Chapter-by-Chapter 考点

#### Chapter 1: Networking Today

- network components：
  - end devices：PC、server、printer、IP phone。
  - intermediary devices：switch、router、wireless AP、firewall。
  - network media：copper、fiber、wireless。
- host roles：client、server、peer-to-peer。
- LAN vs WAN：
  - LAN limited area, usually single organization。
  - WAN larger geographic area, connects LANs, often service provider managed。
- internet / intranet / extranet。
- network representations：
  - NIC、physical port、interface。
  - physical topology vs logical topology。
- reliable network characteristics：
  - fault tolerance、scalability、QoS、security。
- trends：BYOD、cloud、online collaboration、video communication。

#### Chapter 2: Protocols and Models

- communication rules：
  - message encoding、formatting、size、timing、delivery option。
  - unicast、multicast、broadcast。
- protocol suite 的概念。
- OSI model layer functions。
- TCP/IP model layer functions。
- data encapsulation process。
- local vs remote communication：
  - local network 用 MAC 直接交付。
  - remote network 交给 default gateway。

#### Chapter 3: IPv4

- IPv4 dotted decimal 与 binary conversion。
- subnet mask 的意义。
- network, host, broadcast address。
- private IPv4 ranges：
  - `10.0.0.0/8`
  - `172.16.0.0/12`
  - `192.168.0.0/16`
- public vs private IP。
- unicast、broadcast、multicast。
- APIPA：`169.254.0.0/16`。
- subnetting 必练：
  - `/24`、`/25`、`/26`、`/27`、`/28`、`/29`、`/30`
  - block size
  - usable host count: `2^host_bits - 2`

#### Chapter 4: Physical Layer

- physical layer function：传输 bits。
- bandwidth、throughput、goodput。
- copper media：
  - UTP、STP、coaxial。
  - EMI/RFI、crosstalk。
- fiber media：
  - light pulses、long distance、high bandwidth。
  - single-mode vs multimode basic difference。
- wireless media：
  - radio frequency。
  - interference、coverage、security concern。
- encoding/signaling 的基本概念。

#### Chapter 5: Data Link Layer

- data link layer function：
  - framing
  - media access control
  - error detection
- LLC vs MAC sublayers。
- frame fields：header、data、trailer。
- access control methods：
  - contention-based
  - controlled access
- topology：
  - physical topology
  - logical topology
- WAN data link basics。

#### Chapter 6: Ethernet

- Ethernet frame 与 MAC address。
- MAC address：48-bit / 12 hex digits。
- destination MAC / source MAC。
- switch MAC address table learning：
  - source MAC 学习。
  - destination MAC 查表转发。
  - unknown destination flooding。
- ARP request 是 broadcast，ARP reply 是 unicast。
- Ethernet switching forwarding methods：
  - store-and-forward
  - cut-through
- auto-MDIX、duplex、speed 等基础概念。

#### Chapter 7: IPv6

- IPv6 address 长度：128-bit。
- hexadecimal notation，colon-separated。
- zero compression：
  - leading zero 可省略。
  - consecutive zero groups 可用 `::`，但只能用一次。
- IPv6 address types：
  - global unicast
  - link-local
  - multicast
  - anycast
- IPv6 没有 broadcast。
- prefix length，例如 `/64`。
- SLAAC、DHCPv6、router advertisement 的基本概念。
- IPv4 vs IPv6 差异。

#### Chapter 8: Transport Layer

- transport layer responsibilities：
  - tracking individual conversations
  - segmentation and reassembly
  - identifying applications via port numbers
  - multiplexing
- TCP：
  - connection-oriented
  - reliable
  - ordered delivery
  - flow control
  - three-way handshake
- UDP：
  - connectionless
  - no guarantee
  - lower overhead
  - used for DNS, DHCP, streaming, VoIP 等场景。
- port ranges：
  - well-known ports: 0-1023
  - registered ports: 1024-49151
  - dynamic/private ports: 49152-65535

#### Chapter 9: Application Layer

- application / presentation / session layer in OSI 对应 TCP/IP application layer。
- client-server model vs peer-to-peer。
- HTTP methods：GET、POST、PUT。
- email protocols：
  - SMTP send mail。
  - POP retrieve and usually remove from server。
  - IMAP retrieve while keeping mail on server。
- DNS hierarchy 与 DNS message sections。
- DHCP operation。
- FTP two connections：control and data。
- SMB file/printer sharing。

#### Chapter 10: Build a Small Network

- small network topology and device selection。
- IP addressing plan。
- redundancy and traffic management。
- QoS concept。
- verifying connectivity：
  - ping
  - extended ping
  - traceroute/tracert
- network baseline。
- host commands and Cisco IOS show commands。
- troubleshooting methodology：
  1. identify the problem
  2. establish theory
  3. test theory
  4. establish plan and implement
  5. verify and prevent
  6. document findings
- common scenarios：
  - wrong IP/subnet mask
  - wrong/missing default gateway
  - DHCP issue
  - APIPA address

#### Chapter 11: Network Security Fundamentals

- security goals：confidentiality、integrity、availability。
- threat actors and attacks。
- malware types and social engineering basics。
- access control and authentication。
- firewall, ACL, VPN, encryption basics。
- device hardening：
  - strong passwords
  - disable unused services
  - update/patch
  - backup
  - secure remote access with SSH instead of Telnet。

## Introduction to Databases (032026-LCP)

Database 有 mock test 截图，重点非常集中：概念、ERD、normalization、SQL。

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

## 最后冲刺建议

- Networking：每天做一轮 subnetting，做到能快速算 network/broadcast/usable range。
- Database：每天至少写 10 条 SQL，覆盖 `WHERE`、`JOIN`、`GROUP BY`、aggregate。
- Python：每天写 5 个小程序，覆盖 condition、loop、function、list/dict、file handling。
- 所有科目都要练“看题解释为什么”，不是只背定义。

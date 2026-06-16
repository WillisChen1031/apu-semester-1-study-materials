## Programming with Python (032026-ANP)

[返回总 README](../README.md)

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

## 推荐教程与覆盖判断

### 结论

[廖雪峰 Python 教程](https://liaoxuefeng.com/books/python/history/index.html) 可以覆盖 Python 考点大约 75%-80%，但不能完全替代课件。

它覆盖：变量、类型、字符串、list/tuple、dict/set、条件、循环、函数、错误处理、文件读写。

它不足：algorithm、pseudocode、flowchart、trace table、sentinel loop、按流程图追踪输出。这些更像 APU 第一学期考试题，必须回到 `Lecture Slides/Topic 1.pptx`、`Topic 2 - Student Copy.pptx` 和 `Lab Exercises/Lab 2 Problem Solving and Algorithm.docx`。

### B站视频

- [黑马程序员 Python 零基础教程](https://search.bilibili.com/all?keyword=%E9%BB%91%E9%A9%AC%E7%A8%8B%E5%BA%8F%E5%91%98%20Python%20%E9%9B%B6%E5%9F%BA%E7%A1%80)：适合补变量、判断、循环、函数、列表、字典、文件。
- [Python 函数 列表 字典 文件 异常 B站搜索](https://search.bilibili.com/all?keyword=Python%20%E5%87%BD%E6%95%B0%20%E5%88%97%E8%A1%A8%20%E5%AD%97%E5%85%B8%20%E6%96%87%E4%BB%B6%20%E5%BC%82%E5%B8%B8)：适合按薄弱点补。
- [Python 流程图 伪代码 算法 B站搜索](https://search.bilibili.com/all?keyword=Python%20%E6%B5%81%E7%A8%8B%E5%9B%BE%20%E4%BC%AA%E4%BB%A3%E7%A0%81%20%E7%AE%97%E6%B3%95)：专门补廖雪峰没有覆盖好的考试逻辑题。

### YouTube 视频

- [freeCodeCamp Python for Beginners](https://www.youtube.com/results?search_query=freeCodeCamp+Python+for+Beginners+full+course)：完整英文入门课，适合系统补语法。
- [Programming with Mosh Python for Beginners](https://www.youtube.com/results?search_query=Programming+with+Mosh+Python+for+Beginners)：讲得快，适合快速复习。
- [Python file handling exceptions tutorial](https://www.youtube.com/results?search_query=Python+file+handling+exceptions+tutorial)：专门补文件和异常。

### 文字教程/博客

- [廖雪峰 Python 教程](https://liaoxuefeng.com/books/python/history/index.html)：主线教程。
- [W3Schools Python](https://www.w3schools.com/python/)：查语法和小例子。
- [Python 官方教程](https://docs.python.org/3/tutorial/)：权威但偏英文，适合查细节。

### 最短学习路线

1. 先看廖雪峰：基础、函数、list/tuple、dict/set、错误处理、文件读写。
2. 回到课件 Topic 1-2：algorithm、pseudocode、flowchart、trace table。
3. 做 lab/tutorial：尤其是 condition、loop、function、string、list、file handling。
4. 考前重点练“给代码写输出”和“给流程图写输出”。

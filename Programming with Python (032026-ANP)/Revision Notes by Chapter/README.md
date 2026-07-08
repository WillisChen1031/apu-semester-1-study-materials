# Programming with Python 复习笔记

这套笔记按课件 Topic 1-11 拆分，一章一个 Markdown。写法参考了 lecture slides、lab/pre-lab/tutorial，以及 mock test 的题型。

复习重点不是背概念，而是会判断代码对不对、会 trace output、会把题目直接写成 Python code。

## Mock 覆盖范围

| 范围 | Mock 常见问法 | 复习时要练 |
|---|---|---|
| input / print / len | 写代码读取 TP number 并输出长度 | `input()` 得到 string，`len()` 用法 |
| assignment / expression | 按要求写赋值语句 | 右边先算，左边必须是变量 |
| syntax error fixing | 修正缺冒号、括号、缩进、`print` | 看到代码先查 `:`, `()`, indentation |
| if / elif | 判断输出、写 grade program | 条件顺序，从具体/高分到低分 |
| function | `def`, `return`, scope, output tracing | 函数没有 `return` 就不会把结果带回去 |
| string | `capitalize()`, slicing, quote error | index 从 0 开始，slice 不含 end |
| list | slicing, `insert`, sum loop | 空 list 不能直接 `myList[0] = x` |
| tuple/set/dict | 识别 `()`, `[]`, `{}` | tuple immutable，set no duplicate，dict key-value |
| file handling | `open("data.txt", "r")`, append mode | `r/w/a/x`, `read/readline/readlines/write` |

## 建议复习顺序

1. 先看 Topic 3-5：基础语法、变量、条件，这是 mock 的最大基础。
2. 再看 Topic 6-9：loop、function、string、list，这是直接写代码最多的部分。
3. 最后看 Topic 10-11：tuple/set/dict 和 file handling，mock 会考识别、mode、简单代码。
4. Topic 1-2 不要死背，用来练 pseudocode、flowchart、trace table 和把算法翻译成代码。

## 文件目录

- [01_Problem_Solving_and_Algorithm.md](01_Problem_Solving_and_Algorithm.md)
- [02_Control_Structure_Algorithm.md](02_Control_Structure_Algorithm.md)
- [03_Introduction_to_Python.md](03_Introduction_to_Python.md)
- [04_Variables_Expressions_Statements.md](04_Variables_Expressions_Statements.md)
- [05_Conditional_Statements.md](05_Conditional_Statements.md)
- [06_Repetition_Loops.md](06_Repetition_Loops.md)
- [07_Functions.md](07_Functions.md)
- [08_Strings.md](08_Strings.md)
- [09_Lists.md](09_Lists.md)
- [10_Tuples_Sets_Dictionaries.md](10_Tuples_Sets_Dictionaries.md)
- [11_File_and_Exception_Handling.md](11_File_and_Exception_Handling.md)


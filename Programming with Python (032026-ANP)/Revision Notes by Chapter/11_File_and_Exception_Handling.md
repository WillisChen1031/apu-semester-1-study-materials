# Topic 11 - File and Exception Handling

## 你要会什么

File handling 是 mock 高频识别题，也可能出写代码：create/write/read/copy/count lines/filter lines/append data。Tutorial MCQ 重点是 `open()`, mode, `read/readline/readlines/write/close`。

英文关键词：

- file handling: read from and write to files
- open: access a file
- read mode: read file content
- write mode: write and overwrite
- append mode: add data at the end
- exception handling: handle runtime errors

## open() 基本格式

```python
file = open("data.txt", "r")
```

Mock 问：open `data.txt` for reading。

答案：

```python
file = open("data.txt", "r")
```

## File Modes

| Mode | Meaning | Important |
|---|---|---|
| `"r"` | read | file must exist |
| `"w"` | write | overwrite existing content |
| `"a"` | append | add to end |
| `"x"` | create | error if file exists |
| `"r+"` | read and write | file must exist |
| `"w+"` | write and read | overwrite |
| `"a+"` | append and read | append to end |
| `"rb"` | read binary | binary file |
| `"wb"` | write binary | binary file |

Mock append mode 可能选 `a+`。

## Write File

```python
file = open("student.txt", "w")
file.write("My name is Ali.\n")
file.write("I am studying Python.\n")
file.close()
```

注意：`write()` 不会自动换行，要自己写 `\n`。

## Read File

Read whole file：

```python
file = open("student.txt", "r")
content = file.read()
print(content)
file.close()
```

Read one line：

```python
file = open("student.txt", "r")
line = file.readline()
print(line)
file.close()
```

Read all lines as list：

```python
file = open("student.txt", "r")
lines = file.readlines()
print(lines)
file.close()
```

Loop line by line：

```python
file = open("student.txt", "r")

for line in file:
    print(line.rstrip())

file.close()
```

## with open 推荐写法

`with` 会自动 close file。

```python
with open("student.txt", "r") as file:
    content = file.read()
    print(content)
```

考试如果没要求，`open()` + `close()` 也可以，但 `with` 更稳。

## Lab 题型模板

### Create File

```python
file = open("test.txt", "x")
file.close()
print("File created successfully.")
```

### Copy File

```python
source = open("original.txt", "r")
target = open("copy.txt", "w")

for line in source:
    target.write(line)

source.close()
target.close()
```

### Count Lines, Words, Characters

```python
with open("data.txt", "r") as file:
    lines = file.readlines()

line_count = len(lines)
word_count = 0
char_count = 0

for line in lines:
    word_count += len(line.split())
    char_count += len(line)

print("Lines:", line_count)
print("Words:", word_count)
print("Characters:", char_count)
```

### Copy Only Lines Starting With A

```python
with open("names.txt", "r") as infile:
    with open("a_names.txt", "w") as outfile:
        for line in infile:
            if line.startswith("A"):
                outfile.write(line)
```

### Display Students Scored More Than 70

File content:

```text
Ali,80
Bala,65
Chen,90
Devi,55
```

Code:

```python
with open("marks.txt", "r") as file:
    for line in file:
        name, score = line.strip().split(",")
        score = int(score)
        if score > 70:
            print(name, "scored", score)
```

## Exception Handling

Basic syntax：

```python
try:
    num = int(input("Enter number: "))
    print(10 / num)
except ValueError:
    print("Please enter a valid number")
except ZeroDivisionError:
    print("Cannot divide by zero")
```

File not found：

```python
try:
    file = open("data.txt", "r")
    print(file.read())
    file.close()
except FileNotFoundError:
    print("File not found")
```

## Common Exceptions

| Exception | When it happens |
|---|---|
| `ValueError` | `int("hello")` |
| `TypeError` | `2 + "2"` |
| `FileNotFoundError` | open missing file in read mode |
| `KeyError` | dictionary key not found |
| `IndexError` | list index out of range |

## 易错点

- `"w"` 会清空旧内容。
- `"r"` 打开不存在的文件会 error。
- `read()` returns string。
- `readline()` returns next line。
- `readlines()` returns list of lines。
- `write()` 只能写 string，数字要 `str()`。
- 处理每一行时常用 `strip()` 或 `rstrip()` 去掉换行。


# Topic 4 - Variables, Expressions and Statements

## 你要会什么

这一章是 mock 的基础分：变量命名、赋值、type conversion、operators、expression tracing。

英文关键词：

- variable: name that stores a value
- assignment statement: store result into variable
- expression: combination of values/operators that produces a value
- type conversion / casting: convert one type to another
- keyword: reserved word in Python

## Variable Assignment

赋值语句的规则：

```python
variable = expression
```

右边先计算，再把结果放进左边变量。

```python
num1 = 10
num2 = num1 + 2
num1 = num2 * 4
```

Mock 类似题：

```python
num2 = num1 + 2
num1 = num2 * 4
num2 = num1 / 2.9
num1 = num2 - 8
```

## Variable Naming

可以：

```python
student_name = "Ali"
score1 = 80
total_marks = 250
```

不可以：

```python
1score = 80      # cannot start with number
student name = "Ali"  # no space
if = 10          # keyword
```

Python 是 case-sensitive：

```python
score = 80
Score = 90
```

这是两个不同变量。

## Basic Data Types

| Type | Example |
|---|---|
| `int` | `10` |
| `float` | `10.5` |
| `str` | `"Hello"` |
| `bool` | `True`, `False` |

检查类型：

```python
x = 10
print(type(x))
```

## Type Casting

```python
age = int(input("Enter age: "))
price = float(input("Enter price: "))
message = str(100)
```

常见错误：

```python
num = input("Enter number: ")
print(num + 10)  # TypeError
```

正确：

```python
num = int(input("Enter number: "))
print(num + 10)
```

## Arithmetic Operators

| Operator | Meaning | Example |
|---|---|---|
| `+` | add | `a + b` |
| `-` | subtract | `a - b` |
| `*` | multiply | `a * b` |
| `/` | division | `a / b` |
| `//` | floor division | `7 // 2` is `3` |
| `%` | remainder | `7 % 2` is `1` |
| `**` | power | `2 ** 3` is `8` |

## Operator Precedence

先算括号，再算乘除，最后加减。

```python
average = (score1 + score2 + score3) / 3
```

不要写：

```python
average = score1 + score2 + score3 / 3
```

## 常见 TypeError 判断

```python
k = 2
l = "2"
print(k + l)  # TypeError
```

原因：`int + str` 不可以直接加。

正确：

```python
print(k + int(l))
print(str(k) + l)
```

## 易错点

- 左边必须是变量，不能是数字：`4 = y` 是错的，应该 `y = 4`。
- `And` 是错的，Python 逻辑运算符是小写 `and`。
- `print(a; b; c)` 是错的，输出多个值用 comma：`print(a, b, c)`。
- `input()` 结果是 string，数学运算前先 cast。

## 自测

### Q1

What is the output?

```python
x = 5
y = x + 3
x = y * 2
print(x, y)
```

Answer:

```text
16 8
```

### Q2

Fix the error:

```python
x = 23
4 = y
```

Answer:

```python
x = 23
y = 4
```


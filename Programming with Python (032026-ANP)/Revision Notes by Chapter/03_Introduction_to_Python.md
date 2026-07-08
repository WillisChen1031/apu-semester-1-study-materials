# Topic 3 - Introduction to Programming With Python

## 你要会什么

这一章是 Python 入门：如何写 script、如何 input/output、如何理解 syntax error。Mock 很喜欢让你修正简单语法错误。

英文关键词：

- source code: code written by programmer
- syntax: legal structure of a language
- output: message printed to console
- console: where output appears
- interactive mode: run one line at a time
- script mode: run a `.py` file

## 最基本程序结构

```python
print("Hello World")
```

`print()` 在 Python 3 必须有括号。

错误：

```python
print "Hello"
```

正确：

```python
print("Hello")
```

## input()

`input()` 会让用户输入，并且永远先得到 string。

```python
name = input("Enter your name: ")
print("Hello", name)
```

如果要计算数字，要转换：

```python
age = int(input("Enter age: "))
print("In 10 years:", age + 10)
```

## print() 常见写法

```python
name = "Ali"
score = 80

print(name)
print("Score:", score)
print("Hello", name)
print("Hello " + name)
```

逗号 `,` 会自动加空格，而且可以输出不同类型。

```python
print("Score:", 80)
```

`+` 用在 string 拼接时，两边必须都是 string。

```python
print("Score: " + str(80))
```

## Comments

```python
# This program calculates average score
score1 = 80
score2 = 90
average = (score1 + score2) / 2
print(average)
```

考试写 code 时，comment 不是每题都必须，但 lab 里强调 readable code。

## Syntax Error Checklist

看到改错题，按这个顺序检查：

1. `print` 有没有括号。
2. `if`, `elif`, `else`, `while`, `for`, `def` 后面有没有 colon `:`
3. 字符串引号是否配对：`"James"` 或 `'James'`
4. 括号是否配对：`(` 和 `)`
5. indentation 是否正确。
6. 变量有没有先定义再使用。

## Mock 风格改错

错误：

```python
bmi = 21.8
print bmi
```

正确：

```python
bmi = 21.8
print(bmi)
```

错误：

```python
print("x="x)
```

正确：

```python
x = 10
print("x=", x)
```

错误：

```python
name = 'James"
```

正确：

```python
name = "James"
```


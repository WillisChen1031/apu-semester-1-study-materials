# Topic 7 - Functions

## 你要会什么

Function 是 mock 重点：`def` 关键字、parameter/argument、`return`、没有 `return` 的结果、scope、修正 syntax error。

英文关键词：

- function: reusable block of code
- define: create a function using `def`
- call / invoke: run a function
- parameter: variable in function definition
- argument: actual value passed in
- return: send value back to caller
- scope: where a variable can be used

## Function 基本格式

```python
def greet():
    print("Good morning")

greet()
```

有 parameter：

```python
def greet(name):
    print("Hello", name)

greet("Ali")
```

有 return：

```python
def add(a, b):
    return a + b

result = add(5, 3)
print(result)
```

## return 很重要

`return` 会把值带回函数外面。

```python
def calc(x, y):
    return x * y

result = calc(2, 3)
print(result)
```

Output:

```text
6
```

如果没有 `return`：

```python
def bar(num):
    num += 2

def foo(num):
    num += 1
    bar(num)
    return num

num = 0
num = foo(num)
print(num)
```

Output:

```text
1
```

原因：`bar(num)` 里面的 `num += 2` 没有 return，也没有赋值回 `foo` 的 `num`。

## Function with if

```python
def check_even(num):
    if num % 2 == 0:
        return True
    else:
        return False

print(check_even(3))
```

Output:

```text
False
```

## Function with loop

```python
def print_name(name):
    for i in range(5):
        print(name)

print_name("Ali")
```

## Multiple Return Values

Python 多个 return value 实际上是 tuple。

```python
def calculate(a, b):
    add = a + b
    subtract = a - b
    multiply = a * b
    return add, subtract, multiply

x, y, z = calculate(10, 5)
print(x, y, z)
```

## Default Parameter

```python
def greet(name="Student"):
    print("Hello", name)

greet("Ali")
greet()
```

## Syntax Error 修正

错误：

```python
def calculate_average(score1, score2, score3
    average = (score1 + score2 + score3 / 3
    p "The average score is: ", average
return average
```

正确：

```python
def calculate_average(score1, score2, score3):
    average = (score1 + score2 + score3) / 3
    print("The average score is:", average)
    return average
```

检查点：

- `def` 这一行最后要有 `:`
- 参数括号要关上。
- 平均数括号要正确。
- 输出用 `print()`。
- `return` 要缩进在 function 内。

## 易错点

- 定义函数用 `def`，不是 `func` 或 `function`。
- `return` 后面的代码通常不会执行。
- Function 内部变量通常是 local variable。
- `print()` 只是显示，不等于 `return`。
- 调用函数时要写括号：`greet()`。


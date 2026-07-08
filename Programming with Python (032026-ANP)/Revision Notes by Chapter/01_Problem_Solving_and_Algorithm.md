# Topic 1 - Problem Solving and Algorithm

## 你要会什么

这一章主要训练你把问题拆成 Input、Process、Output，再写成 algorithm / pseudocode / flowchart。考试如果考这章，通常不会问长概念，而是让你看题目后写步骤，或者把步骤翻译成 Python。

英文关键词：

- problem solving: solve a problem step by step
- algorithm: clear, ordered, unambiguous steps
- input: data entered by user
- process: calculation or logic
- output: result displayed to user
- sequence: statements run from top to bottom

## IPO 思维

看到题目先写 IPO，后面写 code 会快很多。

| 题目 | Input | Process | Output |
|---|---|---|---|
| rectangle area | length, width | `area = length * width` | area |
| average of 3 scores | score1, score2, score3 | `(score1 + score2 + score3) / 3` | average |
| circle area | radius | `area = 3.142 * radius * radius` | area |

## Pseudocode 模板

```text
START
    DISPLAY "Enter length:"
    GET length
    DISPLAY "Enter width:"
    GET width
    area = length * width
    DISPLAY area
END
```

对应 Python：

```python
length = float(input("Enter length: "))
width = float(input("Enter width: "))
area = length * width
print("Area:", area)
```

## Sequence Structure

Sequence 就是顺序执行。不要跳步，不要把 output 写在 calculation 前面。

```python
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
product = num1 * num2
print("Product:", product)
```

## 常见计算模板

### Rectangle

```python
length = float(input("Enter length: "))
width = float(input("Enter width: "))
area = length * width
print("Area:", area)
```

### Average

```python
score1 = int(input("Enter score 1: "))
score2 = int(input("Enter score 2: "))
score3 = int(input("Enter score 3: "))
average = (score1 + score2 + score3) / 3
print("Average:", average)
```

### Fahrenheit / Celsius

课件 lab 给的公式是：

```text
Fahrenheit = Celsius * 9 / 5 + 32
```

Python：

```python
celsius = float(input("Enter Celsius: "))
fahrenheit = celsius * 9 / 5 + 32
print("Fahrenheit:", fahrenheit)
```

## 易错点

- Algorithm 要有 input 和 output，不只是 formula。
- Pseudocode 不是 Python，不一定要写 `int(input())`，但逻辑顺序要对。
- Python code 里 `input()` 默认读到的是 string，做数学前要 `int()` 或 `float()`。
- 平均数要加括号：`(a + b + c) / 3`，不要写成 `a + b + c / 3`。

## Mock 风格自测

### Q1

Write Python code to ask for a TP number and print its length.

```python
tp = input("Enter TP number: ")
print(len(tp))
```

### Q2

Write Python code to calculate area of a rectangle.

```python
length = float(input("Enter length: "))
width = float(input("Enter width: "))
area = length * width
print("Area:", area)
```


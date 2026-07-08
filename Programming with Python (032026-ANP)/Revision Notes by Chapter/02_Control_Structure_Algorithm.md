# Topic 2 - Problem Solving and Algorithm: Control Structure

## 你要会什么

这一章是 algorithm 里的 selection 和 repetition。也就是：什么时候用 `if`，什么时候用 loop。后面 Topic 5 和 Topic 6 会用 Python 实现。

英文关键词：

- selection: choose one path based on condition
- repetition / iteration: repeat statements
- relational operator: compare values
- logical operator: combine conditions
- trace table: track variable changes step by step

## Relational Operators

| Operator | Meaning |
|---|---|
| `>` | greater than |
| `>=` | greater than or equal |
| `<` | less than |
| `<=` | less than or equal |
| `==` | equal |
| `!=` | not equal |

注意：判断相等用 `==`，赋值用 `=`。

```python
age = 18
print(age == 18)  # True
```

## Logical Operators

| Operator | Meaning | Example |
|---|---|---|
| `and` | both true | `age > 18 and score >= 50` |
| `or` | at least one true | `code == "H" or code == "F"` |
| `not` | reverse | `not passed` |

Python 用 `and/or/not`，不要写 C/Java 的 `&&`, `||`, `!`。

## Selection Pseudocode

```text
IF mark >= 50 THEN
    DISPLAY "Pass"
ELSE
    DISPLAY "Fail"
ENDIF
```

Python：

```python
mark = int(input("Enter mark: "))

if mark >= 50:
    print("Pass")
else:
    print("Fail")
```

## Repetition Pseudocode

Countdown：

```text
GET number
WHILE number >= 0
    DISPLAY number
    number = number - 1
ENDWHILE
```

Python：

```python
number = int(input("Enter number: "))

while number >= 0:
    print(number)
    number = number - 1
```

## Lab 常考算法

### Leap Year

```python
year = int(input("Enter year: "))

if year % 4 == 0:
    print("Leap year")
else:
    print("Not leap year")
```

更完整写法：

```python
year = int(input("Enter year: "))

if (year % 400 == 0) or (year % 4 == 0 and year % 100 != 0):
    print("Leap year")
else:
    print("Not leap year")
```

### Pricing Code Discount

```python
price = float(input("Enter price: "))
code = input("Enter pricing code: ").upper()

if code == "H":
    rate = 0.50
elif code == "F":
    rate = 0.40
elif code == "T":
    rate = 0.33
elif code == "Q":
    rate = 0.25
else:
    rate = 0

discount = price * rate
new_price = price - discount

print("Original price:", price)
print("Discount:", discount)
print("New price:", new_price)
```

## Trace Table 怎么做

给你代码：

```python
x = 1
while x <= 3:
    print(x)
    x = x + 1
```

Trace：

| Step | x | condition | output |
|---|---:|---|---|
| start | 1 | `1 <= 3` True | 1 |
| update | 2 | `2 <= 3` True | 2 |
| update | 3 | `3 <= 3` True | 3 |
| update | 4 | `4 <= 3` False | stop |

## 易错点

- Python 里 selection 的 block 靠 indentation，不靠 `ENDIF`。
- Flowchart / pseudocode 可以写得像自然语言，但 Python 必须有 colon `:`。
- 循环一定要有 update，不然 infinite loop。
- `range(1, 5)` 是 1, 2, 3, 4，不包含 5。


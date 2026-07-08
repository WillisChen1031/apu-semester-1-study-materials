# Topic 5 - Conditional Statements

## 你要会什么

这一章是直接写程序的重点。Mock 会让你 trace `if/elif` 输出，也会让你写 grade、even/odd、positive/negative、menu、biggest number。

英文关键词：

- conditional statement: execute code based on condition
- one-way decision: `if`
- two-way decision: `if...else`
- multi-way decision: `if...elif...else`
- nested if: if inside if
- indentation: spaces that define a block

## if 基本格式

```python
if condition:
    statement
```

Example:

```python
mark = int(input("Enter mark: "))

if mark >= 50:
    print("Pass")
```

## if else

```python
num = int(input("Enter number: "))

if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

`num % 2 == 0` 是 mock 常考：validate even number。

## if elif else

Grade 程序建议从高分往低分写：

```python
average = float(input("Enter average: "))

if average >= 80:
    grade = "A+"
elif average >= 75:
    grade = "A"
elif average >= 70:
    grade = "B+"
elif average >= 65:
    grade = "B"
elif average >= 60:
    grade = "C+"
elif average >= 55:
    grade = "C"
elif average >= 50:
    grade = "C-"
elif average >= 40:
    grade = "D"
else:
    grade = "F"

print("Grade:", grade)
```

为什么不用 `average >= 75 and average <= 79`？可以写，但更慢更容易错。因为前面的 `if average >= 80` 已经排除了 80 以上。

## Mock Trace Example

```python
mark = 80

if mark >= 80 and mark <= 100:
    print("Grade A")
elif mark >= 60 and mark < 80:
    print("Grade B")
elif mark >= 50 and mark < 60:
    print("Grade C")
```

Output:

```text
Grade A
```

## Biggest of Three Numbers

```python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
c = int(input("Enter third number: "))

if a >= b and a >= c:
    biggest = a
elif b >= a and b >= c:
    biggest = b
else:
    biggest = c

print("Biggest:", biggest)
```

## Weekly Pay with Overtime

Lab 题型：first 40 hours regular pay，超过部分 overtime 1.5。

```python
name = input("Enter name: ")
hours = float(input("Enter total hours worked: "))
rate = float(input("Enter hourly rate RM: "))

if hours <= 40:
    pay = hours * rate
else:
    regular_pay = 40 * rate
    overtime_hours = hours - 40
    overtime_pay = overtime_hours * rate * 1.5
    pay = regular_pay + overtime_pay

print(name, "received RM", format(pay, ".2f"))
```

## Menu Program

```python
print("1. Calculate area of rectangle")
print("2. Check vowel or consonant")
print("3. Find smallest of two numbers")
print("4. Exit")

choice = int(input("Enter choice: "))

if choice == 1:
    length = float(input("Enter length: "))
    width = float(input("Enter width: "))
    print("Area:", length * width)
elif choice == 2:
    ch = input("Enter character: ").lower()
    if ch in "aeiou":
        print("Vowel")
    else:
        print("Consonant")
elif choice == 3:
    a = int(input("Enter first number: "))
    b = int(input("Enter second number: "))
    if a < b:
        print("Smallest:", a)
    else:
        print("Smallest:", b)
else:
    print("Exit")
```

## 易错点

- `else` 后面不要写 condition。
- `elif` 可以有多个，`else` 最多一个。
- 每个 `if/elif/else` 后面都有 `:`
- block 必须缩进。
- `=` 是赋值，`==` 是比较。
- Python 里 logical operators 是 `and/or/not`，不是 `&&/||/!`。


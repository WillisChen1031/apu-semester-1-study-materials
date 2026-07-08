# Topic 6 - Repetition Statements / Loops

## 你要会什么

Loop 是写代码题重点。Lab 里有 sum、average、max、countdown、nested loop、input validation、menu loop。Mock 会考 list sum loop 和 trace output。

英文关键词：

- repetition / iteration: repeat code
- while loop: repeat while condition is true
- for loop: loop through a sequence
- definite loop: known number of repetitions
- indefinite loop: unknown number of repetitions
- nested loop: loop inside another loop
- break: exit loop
- continue: skip current iteration

## while Loop

适合“不知道循环几次”的题。

```python
x = 1
while x <= 5:
    print(x)
    x = x + 1
```

while 三件套：

1. initialization: `x = 1`
2. condition: `x <= 5`
3. update: `x = x + 1`

缺 update 会 infinite loop。

## for Loop

适合“知道次数”或遍历 sequence。

```python
for i in range(1, 6):
    print(i)
```

Output:

```text
1
2
3
4
5
```

## range()

| Code | Values |
|---|---|
| `range(5)` | 0, 1, 2, 3, 4 |
| `range(1, 5)` | 1, 2, 3, 4 |
| `range(1, 6, 2)` | 1, 3, 5 |
| `range(10, 0, -1)` | 10, 9, ..., 1 |

Stop value 不包含。

## Sum Pattern

Mock 例子：

```python
numbers = [2, 4, 6, 8, 10]
total = 0

for n in numbers:
    total += n

print(total)
```

Output:

```text
30
```

## Count / Average Pattern

```python
total = 0
count = 0

for i in range(3):
    score = int(input("Enter score: "))
    total = total + score
    count = count + 1

average = total / count
print("Average:", average)
```

## Max Pattern

```python
numbers = [4, 9, 2, 10]
largest = numbers[0]

for num in numbers:
    if num > largest:
        largest = num

print("Largest:", largest)
```

## Input Validation

重复问直到合法：

```python
age = int(input("Enter age: "))

while age < 0:
    print("Invalid age")
    age = int(input("Enter age again: "))

print("Age:", age)
```

## Sentinel Loop

用特殊值结束，例如输入 `-1` 停止。

```python
total = 0
num = int(input("Enter number (-1 to stop): "))

while num != -1:
    total = total + num
    num = int(input("Enter number (-1 to stop): "))

print("Total:", total)
```

## Nested Loop

Multiplication table：

```python
for i in range(1, 6):
    for j in range(1, 6):
        print(i * j, end="\t")
    print()
```

## break and continue

```python
for i in range(1, 6):
    if i == 3:
        break
    print(i)
```

Output:

```text
1
2
```

```python
for i in range(1, 6):
    if i == 3:
        continue
    print(i)
```

Output:

```text
1
2
4
5
```

## 易错点

- `while x < 5:` 如果一开始 `x = 5`，循环 0 次。
- `range(1, 4)` 只到 3。
- `total += n` 等于 `total = total + n`。
- `break` 只跳出当前 loop。
- `continue` 不结束 loop，只跳过本轮剩余代码。


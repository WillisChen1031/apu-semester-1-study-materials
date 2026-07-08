# Topic 8 - Strings

## 你要会什么

String 是 mock 和 tutorial 高频：index、negative index、slicing、methods、immutability、`len()`、loop through string、quote error。

英文关键词：

- string: sequence of characters
- index: position of a character
- slicing: extract part of a string
- immutable: cannot be changed directly
- method: function belonging to an object

## Creating Strings

```python
name = "James"
city = 'Kuala Lumpur'
```

引号必须配对。

错误：

```python
name = 'James"
```

正确：

```python
name = "James"
```

## Indexing

```python
word = "Python"
print(word[0])   # P
print(word[1])   # y
print(word[-1])  # n
```

Index 从 0 开始。

| P | y | t | h | o | n |
|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 |
| -6 | -5 | -4 | -3 | -2 | -1 |

## Slicing

格式：

```python
string[start:end]
```

规则：包含 start，不包含 end。

```python
text = "Hello, World!"
print(text[7:12])  # World
```

常见写法：

```python
word = "Programming"
print(word[0:4])   # Prog
print(word[:3])    # Pro
print(word[3:])    # gramming
print(word[-3:])   # ing
print(word[::-1])  # gnimmargorP
print(word[::2])   # Pormig
```

## String Concatenation

```python
first = "Hello"
second = "World"
print(first + " " + second)
```

不能直接 string + int：

```python
age = 20
print("Age: " + str(age))
```

或者用 comma：

```python
print("Age:", age)
```

## Useful Methods

| Method | Meaning |
|---|---|
| `upper()` | convert to uppercase |
| `lower()` | convert to lowercase |
| `capitalize()` | first character uppercase, rest lowercase |
| `strip()` | remove spaces at both ends |
| `find()` | find index, return `-1` if not found |
| `replace(old, new)` | replace substring |
| `split(separator)` | string to list |
| `count(x)` | count occurrences |
| `startswith(x)` | check prefix |
| `endswith(x)` | check suffix |

Mock:

```python
print("abc.DEF".capitalize())
```

Output:

```text
Abc.def
```

## String is Immutable

错误：

```python
word = "Python"
word[0] = "J"
```

正确：

```python
word = "Python"
word = "J" + word[1:]
print(word)
```

## Loop Through String

```python
text = "Python"

for ch in text:
    print(ch)
```

用 index：

```python
text = "Python"
i = 0

while i < len(text):
    print(text[i])
    i = i + 1
```

## Lab 题型模板

### Remove Odd-Index Characters

```python
text = "Programming with Python"
new_text = ""

for i in range(len(text)):
    if i % 2 == 0:
        new_text = new_text + text[i]

print(new_text)
```

### Split by `#`

```python
text = "Magic#Mirror#on#the#wall"
parts = text.split("#")

for part in parts:
    print(part, end=" ")
```

### First, Middle, Last

```python
word = input("Enter word: ")
middle_index = (len(word) - 1) // 2
new_word = word[0] + word[middle_index] + word[-1]
print(new_word)
```

## 易错点

- `len()` 是 built-in function，不是 string method：`len(word)`。
- `find()` 找不到返回 `-1`。
- Slice 不包含 end。
- String methods 通常返回新 string；原 string 不会自动改变。


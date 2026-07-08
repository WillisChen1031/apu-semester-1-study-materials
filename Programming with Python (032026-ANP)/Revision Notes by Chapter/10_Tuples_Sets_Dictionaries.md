# Topic 10 - Tuples, Sets and Dictionaries

## 你要会什么

Mock 对这一章目前偏识别题：tuple 是 `()`，list 是 `[]`，set 是 `{}`，string 有 quotes。课件还包括 set 去重和 dictionary key-value，写代码题可能会考 frequency count。

英文关键词：

- tuple: ordered immutable collection
- set: unordered collection with no duplicate
- dictionary: key-value pairs
- key: used to access value
- value: data stored under a key
- immutable: cannot be changed

## Tuple

Tuple 像 list，但 immutable。

```python
fruits = ("Cherry", "Guava", "Mango")
print(fruits[0])
print(fruits[-1])
print(fruits[1:3])
```

Mock:

```python
(1, 2, 3, 4)
```

这是 tuple。

不能改：

```python
t = (5, 4, 3)
t[2] = 0  # TypeError
```

Tuple 常见 methods：

```python
t = (1, 2, 2, 3)
print(t.count(2))
print(t.index(3))
```

## Tuple vs List

| Feature | List | Tuple |
|---|---|---|
| syntax | `[1, 2, 3]` | `(1, 2, 3)` |
| ordered | yes | yes |
| mutable | yes | no |
| methods | many | fewer |

## Set

Set 不重复、无顺序。

```python
nums = {1, 2, 2, 3}
print(nums)
```

可能输出：

```text
{1, 2, 3}
```

Empty set 要写：

```python
empty_set = set()
```

不要写：

```python
empty = {}  # this is dictionary
```

Set operations：

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)  # union
print(a & b)  # intersection
print(a - b)  # difference
print(a ^ b)  # symmetric difference
```

## Dictionary

Dictionary 存 key-value。

```python
student = {
    "name": "Ali",
    "age": 20,
    "score": 85
}

print(student["name"])
print(student.get("score"))
```

Add / update：

```python
student["grade"] = "A"
student["score"] = 90
```

Delete：

```python
student.pop("age")
```

Loop：

```python
for key in student:
    print(key, student[key])
```

Better：

```python
for key, value in student.items():
    print(key, value)
```

## Frequency Count Template

常见写代码题：count characters / words。

```python
text = "banana"
freq = {}

for ch in text:
    if ch in freq:
        freq[ch] += 1
    else:
        freq[ch] = 1

print(freq)
```

Output:

```text
{'b': 1, 'a': 3, 'n': 2}
```

## 易错点

- `{}` 是 empty dictionary，不是 empty set。
- Set 不支持 indexing：`s[0]` 错。
- Dictionary 用 key 访问，不是 index。
- `d[key]` 如果 key 不存在会 `KeyError`；`d.get(key)` 更安全。
- Tuple 不能 `append`, `sort`, `reverse`。


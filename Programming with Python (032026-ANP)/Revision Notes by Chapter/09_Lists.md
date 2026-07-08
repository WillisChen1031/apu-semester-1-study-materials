# Topic 9 - Lists

## 你要会什么

List 是 mock 高频：创建、index、negative index、slicing、`append/insert/remove/sort`、loop、sum/average、mutable。

英文关键词：

- list: ordered mutable collection
- element / item: value inside a list
- index: position of item
- mutable: can be changed
- append: add item at the end
- insert: add item at a specific index

## Creating Lists

```python
numbers = [10, 20, 30]
foods = ["cookies", "cake", "ice cream"]
empty = []
mixed = [10, "Python", 3.5, True]
```

List 用 square brackets `[]`。

## Indexing

```python
numbers = [10, 20, 30]
print(numbers[0])   # 10
print(numbers[-1])  # 30
```

## Slicing

```python
my_list = ["a", "b", "c", "d", "e"]
print(my_list[1:4])
```

Output:

```text
['b', 'c', 'd']
```

Mock 解释：index 1 到 3，不包含 index 4。

```python
numbers = [10, 20, 30, 40, 50]
print(numbers[:3])  # [10, 20, 30]
```

## List is Mutable

```python
items = [10, 20, 30]
items[1] = 99
print(items)
```

Output:

```text
[10, 99, 30]
```

## Important Methods

| Method | Meaning | Example |
|---|---|---|
| `append(x)` | add to end | `nums.append(4)` |
| `insert(i, x)` | insert at index | `nums.insert(0, 4)` |
| `remove(x)` | remove first matching value | `nums.remove(5)` |
| `pop()` | remove and return last item | `nums.pop()` |
| `sort()` | sort ascending | `nums.sort()` |
| `reverse()` | reverse order | `nums.reverse()` |
| `count(x)` | count occurrences | `nums.count(5)` |
| `index(x)` | find first index | `nums.index(5)` |

Mock:

```python
myFood = []
myFood.insert(0, "Pizza")
```

空 list 不能这样：

```python
myFood[0] = "Pizza"  # IndexError
```

## Built-in Functions

```python
nums = [65, 75, 85, 95]

print(len(nums))
print(sum(nums))
print(min(nums))
print(max(nums))
```

## Loop Through List

By value：

```python
numbers = [2, 4, 6, 8, 10]
total = 0

for n in numbers:
    total += n

print(total)
```

By index：

```python
numbers = [2, 4, 6]

for i in range(len(numbers)):
    print(numbers[i])
```

## Lab 题型模板

### Check Number Exists

```python
validNumbers = [65, 75, 85, 95, 105]
num = int(input("Enter number: "))

if num in validNumbers:
    print("Available")
else:
    print("Not available")
```

### Filter Valid Numbers 0-100

```python
numbers = [65, 75, 85, 95, 105]
validNumbers = []

for num in numbers:
    if num >= 0 and num <= 100:
        validNumbers.append(num)

print(validNumbers)
```

### Sum / Average / Product

```python
numbers = [65, 75, 85, 95]

total = 0
product = 1

for num in numbers:
    total += num
    product *= num

average = total / len(numbers)

print("Sum:", total)
print("Average:", average)
print("Product:", product)
```

### Remove Duplicate Once

```python
nums = [1, 3, 5, 5, 2]
nums.sort()
nums.append(4)
nums.remove(5)
nums.insert(0, 6)
print(len(nums))
print(nums)
```

## List vs String

| Feature | String | List |
|---|---|---|
| ordered | yes | yes |
| indexed | yes | yes |
| mutable | no | yes |
| syntax | `"abc"` | `[1, 2, 3]` |

## 易错点

- `append(x)` 是把 x 当成一个 item 加进去。
- `insert(index, value)` 可以对空 list 用。
- `remove(x)` 删除第一个 matching item。
- `sort()` 会直接修改原 list。
- `myList[1:4]` 取 index 1, 2, 3。


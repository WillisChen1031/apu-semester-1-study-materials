# Python Mock Test Questions with Answers and Explanations

> 整理自本次对话中的 mock test 题目。代码题的答案可能存在多种写法，下面给出考试中最稳妥、最容易拿分的参考答案。

---

## Q1. Write a Python code that asks the student to enter their TP number and then prints the length of the TP number. [2 marks]

### Answer

```python
tp = input("Type your TP number: ")
print(len(tp))
```

### Explanation

`input()` 读取 TP number，结果是字符串。`len(tp)` 返回字符串长度，`print()` 输出结果。注意是 `len()`，不是 `leng()`。

---

## Q2. Write assignment statements that perform the following operations with the variables `num1`, `num2`, and `num3`:  
a. Adds 2 to `num1` and assigns the result to `num2`  
b. Multiplies `num2` by 4 and assigns the result to `num1`  
c. Divides `num1` by 2.9 and assigns the result to `num2`  
d. Subtracts 8 from `num2` and assigns the result to `num1`  
[8 marks]

### Answer

```python
num2 = num1 + 2
num1 = num2 * 4
num2 = num1 / 2.9
num1 = num2 - 8
```

### Explanation

赋值语句格式是 `变量 = 表达式`。变量名中不能有空格，例如 `num2` 不能写成 `num 2`。

---

## Q3. Observe the following Python code thoroughly and rewrite the Python code after removing all syntactical errors.

Original code:

```python
def calculate_average(score1, score2, score3
    average = (score1 + score2 + score3 / 3
    p "The average score is: ", average
return average
```

[4 marks]

### Answer

```python
def calculate_average(score1, score2, score3):
    average = (score1 + score2 + score3) / 3
    print("The average score is:", average)
    return average
```

### Explanation

函数定义末尾要有 `:`；平均数要先把三个分数加起来再除以 3；输出要用 `print()`；`return average` 必须缩进在函数内部。

---

## Q4. Identify error(s) in the following code and write the correct code.

a.
```python
bmi = 21.8
print bmi
```

b.
```python
num1 = 12
num2 = num1 + num2
print(num1 And num2)
```

c.
```python
print("x="x)
```

d.
```python
x = 23
4 = y
```

e.
```python
a,b,c = 2,8,4
print(a,b,c)
d,e,f = a,b,c
print(d;e;f)
```

[6 marks]

### Answer

```python
# a
bmi = 21.8
print(bmi)

# b
num1 = 12
num2 = 0
num2 = num1 + num2
print(num1, "and", num2)

# c
print("x=", x)

# d
x = 23
y = 4

# e
a, b, c = 2, 8, 4
print(a, b, c)
d, e, f = a, b, c
print(d, e, f)
```

### Explanation

Python 3 中 `print` 必须使用括号。变量必须先定义再使用。字符串和变量之间可以用逗号分隔。赋值语句左边必须是变量，不能是数字。`print()` 中多个值用逗号分隔，不能用分号。

---

## Q5. Write a Python program to calculate average of 3 exam scores and print the student's average grade according to the table below. The program should read student's name, TP number, gender, score1, score2 and score3.

Grade range:

| Score | Grade |
|---|---|
| 80-100 | A+ |
| 75-79 | A |
| 70-74 | B+ |
| 65-69 | B |
| 60-64 | C+ |
| 55-59 | C |
| 50-54 | C- |
| 40-49 | D |
| 0-39 | F |

[10 marks]

### Answer

```python
name = input("Enter student's name: ")
tp = input("Enter TP number: ")
gender = input("Enter gender (M/F): ")

score1 = int(input("Enter score for Exam 1: "))
score2 = int(input("Enter score for Exam 2: "))
score3 = int(input("Enter score for Exam 3: "))

average = (score1 + score2 + score3) / 3

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

print("Student Details")
print("Name:", name)
print("TP Number:", tp)
print("Gender:", gender)
print("Average Score:", average)
print("Grade:", grade)
```

### Explanation

`input()` 得到字符串，考试分数要用 `int(input())` 转成整数。`if-elif-else` 按顺序判断，因此从高分到低分写即可，不需要写 `74 >= average >= 70`。

---

## Q6. Consider the code below. Select the correct output.

```python
def bar(num):
    num += 2

def foo(num):
    num += 1
    bar(num)
    return num

if __name__ == "__main__":
    num = 0
    num = foo(num)
    print(num)
```

Options: a. 3, b. 2, c. 0, d. 1

### Answer

**d. 1**

### Explanation

`foo(0)` 中 `num += 1` 后，`num` 变成 1。`bar(num)` 虽然在 `bar()` 内部把局部变量加 2，但没有 `return`，也没有把结果赋回给 `foo()` 的 `num`。所以 `foo()` 返回 1。

---

## Q7. Choose the correct Python code that produces the output below.

Output:

```text
Abc.def
```

Options:

a. `print("abc.DEF".upper())`  
b. `print("abc. DEF".title())`  
c. `print("abc. DEF".lower())`  
d. `print("abc.DEF".capitalize())`

### Answer

**d. `print("abc.DEF".capitalize())`**

### Explanation

`capitalize()` 会让整个字符串的第一个字符大写，其余字符变小写，所以 `abc.DEF` 变成 `Abc.def`。

---

## Q8. To open a file `data.txt` for reading, we use __________.

Options:

a. `file = open("c:\\data.txt", "r")`  
b. `file = open(file = "data.txt", "r+")`  
c. `file = open("data.txt", "r")`  
d. `file = open(file = "c:\\data.txt", "r")`

### Answer

**c. `file = open("data.txt", "r")`**

### Explanation

`open("data.txt", "r")` 表示以读取模式打开当前目录下的 `data.txt`。`r` means read。

---

## Q9. Trace the correct output for the given code below.

```python
mark = 80

if (mark >= 80 and mark <= 100):
    print("Grade A")
elif (mark >= 60 and mark < 80):
    print("Grade B")
elif (mark >= 50 and mark < 60):
    print("Grade C")
```

Options: a. Grade A, b. Grade C, c. Runtime Error, d. Grade B

### Answer

**a. Grade A**

### Explanation

`mark = 80` 满足 `mark >= 80 and mark <= 100`，所以输出 `Grade A`。没有 `else` 不会报错，`else` 是可选的。

---

## Q10. Which of the following is considered as a tuple?

Options:

a. `(1,2,3,4)`  
b. `[1,2,3,4]`  
c. `{1,2,3,4}`  
d. `"1,2,3,4"`

### Answer

**a. `(1,2,3,4)`**

### Explanation

圆括号 `()` 通常表示 tuple；方括号 `[]` 是 list；花括号 `{}` 是 set；引号中的是 string。

---

## Q11. What does the slice `myList[1:4]` do?

Options:

a. Extracts items 2, 3, and 4 from myList.  
b. Extracts items 2 and 3 from myList.  
c. Extracts items 1, 2, and 3 from myList.  
d. Extracts items 1 to 4 from myList.

### Answer

**a. Extracts items 2, 3, and 4 from myList.**

### Explanation

Python 切片是左闭右开：`myList[1:4]` 取索引 1、2、3，不取索引 4。按“第几个元素”来说，就是第 2、3、4 个元素。

---

## Q12. From the code above, what is the output?

```python
my_list = ['a', 'b', 'c', 'd', 'e']
print(my_list[-4:-1])
```

Options:

a. `['c', 'd', 'e']`  
b. `['b', 'c']`  
c. `['b', 'c', 'd']`  
d. `['c', 'd']`

### Answer

**c. `['b', 'c', 'd']`**

### Explanation

负索引中，`-4` 是 `'b'`，`-1` 是 `'e'`。切片不包含结束位置，所以取 `'b'`, `'c'`, `'d'`。

---

## Q13. What is the output of the following Python code snippet?

```python
my_list = [10, 20, 30, 40, 50]
print(my_list[:3])
```

Options:

a. `[10, 20, 30]`  
b. `[30, 40, 50]`  
c. `[10, 20, 30, 40]`  
d. `[10, 20]`

### Answer

**a. `[10, 20, 30]`**

### Explanation

`my_list[:3]` 等价于 `my_list[0:3]`，取索引 0、1、2，不取索引 3。

---

## Q14. What keyword is used to define a function in Python?

Options:

a. `func`  
b. `declare`  
c. `def`  
d. `function`

### Answer

**c. `def`**

### Explanation

Python 使用 `def` 定义函数，例如 `def hello():`。

---

## Q15. From the code below, what is the expected output from the result variable?

```python
def calc(x, y):
    return x * y

result = calc(2, 3)
print(result)
```

Options: a. 6, b. 5, c. Null, d. 23

### Answer

**a. 6**

### Explanation

`calc(2, 3)` 返回 `2 * 3`，所以结果是 6。

---

## Q16. What is the output of the following code snippet?

```python
def check_num(number):
    if number % 2 == 0:
        return True
    else:
        return False

print(check_num(3))
```

Options: a. False, b. True, c. Null, d. Type Error Happen

### Answer

**a. False**

### Explanation

`3 % 2 = 1`，不是 0，所以 `3` 不是偶数，函数返回 `False`。

---

## Q17. Based on this code, using `end=' '` in a print statement will result in outputs being separated by spaces instead of new lines.

```python
print("Hello", end=' ')
print("World")
```

Options: a. False, b. True

### Answer

**b. True**

### Explanation

`end=' '` 会把默认的换行符替换为空格，因此输出是 `Hello World`，两个输出在同一行，中间有空格。

---

## Q18. What is the output of the following Python code snippet?

```python
my_string = "Hello, World!"
print(my_string[7:12])
```

Options:

a. `, Worl`  
b. `ello,`  
c. `World!`  
d. `World`

### Answer

**d. `World`**

### Explanation

`W` 的索引是 7，`!` 的索引是 12。`[7:12]` 取索引 7 到 11，不包含 12，所以输出 `World`。

---

## Q19. The if condition below is to validate ___ number.

```python
if (num1 % 2 == 0):
```

Options: a. odd, b. even, c. prime, d. percentage of 2

### Answer

**b. even**

### Explanation

`num1 % 2 == 0` 表示除以 2 余数为 0，因此是偶数 even。

---

## Q20. Trace the correct output based on the snippet code below.

```python
numbers = [2, 4, 6, 8, 10]
total = 0
for n in numbers:
    total += n
print(total)
```

Options: a. 30, b. 31, c. 33, d. 32

### Answer

**a. 30**

### Explanation

循环把列表中的数字全部加起来：`2 + 4 + 6 + 8 + 10 = 30`。

---

## Q21. Given the code below, choose which Python expression will produce `TypeError`.

```python
k = 2
l = '2'
m = 'foo'
n = 'bar'
o = 6.0
p = True
```

Options:

a. `print(m + " " + n)`  
b. `print(k + l)`  
c. `print(o + k)`  
d. `print(k + p)`

### Answer

**b. `print(k + l)`**

### Explanation

`k` 是整数 2，`l` 是字符串 `'2'`。Python 不能直接计算 `2 + '2'`，会产生 `TypeError`。但是 `6.0 + 2` 可以，`2 + True` 也可以，因为 `True` 可当作 1。

---

## Q22. Built-in function that will return the length of a list or string.

Options:

a. `len()`  
b. `sizeof()`  
c. `str()`  
d. `getLength()`

### Answer

**a. `len()`**

### Explanation

`len()` 用来返回字符串或列表等对象的长度。例如 `len("Hello")` 是 5，`len([1,2,3])` 是 3。

---

## Q23. `myFood = []`. Choose the correct statement to add an element `'Pizza'` to the `myFood` list at index 0.

Options:

a. `myFood[0] = 'Pizza'`  
b. `myFood.insert(0, 'Pizza')`  
c. `myFood.insert(1, 'Pizza')`  
d. `myFood[1] = 'Pizza'`

### Answer

**b. `myFood.insert(0, 'Pizza')`**

### Explanation

空列表没有索引 0，所以不能用 `myFood[0] = 'Pizza'`。要在指定位置插入新元素，应使用 `insert(index, value)`。

---

## Q24. Which of the following mode refers to append data to the file?

Options:

a. `b+`  
b. `w`  
c. `r`  
d. `a+`

### Answer

**d. `a+`**

### Explanation

`a` 表示 append。`a+` 表示追加写入并允许读取。`w` 是写入并覆盖，`r` 是读取。

---

## Q25. Choose which statement is NOT valid string in Python.

Options:

a. `name = 'James'`  
b. `name = "\"James\""`  
c. `name = "James"`  
d. `name = 'James"`

### Answer

**d. `name = 'James"`**

### Explanation

Python 字符串的引号必须匹配。`'James"` 以单引号开始，却以双引号结束，会产生语法错误。

---


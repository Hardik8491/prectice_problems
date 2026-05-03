# 📘 Practice Problems

---

## 🔹 Question 1: Separate Alphabets and Numbers

### 📝 Problem Statement
Given a string containing both alphabets and digits, separate them into:
- A string of all alphabets
- A number formed by all digits

---

### 📥 Input
```

Hyper12345Lower100

```

---

### 📤 Output
```

['HyperLower', 12345100]

````

---

### 💻 Solution
```python
s = "Hyper12345Lower100"

strings = ''
num = ''
lst = []

for i in s:
    if i.isdigit():
        num += i
    else:
        strings += i

if strings:
    lst.append(strings)

if num:
    lst.append(int(num))

print(lst)
````

---

## 🔹 Question 2: Unique Number of Occurrences

### 📝 Problem Statement

Given an array, check if the frequency of each element is unique.

---

### 📥 Input

```
arr = [1,2,2,1,1,3]
```

---

### 📤 Output

```
True
```

---

### 💻 Solution

```python
arr = [1,2,2,1,1,3]

dic = {}

for i in arr:
    if i in dic:
        dic[i] += 1
    else:
        dic[i] = 1

values = list(dic.values())

print(len(values) == len(set(values)))
```

---

## 🔹 Question 3: Maximum Product of Two Elements

### 📝 Problem Statement

Given an array of integers, find the maximum value of:

```
(nums[i] - 1) * (nums[j] - 1)
```

where `i != j`.

---

### 📥 Input

```
nums = [6,4,5,1]
```

---

### 📤 Output

```
20
```

---

### 💻 Solution

```python
nums = [6,4,5,1]

nums.sort()
l = len(nums)

result = (nums[l-1] - 1) * (nums[l-2] - 1)

print(result)
```

---

## 🔥 Summary

* Q1 → String + Number separation
* Q2 → Frequency uniqueness (HashMap concept)
* Q3 → Max pair product (Greedy / Sorting)


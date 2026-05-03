# 🔍 String Search Problem

## 📌 Problem Statement

You are given a number `n` followed by `n` strings. After that, you are given one more string (target string). Your task is to find the position (index) of the target string in the list of given strings.

---

## 📥 Input

```

4
Hello Good Morning
abcd123Fghy
India
progoti.c
India

```

---

## 📤 Output

```

Position of the searched string is:2

````

---

## 🧠 Explanation

- Total strings = 4  
- Target string = `India`  
- It is found at index **2** (0-based indexing)

---

## ✅ Solution Code (Python)

```python
n = int(input())
strings = []

# Read n strings
for _ in range(n):
    strings.append(input())

# Target string
target = input()

# Find position
position = -1
for i in range(n):
    if strings[i] == target:
        position = i
        break

# Output
if position != -1:
    print(f"Position of the searched string is:{position}")
````

---

## 🚀 Alternative (Short Approach)

```python
n = int(input())
strings = [input() for _ in range(n)]
target = input()

if target in strings:
    print(f"Position of the searched string is:{strings.index(target)}")
```

---

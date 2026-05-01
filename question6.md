# 📘 Practice Problems (Pangram + Matrix Rotation)

---

## 🔹 Question 1: Check Pangram String

### 📝 Problem Statement
Given a string `s`, check whether it is a **pangram**.  
A pangram contains **all 26 letters of the English alphabet** at least once.

---

### 📥 Input
```

A quick brown fox jumps over the lazy dog

```

---

### 📤 Output
```

YES

```

---

### 📥 Input
```

abcdefghijklg

```

---

### 📤 Output
```

NO

````

---

# 💻 Solutions

---

## ✅ Solution 1: Using Alphabet Check (Loop)

```python
def is_pangram(s):
    alphabet = "abcdefghijklmnopqrstuvwxyz"
    s = s.lower()
    
    for ch in alphabet:
        if ch not in s:
            return "NO"
    return "YES"

print(is_pangram("A quick brown fox jumps over the lazy dog"))
````

---

## ✅ Solution 2: Using Set (Best Approach)

```python
def is_pangram(s):
    letters = set()

    for ch in s.lower():
        if ch.isalpha():
            letters.add(ch)

    return "YES" if len(letters) == 26 else "NO"

print(is_pangram("A quick brown fox jumps over the lazy dog"))
```

---

## ✅ Solution 3: One-Liner

```python
s = "A quick brown fox jumps over the lazy dog"
print("YES" if len(set(filter(str.isalpha, s.lower()))) == 26 else "NO")
```

---

## 🔥 Key Concept

* Use **set** to store unique characters
* Check if count == 26

---

---

## 🔹 Question 2: 2D Matrix Rotation

### 📝 Problem Statement

Given a **3 × 3 matrix**, perform:

1. **90-degree rotation (clockwise)**
2. **180-degree rotation**

---

### 📥 Input

```
1 2 3
4 5 6
7 8 9
```

---

### 📤 Output

```
90 Degree Rotation
7 4 1
8 5 2
9 6 3

180 Degree Rotation
9 8 7
6 5 4
3 2 1
```

---

# 💻 Solutions

---

## ✅ Solution 1: Hardcoded (Your Approach)

```python
l1 = input().split()
l2 = input().split()
l3 = input().split()

print("90 Degree Rotation")
for i in range(3):
    print(l3[i], l2[i], l1[i])

print("180 Degree Rotation")
print(l3[::-1])
print(l2[::-1])
print(l1[::-1])
```

---

## ✅ Solution 2: Using Matrix (General Approach)

```python
matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
]

# 90 degree rotation
print("90 Degree Rotation")
for col in range(3):
    for row in range(2, -1, -1):
        print(matrix[row][col], end=" ")
    print()

# 180 degree rotation
print("180 Degree Rotation")
for row in range(2, -1, -1):
    for col in range(2, -1, -1):
        print(matrix[row][col], end=" ")
    print()
```

---

## ✅ Solution 3: Pythonic (Zip Trick)

```python
matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
]

# 90 degree
rot90 = list(zip(*matrix[::-1]))

# 180 degree
rot180 = [row[::-1] for row in matrix[::-1]]

print("90 Degree Rotation")
for row in rot90:
    print(*row)

print("180 Degree Rotation")
for row in rot180:
    print(*row)
```

---

# 🔥 Summary

| Problem         | Concept           |
| --------------- | ----------------- |
| Pangram         | Set / String      |
| Matrix Rotation | Arrays / Indexing |

---

# 💡 Interview Tips

* Pangram → Always use **set (O(n))**
* Matrix → Learn **transpose + reverse trick**


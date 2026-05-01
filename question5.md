
# 📘 Reverse Words in a String (All Approaches)

---

## 🔹 Problem Statement

Given a string `s` consisting of words separated by spaces:

1. Reverse the **characters of each word individually**
2. Keep the **word order unchanged**

---

## 📥 Input
```

Let's take LeetCode contest

```

---

## 📤 Output
```

s'teL ekat edoCteeL tsetnoc

```

---

## 🔹 Additional Task
After processing:
- Sort the words
- Print the length of the first word

### 📤 Output
```

8

````

---

# 💻 All Possible Solutions

---

## ✅ Solution 1: Using Slicing (Best & Cleanest)

```python
s = "Let's take LeetCode contest"

words = s.split()
result = [word[::-1] for word in words]

print(' '.join(result))
````

---

## ✅ Solution 2: Using Loop

```python
s = "Let's take LeetCode contest"

words = s.split()
res = []

for word in words:
    res.append(word[::-1])

print(' '.join(res))
```

---

## ✅ Solution 3: Using map()

```python
s = "Let's take LeetCode contest"

result = list(map(lambda x: x[::-1], s.split()))

print(' '.join(result))
```

---

## ✅ Solution 4: Without Slicing (Manual Reverse)

```python
s = "Let's take LeetCode contest"

words = s.split()
res = []

for word in words:
    temp = ""
    for ch in word:
        temp = ch + temp
    res.append(temp)

print(' '.join(res))
```

---

## ✅ Solution 5: Using Stack Concept

```python
s = "Let's take LeetCode contest"

words = s.split()
res = []

for word in words:
    stack = list(word)
    rev = ""
    
    while stack:
        rev += stack.pop()
    
    res.append(rev)

print(' '.join(res))
```

---

## ✅ Solution 6: One-Liner (Pythonic)

```python
s = "Let's take LeetCode contest"

print(' '.join(word[::-1] for word in s.split()))
```

---

## 🔹 Additional Task Solution

```python
s = "Let's take LeetCode contest"

words = s.split()
words.sort()

print(len(words[0]))
```

---

# 🔥 Summary

| Approach       | Complexity | Notes              |
| -------------- | ---------- | ------------------ |
| Slicing        | O(n)       | ✅ Best             |
| Loop           | O(n)       | Easy to understand |
| map()          | O(n)       | Functional style   |
| Manual Reverse | O(n²)      | Interview logic    |
| Stack          | O(n²)      | Concept-based      |
| One-liner      | O(n)       | Clean & short      |

---

# 💡 Key Learning

* `[::-1]` → fastest way to reverse string
* `split()` → converts string → list
* `' '.join()` → list → string


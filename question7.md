## 🔹 Question 1: Print All Palindrome Strings

### 📝 Problem Statement  
Given an integer `n` and `n` strings, print all the **palindrome strings** present in the list.  
A palindrome is a string that reads the same forward and backward.

---

### 📥 Input
```

3
malayalam
radar
nitish


```id="q1-in"
```
---


### 📤 Output
```

malayalam
radar

````id="q1-out"

---
```

# 💻 All Solutions

---

## ✅ Solution 1: Basic Loop

```python
n = int(input())
l = []

for _ in range(n):
    l.append(input())

for word in l:
    if word == word[::-1]:
        print(word)
````

---

## ✅ Solution 2: Using Function

```python id="q1-sol2"
def get_palindromes(lst):
    res = []
    for word in lst:
        if word == word[::-1]:
            res.append(word)
    return res

n = int(input())
l = [input() for _ in range(n)]

for word in get_palindromes(l):
    print(word)
```

---

## ✅ Solution 3: List Comprehension

```python id="q1-sol3"
n = int(input())
l = [input() for _ in range(n)]

res = [word for word in l if word == word[::-1]]

for word in res:
    print(word)
```

---

## ✅ Solution 4: Using filter()

```python id="q1-sol4"
n = int(input())
l = [input() for _ in range(n)]

res = list(filter(lambda x: x == x[::-1], l))

for word in res:
    print(word)
```

---

## ✅ Solution 5: Manual Reverse (No slicing)

```python id="q1-sol5"
def is_palindrome(word):
    rev = ""
    for ch in word:
        rev = ch + rev
    return word == rev

n = int(input())
l = [input() for _ in range(n)]

for word in l:
    if is_palindrome(word):
        print(word)
```

---

# 🔥 Key Concept

* `word[::-1]` → fastest palindrome check
* Use list comprehension for clean code

---

---

## 🔹 Question 2: Word Frequency & Maximum Occurrence

### 📝 Problem Statement

Given a string:

1. Count frequency of each word
2. Return the word that occurs **maximum number of times**

---

### 📥 Input

```id="q2-in"
hello hi hello world hello
```

---

### 📤 Output

```id="q2-out"
hello
```

---

# 💻 All Solutions

---

## ✅ Solution 1: Using Dictionary (Basic)

```python id="q2-sol1"
s = input()
words = s.split()

freq = {}

for word in words:
    if word in freq:
        freq[word] += 1
    else:
        freq[word] = 1

max_word = max(freq, key=freq.get)

print(max_word)
```

---

## ✅ Solution 2: Using count()

```python id="q2-sol2"
s = input()
words = s.split()

unique = set(words)
freq = {}

for word in unique:
    freq[word] = words.count(word)

print(max(freq, key=freq.get))
```

---

## ✅ Solution 3: Using collections.Counter (Best)

```python id="q2-sol3"
from collections import Counter

s = input()
words = s.split()

freq = Counter(words)

print(freq.most_common(1)[0][0])
```

---

## ✅ Solution 4: One-Liner

```python id="q2-sol4"
s = input()
print(max(set(s.split()), key=s.split().count))
```

---

## ✅ Solution 5: Manual Max Tracking

```python id="q2-sol5"
s = input()
words = s.split()

freq = {}
max_count = 0
max_word = ""

for word in words:
    freq[word] = freq.get(word, 0) + 1
    
    if freq[word] > max_count:
        max_count = freq[word]
        max_word = word

print(max_word)
```

---

# 🔥 Summary

| Problem    | Best Approach                |
| ---------- | ---------------------------- |
| Palindrome | Slicing / List Comprehension |
| Word Count | Counter / Dictionary         |

---

# 💡 Interview Tips

* Always mention **time complexity**
* Prefer **set / Counter** for optimization
* Avoid nested loops if possible

---

```


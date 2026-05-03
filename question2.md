# 🌶️ Pepper Store Management System

## 📌 Problem Statement

Design a system to manage different types of peppers in a store and perform operations based on their spiciness and price.

---

## 🧱 Class Structure

### 🔹 Class: Pepper

Attributes:
- name → Name of the pepper (string)
- color → Color of the pepper (string)
- SHI → Scoville Heat Units (integer)
- price → Price of the pepper (float)

---

### 🔹 Class: Store

Attributes:
- username → Name of the store owner
- pepper list → List of Pepper objects

---

## ⚙️ Methods

### 🔸 findSpiciestPepper()

- Find the pepper with the **highest SHI**
- Consider only peppers where **SHI ≥ 14000**
- Print:
```

<name> with <color> of SHI : <SHI>

```
- If no such pepper exists → return None

---

### 🔸 sortPepperByPrice()

- Sort peppers in **ascending order of price**
- Print:
```

  <name>
  <price>
  ```
- If list is empty → return None

---

## 📥 Input Format

1. Integer `n` → number of peppers
2. For each pepper:

   * name
   * color
   * SHI
   * price

---

## 📤 Output Format

```
Spiciest Pepper :
<result>

Sorted Pepper by price :
<result>
```

---

## 🧪 Sample Input

```
3
corona
red
15000
32
nupur
green
42350
90
greenchilli
yellow
12343
43
```

---

## ✅ Sample Output

```
Spiciest Pepper :
nupur with green of SHI : 42350

Sorted Pepper by price :
corona
32.0
greenchilli
43.0
nupur
90.0
```

---

## ✅ Solution Code

```python
class Pepper:
    def __init__(self, name, color, SHI, price):
        self.name = name
        self.color = color
        self.SHI = SHI
        self.price = price


class Store:
    def __init__(self, username, pepper_list):
        self.username = username
        self.pepper_list = pepper_list

    def findSpiciestPepper(self):
        eligible = []

        for pepper in self.pepper_list:
            if pepper.SHI >= 14000:
                eligible.append(pepper)

        if not eligible:
            return None

        max_pepper = max(eligible, key=lambda x: x.SHI)

        print(f"{max_pepper.name} with {max_pepper.color} of SHI : {max_pepper.SHI}")

    def sortPepperByPrice(self):
        if not self.pepper_list:
            return None

        sorted_list = sorted(self.pepper_list, key=lambda x: x.price)

        for pepper in sorted_list:
            print(pepper.name)
            print(pepper.price)


# MAIN
n = int(input())
pepper_list = []

for _ in range(n):
    name = input()
    color = input()
    SHI = int(input())
    price = float(input())

    pepper_list.append(Pepper(name, color, SHI, price))

store = Store("Mayank", pepper_list)

print("\nSpiciest Pepper :")
store.findSpiciestPepper()

print("\nSorted Pepper by price :")
store.sortPepperByPrice()
```

---

## 🧠 Key Concepts

* Object-Oriented Programming (OOP)
* Filtering using conditions
* Finding max using `key`
* Sorting using `lambda`
* Clean output formatting


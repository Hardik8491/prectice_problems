
# 📘 Icecream Store Management Problem

---

## 🔹 Problem Statement

You are given details of `n` ice creams. Each ice cream has the following attributes:

- `id` (integer)  
- `price` (integer)  
- `name` (string)  
- `quantityGrams` (integer)  
- `category` (string)  

Create a class `Icecream` to store these details.

Create another class `IcecreamStore` with the following methods:

---

### 🔸 Method 1: `findMinimumPrice()`
- Find the ice cream(s) with the **minimum price**
- If multiple ice creams have the same minimum price, return the **lexicographically smallest name**
- If no ice cream exists, return `"no icecream found"`

---

### 🔸 Method 2: `sortIcecreamById()`
- Return a **sorted list of ice cream IDs** in ascending order
- If no ice cream exists, return `None`

---

## 📥 Input Format
- First line: Integer `n` (number of ice creams)  
- Next `n` blocks:
  - `id`  
  - `price`  
  - `name`  
  - `quantityGrams`  
  - `category`  

---

## 📥 Sample Input
```

2
1
10
vanila
200
indian
2
20
chocobar
300
italian

```id="ice-in"

---

## 📤 Sample Output
```

vanila
[1, 2]

````id="ice-out"

---

# 💻 Solution

```python
class Icecream:
    def __init__(self, id, price, name, quantityGrams, category):
        self.id = id
        self.price = price
        self.name = name
        self.quantityGrams = quantityGrams
        self.category = category


class IcecreamStore:
    def __init__(self, icecreams):
        self.icecreams = icecreams

    def findMinimumPrice(self):
        if not self.icecreams:
            return "no icecream found"

        # find minimum price
        min_price = min(i.price for i in self.icecreams)

        # filter names with minimum price
        names = [i.name for i in self.icecreams if i.price == min_price]

        # return lexicographically smallest name
        return sorted(names)[0]

    def sortIcecreamById(self):
        if not self.icecreams:
            return None

        return sorted([i.id for i in self.icecreams])


# main
n = int(input())
icecreams = []

for _ in range(n):
    id = int(input())
    price = int(input())
    name = input()
    quantityGram = int(input())
    category = input()

    icecreams.append(Icecream(id, price, name, quantityGram, category))

store = IcecreamStore(icecreams)

print(store.findMinimumPrice())
print(store.sortIcecreamById())
````

---

# 🔥 Key Concepts

* **OOP Design** (Class + Objects)
* **Sorting with key**
* **List comprehension**
* **Lexicographic order**
* **Edge case handling**

---

# 💡 Interview Tips

* Always clarify **tie-breaking condition**
* Prefer **built-in functions like min(), sorted()**
* Handle **empty list cases**

---

```

---
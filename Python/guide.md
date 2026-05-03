# Python Complete Guide

## ðŸ Python Basics

### What is Python?
Python is a high-level, interpreted programming language known for:
- Simple, readable syntax
- Dynamic typing
- Object-oriented and functional programming support
- Extensive standard library
- Cross-platform compatibility

### Data Types

```python
# Numbers
integer = 42
floating = 3.14
complex_num = 3 + 4j

# Strings
name = "John"
message = 'Hello'
multiline = """This is
a multiline
string"""

# Boolean
is_valid = True
is_empty = False

# Type checking
type(variable)       # Get data type
isinstance(var, int) # Check type
```

### Variables and Operations

```python
# Assignment
x = 10
y = 20
z = x + y

# Unpacking
a, b, c = 1, 2, 3
x, y = y, x          # Swap

# Operations
x = 10
y = 3
print(x + y)         # Addition: 13
print(x - y)         # Subtraction: 7
print(x * y)         # Multiplication: 30
print(x / y)         # True division: 3.333...
print(x // y)        # Floor division: 3
print(x % y)         # Modulus: 1
print(x ** y)        # Exponentiation: 1000
```

### String Operations

```python
# String methods
name = "John"
name.upper()         # "JOHN"
name.lower()         # "john"
name.capitalize()    # "John"
name.replace("o", "0")  # "J0hn"
name.split()         # Separate by spaces
",".join(["a","b"])  # "a,b"

# String formatting
name = "Alice"
age = 30
print(f"Name: {name}, Age: {age}")  # f-string
print("Name: {}, Age: {}".format(name, age))
print("Name: %s, Age: %d" % (name, age))  # % formatting

# String slicing
s = "Hello"
s[0]                 # "H" (first char)
s[-1]                # "o" (last char)
s[1:4]               # "ell" (index 1 to 3)
s[:3]                # "Hel" (first 3 chars)
s[2:]                # "llo" (from index 2 to end)
s[::2]               # "Hlo" (every 2nd char)
```

### Lists

```python
# List creation and access
fruits = ["apple", "banana", "cherry"]
fruits[0]            # "apple"
fruits[-1]           # "cherry"
fruits[1:3]          # ["banana", "cherry"]

# List methods
fruits.append("date")      # Add to end
fruits.insert(1, "blueberry")  # Insert at index
fruits.remove("banana")    # Remove by value
fruits.pop()               # Remove and return last item
fruits.pop(0)              # Remove first item
fruits.reverse()           # Reverse list
fruits.sort()              # Sort in place
len(fruits)                # Get length

# List comprehension
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
evens = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]
```

### Tuples

```python
# Immutable sequence
coords = (10, 20)
person = ("John", 30, "Engineer")
coords[0]            # 10
# coords[0] = 15    # ERROR! Tuples are immutable

# Tuple unpacking
x, y = coords
name, age, job = person

# Tuple vs List
tuple_data = (1, 2, 3)  # Immutable, faster, hashable
list_data = [1, 2, 3]   # Mutable, flexible
```

### Dictionaries

```python
# Key-value pairs
person = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

# Accessing
person["name"]       # "John"
person.get("age")    # 30
person.get("phone", "N/A")  # "N/A" (default)

# Modification
person["age"] = 31
person["phone"] = "123-456-7890"
del person["city"]

# Iteration
for key in person:
    print(f"{key}: {person[key]}")

# Dictionary methods
person.keys()        # dict_keys(['name', 'age', ...])
person.values()      # dict_values(['John', 31, ...])
person.items()       # dict_items([('name', 'John'), ...])
person.pop("age")    # Remove and return
person.clear()       # Remove all items
```

### Sets

```python
# Unordered, unique values
colors = {"red", "blue", "green"}
colors = set(["red", "blue", "red"])  # {"red", "blue"}

# Set operations
colors.add("yellow")
colors.remove("red")
colors.discard("green")  # No error if missing

# Set math
a = {1, 2, 3}
b = {2, 3, 4}
a | b                # Union: {1, 2, 3, 4}
a & b                # Intersection: {2, 3}
a - b                # Difference: {1}
a ^ b                # Symmetric difference: {1, 4}
a.issubset(b)
a.issuperset(b)
```

### Control Flow

```python
# if...elif...else
age = 20
if age < 13:
    print("Child")
elif age < 18:
    print("Teenager")
elif age < 65:
    print("Adult")
else:
    print("Senior")

# Ternary operator
status = "Adult" if age >= 18 else "Minor"

# Logical operators
if age >= 18 and has_license:
    print("Can drive")

if country == "USA" or country == "Canada":
    print("North America")

if not is_empty:
    print("Not empty")
```

### Loops

```python
# for loop
for i in range(5):
    print(i)         # 0, 1, 2, 3, 4

for i in range(1, 6):
    print(i)         # 1, 2, 3, 4, 5

for i in range(0, 10, 2):
    print(i)         # 0, 2, 4, 6, 8

# Looping through sequences
for fruit in fruits:
    print(fruit)

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

for key, value in person.items():
    print(f"{key}: {value}")

# while loop
count = 0
while count < 5:
    print(count)
    count += 1

# Loop control
for i in range(10):
    if i == 3:
        continue      # Skip to next iteration
    if i == 7:
        break         # Exit loop
    print(i)

# Loop with else
for i in range(5):
    if i == 10:
        break
else:
    print("Loop completed")  # Executes if no break
```

### Functions

```python
# Basic function
def greet(name):
    return f"Hello, {name}!"

result = greet("John")

# Default parameters
def add(a, b=0):
    return a + b

add(5)           # 5
add(5, 3)        # 8

# Multiple return values
def get_coordinates():
    return 10, 20

x, y = get_coordinates()

# *args (variable positional arguments)
def sum_all(*args):
    return sum(args)

sum_all(1, 2, 3, 4)  # 10

# **kwargs (variable keyword arguments)
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="John", age=30, city="NYC")

# Combining all
def complex_function(a, b=2, *args, **kwargs):
    print(f"a={a}, b={b}")
    print(f"args={args}")
    print(f"kwargs={kwargs}")
```

### Lambda Functions

```python
# Anonymous single-expression function
square = lambda x: x ** 2
square(5)            # 25

add = lambda x, y: x + y
add(3, 4)            # 7

# With map, filter, sort
numbers = [1, 2, 3, 4, 5]
squares = list(map(lambda x: x**2, numbers))  # [1, 4, 9, 16, 25]
evens = list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4]

data = [("John", 30), ("Alice", 25), ("Bob", 35)]
sorted_data = sorted(data, key=lambda x: x[1])  # Sort by age
```

### Exception Handling

```python
# try...except
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
except Exception as e:
    print(f"Error: {e}")

# try...except...else
try:
    num = int(input("Enter number: "))
except ValueError:
    print("Invalid number")
else:
    print(f"Number is {num}")

# try...except...finally
try:
    file = open("data.txt")
    data = file.read()
except FileNotFoundError:
    print("File not found")
finally:
    file.close()  # Always executes

# Raising exceptions
if age < 0:
    raise ValueError("Age cannot be negative")
```

---

## ðŸ—ï¸ Object-Oriented Programming (OOP)

### Classes and Objects

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greet(self):
        return f"Hello, I'm {self.name}"
    
    def birthday(self):
        self.age += 1

# Create object
person = Person("John", 30)
print(person.greet())  # "Hello, I'm John"
person.birthday()
print(person.age)      # 31
```

### Inheritance

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        return f"{self.name} makes a sound"

class Dog(Animal):
    def speak(self):
        return f"{self.name} barks"

class Cat(Animal):
    def speak(self):
        return f"{self.name} meows"

dog = Dog("Buddy")
print(dog.speak())  # "Buddy barks"
```

### Polymorphism

```python
def animal_sound(animal):
    print(animal.speak())

dog = Dog("Buddy")
cat = Cat("Whiskers")

animal_sound(dog)    # "Buddy barks"
animal_sound(cat)    # "Whiskers meows"
```

### Encapsulation

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private attribute
    
    def deposit(self, amount):
        self.__balance += amount
    
    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient funds")
    
    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 1500
# account.__balance = 0  # ERROR! Cannot access private attribute
```

### Class Methods and Static Methods

```python
class Math:
    pi = 3.14159
    
    @staticmethod
    def add(a, b):
        return a + b
    
    @classmethod
    def from_string(cls, string):
        a, b = map(int, string.split(','))
        return cls(a, b)
    
    def multiply(self, a, b):
        return a * b

# Static method
Math.add(5, 3)       # 8

# Class variable
Math.pi              # 3.14159
```

---

## ðŸ“š File Handling

```python
# Writing to file
with open("file.txt", "w") as f:
    f.write("Hello, World!\n")
    f.writelines(["Line 1\n", "Line 2\n"])

# Reading from file
with open("file.txt", "r") as f:
    content = f.read()        # Read entire file
    # or
    line = f.readline()       # Read one line
    # or
    lines = f.readlines()     # Read all lines

# Appending to file
with open("file.txt", "a") as f:
    f.write("Appended text\n")

# Working with JSON
import json

data = {"name": "John", "age": 30}
json.dump(data, open("data.json", "w"))
loaded = json.load(open("data.json", "r"))

# CSV files
import csv
with open("data.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["Name", "Age"])
    writer.writerow(["John", 30])
```

---

## ðŸ”§ Common Libraries

```python
# os module
import os
os.getcwd()          # Get current directory
os.listdir(".")      # List files
os.mkdir("newdir")   # Create directory
os.remove("file.txt")  # Delete file

# sys module
import sys
sys.argv             # Command-line arguments
sys.exit(0)          # Exit program

# datetime
from datetime import datetime, timedelta
now = datetime.now()
tomorrow = now + timedelta(days=1)
formatted = now.strftime("%Y-%m-%d")

# math
import math
math.sqrt(16)        # 4
math.ceil(4.3)       # 5
math.floor(4.7)      # 4
math.pi              # 3.14159

# random
import random
random.choice([1, 2, 3])  # Random element
random.randint(1, 10)     # Random int 1-10
random.shuffle(list)      # Shuffle in place
```

---


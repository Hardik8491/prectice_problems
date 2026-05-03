# Python Problems

## Problem 1: Employee Overtime Bonus System

### Problem Statement
Design a system to calculate bonuses for employees based on their overtime hours.

### Requirements:
1. Create `Employee` class with:
   - name, designation, salary
   - overtimeStatus (Boolean)
   - overtimeContribute (Dictionary: month -> hours)

2. Create `Organization` class with:
   - emp_list (List of employees)
   - checkEligibility(m) - Mark eligible if overtime > m
   - bonus(k) - Calculate total bonus

### Input Format:
```
Number of employees
For each employee:
  - Name
  - Designation
  - Salary
  - Number of months
  - For each month: month_name, overtime_days
Overtime threshold (m)
Bonus multiplier (k)
```

### Solution:
```python
class Employee:
    def __init__(self, name, designation, salary):
        self.name = name
        self.designation = designation
        self.salary = salary
        self.overtimeStatus = False
        self.overtimeContribute = {}

class Organization:
    def __init__(self, emp_list):
        self.emp_list = emp_list

    def checkEligibility(self, m):
        for emp in self.emp_list:
            total_hours = sum(emp.overtimeContribute.values())
            if total_hours > m:
                emp.overtimeStatus = True

    def bonus(self, k):
        total = 0
        for emp in self.emp_list:
            if emp.overtimeStatus:
                total += emp.salary
        print(total * k)

# Main execution
n = int(input("Number of employees: "))
emp_list = []

for _ in range(n):
    name = input("Name: ")
    designation = input("Designation: ")
    salary = int(input("Salary: "))
    months = int(input("Months count: ")

    overtime = {}
    for _ in range(months):
        month = input("Month: ")
        days = int(input("Days: "))
        overtime[month] = days

    emp = Employee(name, designation, salary)
    emp.overtimeContribute = overtime
    emp_list.append(emp)

m = int(input("Threshold: "))
k = int(input("Multiplier: "))

org = Organization(emp_list)
org.checkEligibility(m)
org.bonus(k)
```

### Test Case:
```
Input:
2
John
Developer
50000
2
Jan
5
Feb
10
Jane
Tester
40000
2
Jan
3
Feb
2
10
2

Output:
100000
```

---

## Problem 2: Student Grade Management System

### Problem Statement
Create a system to manage student grades and calculate statistics.

### Requirements:
1. Create `Student` class with:
   - name, roll_no, marks (dict: subject -> marks)

2. Create `Classroom` class with:
   - students list
   - add_student(student)
   - get_average(roll_no)
   - topper()
   - subject_average(subject)

### Solution:
```python
class Student:
    def __init__(self, name, roll_no):
        self.name = name
        self.roll_no = roll_no
        self.marks = {}
    
    def add_marks(self, subject, mark):
        self.marks[subject] = mark
    
    def get_average(self):
        if not self.marks:
            return 0
        return sum(self.marks.values()) / len(self.marks)

class Classroom:
    def __init__(self):
        self.students = []
    
    def add_student(self, student):
        self.students.append(student)
    
    def get_average(self, roll_no):
        for student in self.students:
            if student.roll_no == roll_no:
                return student.get_average()
        return None
    
    def topper(self):
        if not self.students:
            return None
        return max(self.students, key=lambda s: s.get_average())
    
    def subject_average(self, subject):
        total = 0
        count = 0
        for student in self.students:
            if subject in student.marks:
                total += student.marks[subject]
                count += 1
        return total / count if count > 0 else 0

# Usage
classroom = Classroom()
s1 = Student("John", 1)
s1.add_marks("Math", 85)
s1.add_marks("Science", 90)

classroom.add_student(s1)
print(f"Average: {classroom.get_average(1)}")
print(f"Topper: {classroom.topper().name}")
```

---

## Problem 3: Bank Account Management

### Problem Statement
Create a banking system with account management features.

### Requirements:
1. Account class with balance management
2. Methods: deposit, withdraw, check_balance
3. Error handling for invalid transactions

### Solution:
```python
class BankAccount:
    def __init__(self, account_number, holder_name, initial_balance=0):
        self.account_number = account_number
        self.holder_name = holder_name
        self.__balance = initial_balance
        self.transactions = []
    
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        self.__balance += amount
        self.transactions.append(f"+{amount}")
    
    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self.__balance:
            raise ValueError("Insufficient funds")
        self.__balance -= amount
        self.transactions.append(f"-{amount}")
    
    def get_balance(self):
        return self.__balance
    
    def get_statement(self):
        print(f"Account: {self.account_number}")
        print(f"Holder: {self.holder_name}")
        print(f"Balance: {self.__balance}")
        print("Transactions:", self.transactions)

# Usage
account = BankAccount("1001", "John Doe", 5000)
account.deposit(1000)
account.withdraw(500)
account.get_statement()
```

---

## Problem 4: To-Do List Manager

### Problem Statement
Create a task management system with priorities.

### Solution:
```python
class Task:
    def __init__(self, title, priority=1, completed=False):
        self.title = title
        self.priority = priority
        self.completed = completed
    
    def mark_complete(self):
        self.completed = True
    
    def __str__(self):
        status = "[âœ“]" if self.completed else "[ ]"
        return f"{status} {self.title} (Priority: {self.priority})"

class TodoList:
    def __init__(self):
        self.tasks = []
    
    def add_task(self, title, priority=1):
        task = Task(title, priority)
        self.tasks.append(task)
    
    def remove_task(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks.pop(index)
    
    def sort_by_priority(self):
        self.tasks.sort(key=lambda t: t.priority)
    
    def display_tasks(self):
        for i, task in enumerate(self.tasks):
            print(f"{i+1}. {task}")
    
    def mark_complete(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks[index].mark_complete()

# Usage
todo = TodoList()
todo.add_task("Complete project", 1)
todo.add_task("Review code", 2)
todo.display_tasks()
```

---


# 📋 UNIX, Python & SQL - Complete Questions & Problems

## 📑 Table of Contents
1. [UNIX Questions](#unix-questions)
2. [Python Problems](#python-problems)
3. [SQL Problems](#sql-problems)
4. [Integrated Challenges](#integrated-challenges)

---

# UNIX Questions

## Basic Concepts

### Q1: Explain the architecture of UNIX Operating System
**Answer:**
The UNIX OS has three main layers:
1. **Kernel** - Core that manages resources (memory, processes, files, I/O)
2. **Shell** - Command interpreter that processes user commands
3. **Utilities** - User programs and applications

**Diagram:**
```
┌──────────────────────────────────────┐
│      User Interface (Shell)          │
├──────────────────────────────────────┤
│      System Calls                    │
├──────────────────────────────────────┤
│   Kernel (Resource Management)       │
├──────────────────────────────────────┤
│   Hardware (CPU, Memory, I/O)        │
└──────────────────────────────────────┘
```

### Q2: What are the key features of UNIX?
**Answer:**
- **Multi-user** - Multiple users can work simultaneously
- **Multitasking** - Multiple processes run concurrently
- **Portability** - Written in C, runs on various platforms
- **Security** - User authentication and file permissions
- **Modularity** - Small, single-purpose programs
- **Piping** - Connect programs with pipes (|)

### Q3: Differentiate between absolute and relative pathnames
**Answer:**
- **Absolute pathname** - Starts from root (/) and specifies full path
  - Example: `/home/user/documents/file.txt`
  
- **Relative pathname** - Relative to current working directory
  - Example: `documents/file.txt` (if in /home/user)
  - Example: `../file.txt` (parent directory)

### Q4: What is an inode and what information does it contain?
**Answer:**
An **inode** is a disk file record (64 bytes) containing file metadata:
- Owner and group IDs
- File type and size
- Number of hard links
- Access permissions (rwx)
- Timestamps (creation, access, modification)
- Reference count (open count)
- 13 pointers to data blocks

**Importance:** Allows the kernel to locate file on disk and verify access permissions.

### Q5: Explain file permissions in UNIX
**Answer:**
Three permission types for three ownership levels:

| Permission | File Meaning | Directory Meaning |
|------------|-------------|-------------------|
| **r (4)** | Read content | List contents |
| **w (2)** | Modify | Create/delete files |
| **x (1)** | Execute | Enter directory |

**Ownership levels:** User (u), Group (g), Others (o)

**Example:** `chmod 755 file.txt`
- User: 7 = rwx (4+2+1)
- Group: 5 = r-x (4+1)
- Others: 5 = r-x (4+1)

---

## Command Practice

### Q6: Write commands for the following tasks:

**a) Find all files ending with .txt in current directory**
```bash
find . -name "*.txt"
```

**b) Show last 20 lines of a file**
```bash
tail -20 file.txt
```

**c) Count the number of words in a file**
```bash
wc -w file.txt
```

**d) Search for pattern "error" in all files**
```bash
grep -r "error" .
```

**e) Change permissions to make file executable**
```bash
chmod +x file.sh
chmod 755 file.sh
```

**f) Copy directory with all subdirectories**
```bash
cp -r source_dir dest_dir
```

### Q7: What is the output of these commands?

**a) `ls -la`**
- Lists all files and directories in long format
- `-l` = long format, `-a` = include hidden files

**b) `grep "pattern" file | wc -l`**
- Counts lines containing "pattern" in file

**c) `find . -size +10M`**
- Finds all files larger than 10MB

**d) `ps aux | grep "java"`**
- Shows all java processes running

### Q8: Pipe exercises

**a) Display first 10 lines of a large file and sort them**
```bash
head -10 large_file.txt | sort
```

**b) Find all Python files and count them**
```bash
find . -name "*.py" | wc -l
```

**c) Get unique department names sorted alphabetically**
```bash
cat employees.csv | cut -d, -f3 | sort | uniq
```

**d) Extract and count occurrences of each user**
```bash
who | cut -d' ' -f1 | sort | uniq -c
```

---

## Shell Scripting

### Q9: Write a shell script to check if a file exists
**Answer:**
```bash
#!/bin/bash

read -p "Enter filename: " filename

if [ -f "$filename" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

### Q10: Write a shell script to calculate factorial
**Answer:**
```bash
#!/bin/bash

read -p "Enter a number: " num

factorial=1
i=1

while [ $i -le $num ]; do
    factorial=$((factorial * i))
    i=$((i + 1))
done

echo "Factorial of $num is $factorial"
```

### Q11: Write a script to find the largest file in a directory
**Answer:**
```bash
#!/bin/bash

if [ -z "$1" ]; then
    directory="."
else
    directory="$1"
fi

largest_file=$(find "$directory" -type f -exec ls -lS {} + | head -1)
echo "Largest file: $largest_file"
```

### Q12: Write a script to backup files daily
**Answer:**
```bash
#!/bin/bash

source_dir="/home/user/documents"
backup_dir="/backup/documents"
date=$(date +%Y-%m-%d)

mkdir -p "$backup_dir"
cp -r "$source_dir"/* "$backup_dir/backup_$date/"
echo "Backup completed on $date"
```

---

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
        status = "[✓]" if self.completed else "[ ]"
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

# SQL Problems

## Problem 1: Company Database Management

### Schema Design:
```sql
CREATE DATABASE company_db;

CREATE TABLE departments (
    dept_id INT PRIMARY KEY AUTO_INCREMENT,
    dept_name VARCHAR(100) NOT NULL,
    location VARCHAR(100)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    emp_name VARCHAR(100) NOT NULL,
    designation VARCHAR(50),
    salary DECIMAL(10, 2),
    dept_id INT,
    hire_date DATE,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);

CREATE TABLE projects (
    proj_id INT PRIMARY KEY AUTO_INCREMENT,
    proj_name VARCHAR(100),
    start_date DATE,
    end_date DATE
);

CREATE TABLE emp_projects (
    emp_id INT,
    proj_id INT,
    hours_allocated INT,
    PRIMARY KEY (emp_id, proj_id),
    FOREIGN KEY (emp_id) REFERENCES employees(emp_id),
    FOREIGN KEY (proj_id) REFERENCES projects(proj_id)
);
```

### Sample Data:
```sql
INSERT INTO departments VALUES 
(1, 'IT', 'New York'),
(2, 'Sales', 'Los Angeles'),
(3, 'Finance', 'Chicago');

INSERT INTO employees VALUES
(1, 'John Doe', 'Developer', 75000, 1, '2020-01-15'),
(2, 'Jane Smith', 'Manager', 85000, 2, '2019-06-20'),
(3, 'Bob Johnson', 'Analyst', 65000, 3, '2021-03-10');
```

### Queries:

**Q1: Find employees earning more than average salary**
```sql
SELECT emp_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees)
ORDER BY salary DESC;
```

**Q2: Count employees by department**
```sql
SELECT d.dept_name, COUNT(e.emp_id) as emp_count
FROM departments d
LEFT JOIN employees e ON d.dept_id = e.dept_id
GROUP BY d.dept_id, d.dept_name;
```

**Q3: Get department with highest average salary**
```sql
SELECT d.dept_name, AVG(e.salary) as avg_salary
FROM departments d
JOIN employees e ON d.dept_id = e.dept_id
GROUP BY d.dept_id, d.dept_name
ORDER BY avg_salary DESC
LIMIT 1;
```

**Q4: Find employees not assigned to any project**
```sql
SELECT e.emp_id, e.emp_name
FROM employees e
WHERE e.emp_id NOT IN (
    SELECT DISTINCT emp_id FROM emp_projects
);
```

**Q5: Get project details with employee count**
```sql
SELECT p.proj_name, COUNT(ep.emp_id) as emp_count
FROM projects p
LEFT JOIN emp_projects ep ON p.proj_id = ep.proj_id
GROUP BY p.proj_id, p.proj_name;
```

---

## Problem 2: E-Commerce Database

### Schema:
```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_name VARCHAR(100),
    email VARCHAR(100),
    country VARCHAR(50)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(8, 2),
    stock INT
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE order_items (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT,
    unit_price DECIMAL(8, 2),
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

### Sample Queries:

**Q1: Total sales by product**
```sql
SELECT p.product_name, SUM(oi.quantity) as total_quantity, 
       SUM(oi.quantity * oi.unit_price) as total_sales
FROM products p
LEFT JOIN order_items oi ON p.product_id = oi.product_id
GROUP BY p.product_id, p.product_name
ORDER BY total_sales DESC;
```

**Q2: Customers who spent more than 5000**
```sql
SELECT c.customer_name, SUM(o.total_amount) as total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.customer_name
HAVING SUM(o.total_amount) > 5000;
```

**Q3: Top 5 customers by spending**
```sql
SELECT c.customer_name, SUM(o.total_amount) as total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.customer_name
ORDER BY total_spent DESC
LIMIT 5;
```

**Q4: Products never ordered**
```sql
SELECT p.product_name
FROM products p
WHERE p.product_id NOT IN (
    SELECT DISTINCT product_id FROM order_items
);
```

---

## Problem 3: Student Management System

### Schema:
```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY AUTO_INCREMENT,
    course_name VARCHAR(100),
    credits INT
);

CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    student_name VARCHAR(100),
    enrollment_year INT
);

CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    course_id INT,
    marks INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

### Queries:

**Q1: Average marks per course**
```sql
SELECT c.course_name, AVG(e.marks) as avg_marks
FROM courses c
JOIN enrollments e ON c.course_id = e.course_id
GROUP BY c.course_id, c.course_name;
```

**Q2: Student with highest average**
```sql
SELECT s.student_name, AVG(e.marks) as avg_marks
FROM students s
JOIN enrollments e ON s.student_id = e.student_id
GROUP BY s.student_id, s.student_name
ORDER BY avg_marks DESC
LIMIT 1;
```

**Q3: Students failing any course (marks < 40)**
```sql
SELECT DISTINCT s.student_name
FROM students s
JOIN enrollments e ON s.student_id = e.student_id
WHERE e.marks < 40;
```

---

# Integrated Challenges

## Challenge 1: Build a Complete School Management System

### Phase 1: Design (SQL)
- Create database schema for students, teachers, classes, subjects, grades
- Define relationships between entities

### Phase 2: Backend (Python + SQL)
- Create Python classes to manage database operations
- Implement CRUD operations
- Calculate GPA, class rankings

### Phase 3: Shell Script (Bash)
- Create backup script for database
- Monitor database performance
- Generate reports

---

## Challenge 2: Log Analysis System

### Phase 1: Generate Log Files (Bash)
```bash
#!/bin/bash
# Generate sample logs
for i in {1..100}; do
    echo "$(date '+%Y-%m-%d %H:%M:%S') ERROR: Process failed" >> system.log
done
```

### Phase 2: Parse and Analyze (Python)
```python
import re
from collections import Counter

with open('system.log', 'r') as f:
    errors = [line for line in f if 'ERROR' in line]
    print(f"Total errors: {len(errors)}")
```

### Phase 3: Store in Database (SQL)
```sql
CREATE TABLE logs (
    log_id INT PRIMARY KEY AUTO_INCREMENT,
    timestamp DATETIME,
    level VARCHAR(20),
    message TEXT
);
```

---

## Challenge 3: File Processing Pipeline

### Scenario:
1. **UNIX:** Gather all CSV files from a directory
2. **Python:** Parse and clean data
3. **SQL:** Load into database and generate reports

### UNIX commands:
```bash
find . -name "*.csv" -type f
```

### Python script:
```python
import csv
import mysql.connector

for file in ['file1.csv', 'file2.csv']:
    with open(file, 'r') as f:
        reader = csv.DictReader(f)
        for row in reader:
            # Insert into database
            pass
```

---

**Created:** May 3, 2026
**Subject Matter:** UNIX, Python, and SQL
**Purpose:** Comprehensive learning and interview preparation

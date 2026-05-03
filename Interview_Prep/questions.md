# Interview Questions

## UNIX Interview Questions

### Beginner Level

1. **What is the difference between Unix and Linux?**
   - Unix is a proprietary OS (Solaris, AIX, HP-UX)
   - Linux is free, open-source, Unix-like OS

2. **What does the shebang (#!) do in shell scripts?**
   - Tells the system which interpreter to use

3. **How do you make a file executable in Unix?**
   ```bash
   chmod +x filename
   chmod 755 filename
   ```

4. **What's the difference between > and >> redirection?**
   - `>` overwrites the file
   - `>>` appends to the file

5. **How do you find a file named "test.txt"?**
   ```bash
   find . -name "test.txt"
   ```

### Intermediate Level

6. **Explain the difference between pipes and redirection.**
   - Redirection: sends output to/from files
   - Pipes: connect output of one command to input of another

7. **What is the purpose of the grep command?**
   - Search for patterns in files

8. **How do you count the number of lines in a file?**
   ```bash
   wc -l filename
   ```

9. **What's the difference between soft and hard links?**
   - Soft link: symbolic link pointing to file path
   - Hard link: multiple names for same inode

10. **How do you change file permissions?**
    ```bash
    chmod u+x file.txt    # User execute
    chmod 755 file.txt    # User rwx, group rx, other rx
    ```

### Advanced Level

11. **Explain the process of booting a Unix system.**
    - BIOS â†’ Bootloader â†’ Kernel â†’ Init â†’ User login

12. **What are daemon processes?**
    - Background processes that run independently (e.g., sshd, httpd)

13. **How do you monitor system resources?**
    ```bash
    top, ps aux, vmstat, iostat, df, du
    ```

14. **Explain inode structure and its importance.**
    - Inode contains file metadata
    - Points to actual data blocks on disk

15. **How do you schedule recurring tasks?**
    ```bash
    crontab -e
    0 2 * * * /backup.sh  # Run at 2 AM daily
    ```

---

## Python Interview Questions

### Beginner Level

1. **What is Python and why is it popular?**
   - High-level, interpreted language
   - Simple syntax, large library, cross-platform

2. **What's the difference between list and tuple?**
   - List: mutable, changeable
   - Tuple: immutable, fixed

3. **How do you define a function in Python?**
   ```python
   def function_name(parameters):
       return value
   ```

4. **What are list comprehensions?**
   ```python
   [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
   ```

5. **What's the purpose of __init__ method?**
   - Constructor that initializes object attributes

### Intermediate Level

6. **Explain decorators in Python.**
   - Functions that modify behavior of other functions
   ```python
   @decorator
   def function():
       pass
   ```

7. **What's the difference between append() and extend()?**
   - append(): adds single element
   - extend(): adds multiple elements

8. **How do you handle exceptions?**
   ```python
   try:
       # code
   except SpecificError:
       # handle
   finally:
       # cleanup
   ```

9. **What are lambda functions used for?**
   - Anonymous, single-expression functions
   - Often used with map(), filter(), sort()

10. **Explain list vs generator.**
    - List: entire sequence in memory
    - Generator: yields values one at a time

### Advanced Level

11. **What's the Global Interpreter Lock (GIL)?**
    - Allows only one thread to execute Python code at a time

12. **Explain *args and **kwargs.**
    - *args: variable positional arguments (tuple)
    - **kwargs: variable keyword arguments (dict)

13. **What are context managers?**
    - Manage resource setup and cleanup
    - `with` statement

14. **Explain the difference between shallow and deep copy.**
    - Shallow: copies object references
    - Deep: copies entire object structure

15. **How do you implement a singleton pattern?**
    ```python
    class Singleton:
        _instance = None
        def __new__(cls):
            if cls._instance is None:
                cls._instance = super().__new__(cls)
            return cls._instance
    ```

---

## SQL Interview Questions

### Beginner Level

1. **What is SQL and what are its main operations?**
   - Query language for databases
   - CRUD: Create, Read, Update, Delete

2. **What's the difference between WHERE and HAVING?**
   - WHERE: filters rows before grouping
   - HAVING: filters groups after grouping

3. **Explain primary key and foreign key.**
   - Primary key: unique identifier for record
   - Foreign key: references primary key in another table

4. **What's ACID in databases?**
   - Atomicity, Consistency, Isolation, Durability

5. **How do you join tables?**
   ```sql
   SELECT * FROM table1
   JOIN table2 ON table1.id = table2.id
   ```

### Intermediate Level

6. **Difference between INNER JOIN and LEFT JOIN.**
   - INNER JOIN: only matching records
   - LEFT JOIN: all from left, matching from right

7. **What are indexes and why are they important?**
   - Speed up queries by creating sorted structure
   - Slow down inserts/updates

8. **Explain subqueries.**
   - Query within a query
   - Can be in SELECT, FROM, WHERE clauses

9. **What's the difference between UNION and UNION ALL?**
   - UNION: removes duplicates
   - UNION ALL: keeps all records

10. **How do you use GROUP BY and aggregate functions?**
    ```sql
    SELECT department, COUNT(*), AVG(salary)
    FROM employees
    GROUP BY department
    ```

### Advanced Level

11. **Explain normalization.**
    - Process of organizing data to reduce redundancy
    - Normal forms: 1NF, 2NF, 3NF, BCNF

12. **What are transactions and ACID properties?**
    - Group of SQL operations treated as single unit
    - Ensures data consistency

13. **Explain views and their advantages.**
    - Virtual tables based on queries
    - Simplify complex queries, enhance security

14. **How do you optimize SQL queries?**
    - Use indexes
    - Avoid SELECT *
    - Use EXPLAIN to analyze
    - Denormalization when needed

15. **What's a stored procedure?**
    ```sql
    CREATE PROCEDURE GetEmployees
    AS
    SELECT * FROM employees
    WHERE salary > 50000
    ```

---

## Integration Problems

### Problem 1: Employee Overtime Bonus System (Python)

See question1.md for complete problem and solution.

**Key Concepts:**
- Object-Oriented Programming (OOP)
- Class design with attributes and methods
- Dictionary for data storage
- List operations and aggregations
- Conditional logic

---

## ðŸš€ Study Tips

1. **UNIX**: Practice commands daily, understand pipes and filters
2. **Python**: Write code regularly, focus on data structures and OOP
3. **SQL**: Design schemas, write complex queries, understand joins

---

## ðŸ“– Quick Reference

### Common Commands Cheatsheet

```bash
# Navigation
pwd, cd, ls, mkdir, rmdir

# File operations
cat, touch, cp, mv, rm, grep, find

# Text processing
grep, sed, awk, cut, paste, sort, uniq

# Permissions
chmod, chown, chgrp

# Process management
ps, kill, bg, fg, nohup, nice

# System info
uname, whoami, date, df, du, free, top
```

### Python Quick Syntax

```python
# Data structures
list, tuple, dict, set

# Control flow
if/elif/else, for, while, try/except

# Functions
def, lambda, @decorator

# OOP
class, __init__, inheritance, polymorphism

# Modules
import, from...import
```

### SQL Quick Syntax

```sql
-- DDL
CREATE, ALTER, DROP

-- DML
SELECT, INSERT, UPDATE, DELETE

-- Functions
COUNT, SUM, AVG, MIN, MAX
GROUP BY, HAVING, ORDER BY

-- Joins
INNER, LEFT, RIGHT, FULL, CROSS

-- Constraints
PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL
```

---

## ðŸ“ž Support and Resources

- UNIX Documentation: `man command_name`
- Python Official Docs: https://docs.python.org/3/
- SQL Tutorials: https://www.w3schools.com/sql/
- Online IDE: Repl.it, LeetCode, HackerRank

---

**Last Updated:** May 3, 2026

This comprehensive guide covers the fundamentals and advanced concepts of UNIX, Python, and SQL. Use it as a reference for learning, interviews, and problem-solving!

# 📚 SQL - Complete Learning Guide

**Version:** 1.0 | **Last Updated:** May 3, 2026

---

## 📑 Table of Contents

1. [SQL Fundamentals](#sql-fundamentals)
2. [Database Design](#database-design)
3. [CRUD Operations](#crud-operations)
4. [Query Operations](#query-operations)
5. [Advanced Queries](#advanced-queries)
6. [Joins](#joins)
7. [Aggregation & Grouping](#aggregation--grouping)
8. [Subqueries & Complex Queries](#subqueries--complex-queries)
9. [Views & Indexes](#views--indexes)
10. [Transactions](#transactions)
11. [Stored Procedures & Functions](#stored-procedures--functions)
12. [SQL Optimization](#sql-optimization)
13. [Practice Problems](#practice-problems)

---

# SQL Fundamentals

## What is SQL?

**SQL (Structured Query Language)** is a standard language for:
- **Creating** databases and tables
- **Inserting** data
- **Querying** data
- **Updating** records
- **Deleting** records
- **Managing** database objects
- **Controlling** access and security

## SQL Dialects

Different database systems have slightly different SQL syntax:
- **MySQL** - Open-source, popular for web applications
- **PostgreSQL** - Open-source, feature-rich
- **Oracle** - Enterprise, powerful
- **SQL Server** - Microsoft's relational database
- **SQLite** - Lightweight, embedded databases

## Data Types

### Numeric Types

```sql
INT, BIGINT, SMALLINT      -- Integers
TINYINT                    -- Small integer (-128 to 127)
DECIMAL(p,s), NUMERIC      -- Fixed-point numbers
FLOAT, DOUBLE, REAL        -- Floating-point numbers
```

### String Types

```sql
CHAR(n)                    -- Fixed-length string
VARCHAR(n)                 -- Variable-length string
TEXT                       -- Large text
LONGTEXT                   -- Very large text
NVARCHAR(n)               -- Unicode string
```

### Date/Time Types

```sql
DATE                       -- YYYY-MM-DD
TIME                       -- HH:MM:SS
DATETIME                   -- YYYY-MM-DD HH:MM:SS
TIMESTAMP                  -- Date and time with timezone
YEAR                       -- Year only
```

### Boolean Type

```sql
BOOLEAN, BOOL             -- TRUE or FALSE (1 or 0)
```

### Special Types

```sql
JSON                       -- JSON document
BLOB                       -- Binary data
ENUM                       -- Fixed set of values
```

---

# Database Design

## Creating Databases

```sql
-- Create database
CREATE DATABASE company_db;

-- Create database with character set
CREATE DATABASE company_db CHARACTER SET utf8mb4;

-- Drop database
DROP DATABASE company_db;

-- Use database
USE company_db;
```

## Creating Tables

### Basic Table Creation

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    salary DECIMAL(10, 2),
    hire_date DATE,
    is_active BOOLEAN DEFAULT TRUE
);
```

### Table with Constraints

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY AUTO_INCREMENT,
    dept_name VARCHAR(100) NOT NULL UNIQUE,
    budget DECIMAL(12, 2) CHECK (budget > 0),
    created_date DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

### Table with Foreign Key

```sql
CREATE TABLE projects (
    project_id INT PRIMARY KEY AUTO_INCREMENT,
    project_name VARCHAR(100) NOT NULL,
    dept_id INT,
    start_date DATE,
    end_date DATE,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

## Constraints

| Constraint | Purpose | Example |
|-----------|---------|---------|
| **PRIMARY KEY** | Unique identifier | `id INT PRIMARY KEY` |
| **UNIQUE** | Ensure unique values | `email VARCHAR(100) UNIQUE` |
| **NOT NULL** | Column must have value | `name VARCHAR(100) NOT NULL` |
| **DEFAULT** | Default value if not provided | `status VARCHAR(20) DEFAULT 'active'` |
| **CHECK** | Validate values | `age INT CHECK (age >= 18)` |
| **FOREIGN KEY** | Reference another table | `dept_id INT FOREIGN KEY REFERENCES departments(dept_id)` |

## Modifying Tables

```sql
-- Add column
ALTER TABLE employees ADD COLUMN department VARCHAR(50);

-- Modify column type
ALTER TABLE employees MODIFY COLUMN salary DECIMAL(12, 2);

-- Drop column
ALTER TABLE employees DROP COLUMN department;

-- Rename table
ALTER TABLE employees RENAME TO staff;

-- Rename column
ALTER TABLE employees CHANGE COLUMN name employee_name VARCHAR(100);

-- Add constraint
ALTER TABLE employees ADD UNIQUE (email);

-- Drop constraint
ALTER TABLE employees DROP INDEX email;

-- Drop table
DROP TABLE employees;
```

---

# CRUD Operations

## CREATE (INSERT)

### Single Row Insert

```sql
INSERT INTO employees (name, email, salary, hire_date)
VALUES ('John Doe', 'john@example.com', 75000, '2025-01-15');
```

### Multiple Row Insert

```sql
INSERT INTO employees (name, email, salary, hire_date)
VALUES 
    ('Jane Smith', 'jane@example.com', 82000, '2025-02-20'),
    ('Bob Johnson', 'bob@example.com', 68000, '2025-03-10'),
    ('Alice Brown', 'alice@example.com', 90000, '2025-01-05');
```

### Insert with Default Values

```sql
INSERT INTO employees (name, email)
VALUES ('Default User', 'default@example.com');
-- salary, hire_date, is_active will use defaults
```

### Insert from SELECT

```sql
INSERT INTO employees_archive
SELECT * FROM employees WHERE hire_date < '2020-01-01';
```

## READ (SELECT)

### Basic SELECT

```sql
-- Select all columns and rows
SELECT * FROM employees;

-- Select specific columns
SELECT name, email, salary FROM employees;

-- Select with aliases
SELECT name AS employee_name, salary AS annual_salary FROM employees;
```

### WHERE Clause

```sql
-- Simple condition
SELECT * FROM employees WHERE salary > 75000;

-- Multiple conditions
SELECT * FROM employees 
WHERE salary > 75000 AND dept_id = 1;

SELECT * FROM employees 
WHERE dept_id = 1 OR dept_id = 2;

-- NOT condition
SELECT * FROM employees WHERE NOT is_active;
```

### Comparison Operators

```sql
= (equal)
!= or <> (not equal)
> (greater than)
< (less than)
>= (greater than or equal)
<= (less than or equal)
BETWEEN (range)
IN (list of values)
LIKE (pattern matching)
IS NULL / IS NOT NULL
```

### LIKE Pattern Matching

```sql
-- Starts with
SELECT * FROM employees WHERE name LIKE 'John%';

-- Contains
SELECT * FROM employees WHERE email LIKE '%@gmail.com';

-- Specific pattern
SELECT * FROM employees WHERE name LIKE '_ohn%';  -- 4th char is 'h', starts with any 3 chars

-- Ends with
SELECT * FROM employees WHERE email LIKE '%.org';
```

### BETWEEN Operator

```sql
-- Between range
SELECT * FROM employees WHERE salary BETWEEN 50000 AND 80000;

-- Date range
SELECT * FROM employees WHERE hire_date BETWEEN '2023-01-01' AND '2024-12-31';
```

### IN Operator

```sql
-- Select specific IDs
SELECT * FROM employees WHERE id IN (1, 5, 10, 15);

-- Subquery in IN
SELECT * FROM employees WHERE dept_id IN (
    SELECT dept_id FROM departments WHERE budget > 100000
);
```

### NULL Handling

```sql
-- Find NULL values
SELECT * FROM employees WHERE department IS NULL;

-- Find non-NULL values
SELECT * FROM employees WHERE department IS NOT NULL;

-- COALESCE for default values
SELECT name, COALESCE(department, 'Unassigned') AS dept FROM employees;
```

## UPDATE

### Simple Update

```sql
UPDATE employees SET salary = 80000 WHERE id = 1;
```

### Multiple Columns

```sql
UPDATE employees 
SET salary = 85000, department = 'IT' 
WHERE id = 1;
```

### Conditional Update

```sql
-- Increase salary by 10% for IT department
UPDATE employees 
SET salary = salary * 1.1 
WHERE department = 'IT';

-- Update based on calculation
UPDATE employees 
SET hire_date = CURDATE() 
WHERE is_active = TRUE AND hire_date IS NULL;
```

### Update with JOIN

```sql
UPDATE employees e
INNER JOIN departments d ON e.dept_id = d.dept_id
SET e.salary = e.salary * 1.05
WHERE d.dept_name = 'Sales';
```

## DELETE

### Simple Delete

```sql
DELETE FROM employees WHERE id = 5;
```

### Delete with Condition

```sql
-- Delete inactive employees
DELETE FROM employees WHERE is_active = FALSE;

-- Delete old records
DELETE FROM employees WHERE hire_date < '2015-01-01';
```

### Delete All Records

```sql
DELETE FROM employees;
```

### TRUNCATE (Faster)

```sql
TRUNCATE TABLE employees;  -- Removes all rows, resets auto-increment
```

---

# Query Operations

## Sorting Results

### ORDER BY

```sql
-- Sort ascending (default)
SELECT * FROM employees ORDER BY salary;

-- Sort descending
SELECT * FROM employees ORDER BY salary DESC;

-- Sort by multiple columns
SELECT * FROM employees ORDER BY department ASC, salary DESC;

-- Sort by column position
SELECT id, name, salary FROM employees ORDER BY 3 DESC;  -- Sort by 3rd column (salary)
```

## Limiting Results

### LIMIT

```sql
-- First 10 records
SELECT * FROM employees LIMIT 10;

-- Skip first 10, get next 10 (offset)
SELECT * FROM employees LIMIT 10 OFFSET 10;

-- Alternate syntax
SELECT * FROM employees LIMIT 10, 10;
```

## Distinct Values

### DISTINCT

```sql
-- Get unique departments
SELECT DISTINCT department FROM employees;

-- Multiple columns
SELECT DISTINCT department, job_title FROM employees;

-- Count distinct
SELECT COUNT(DISTINCT department) FROM employees;
```

## String Functions

```sql
-- Case conversion
SELECT UPPER(name) FROM employees;           -- Uppercase
SELECT LOWER(name) FROM employees;           -- Lowercase
SELECT CONCAT(UPPER(name), ' (ID: ', id, ')')  -- Concatenate

-- Length and substrings
SELECT LENGTH(name) FROM employees;
SELECT SUBSTRING(name, 1, 5) FROM employees;  -- First 5 chars
SELECT SUBSTR(email, POSITION('@' IN email) + 1) FROM employees;  -- Domain part

-- Trim and Replace
SELECT TRIM(name) FROM employees;            -- Remove spaces
SELECT LTRIM(name), RTRIM(name) FROM employees;
SELECT REPLACE(email, '.com', '.org') FROM employees;

-- REVERSE and REPEAT
SELECT REVERSE(name) FROM employees;
SELECT REPEAT('*', 5);                       -- *****

-- LPAD and RPAD
SELECT LPAD(id, 5, '0') FROM employees;     -- Pad left with zeros
SELECT RPAD(name, 20, '.') FROM employees;  -- Pad right with dots
```

## Numeric Functions

```sql
-- Rounding
SELECT ROUND(salary, 2) FROM employees;
SELECT CEIL(salary) FROM employees;           -- Round up
SELECT FLOOR(salary) FROM employees;          -- Round down
SELECT TRUNCATE(salary, 2) FROM employees;    -- Truncate decimals

-- Math operations
SELECT ABS(-100);                             -- Absolute value
SELECT POWER(2, 3);                           -- 2^3 = 8
SELECT SQRT(16);                              -- Square root = 4
SELECT MOD(10, 3);                            -- Modulus = 1
SELECT GREATEST(10, 20, 5);                   -- Maximum
SELECT LEAST(10, 20, 5);                      -- Minimum
```

## Date Functions

```sql
-- Current date/time
SELECT CURDATE();                             -- 2026-05-03
SELECT CURTIME();                             -- 14:30:45
SELECT NOW();                                 -- 2026-05-03 14:30:45

-- Date manipulation
SELECT DATE_ADD(NOW(), INTERVAL 30 DAY);      -- 30 days from now
SELECT DATE_SUB(NOW(), INTERVAL 1 MONTH);    -- 1 month ago
SELECT ADDDATE(NOW(), 7);                     -- 7 days from now

-- Date difference
SELECT DATEDIFF('2026-12-31', CURDATE());     -- Days between dates
SELECT TIMEDIFF('14:30:00', '10:15:00');      -- Time difference

-- Extract parts
SELECT YEAR(hire_date) FROM employees;
SELECT MONTH(hire_date) FROM employees;
SELECT DAY(hire_date) FROM employees;
SELECT QUARTER(hire_date) FROM employees;
SELECT WEEK(hire_date) FROM employees;

-- Date formatting
SELECT DATE_FORMAT(hire_date, '%Y-%m-%d') FROM employees;
SELECT DATE_FORMAT(NOW(), '%d/%m/%Y %H:%i:%s');

-- Date parsing
SELECT STR_TO_DATE('2026-05-03', '%Y-%m-%d');
```

---

# Advanced Queries

## Aggregate Functions

### COUNT

```sql
-- Count all rows
SELECT COUNT(*) FROM employees;

-- Count specific column (excludes NULL)
SELECT COUNT(department) FROM employees;

-- Count distinct values
SELECT COUNT(DISTINCT department) FROM employees;

-- Count with condition
SELECT COUNT(*) FROM employees WHERE salary > 75000;
```

### SUM

```sql
-- Total salary
SELECT SUM(salary) FROM employees;

-- Sum with condition
SELECT SUM(salary) FROM employees WHERE department = 'IT';

-- Sum with CASE
SELECT SUM(CASE WHEN department = 'IT' THEN salary ELSE 0 END) FROM employees;
```

### AVG

```sql
-- Average salary
SELECT AVG(salary) FROM employees;

-- Average with condition
SELECT AVG(salary) FROM employees WHERE hire_date > '2020-01-01';

-- Average with rounding
SELECT ROUND(AVG(salary), 2) FROM employees;
```

### MIN and MAX

```sql
-- Minimum salary
SELECT MIN(salary) FROM employees;

-- Maximum salary
SELECT MAX(salary) FROM employees;

-- Both together
SELECT MIN(salary) AS min_salary, MAX(salary) AS max_salary FROM employees;

-- Min/Max with date
SELECT MIN(hire_date), MAX(hire_date) FROM employees;
```

### Combined Aggregate Functions

```sql
SELECT 
    COUNT(*) AS total_employees,
    SUM(salary) AS total_salary,
    AVG(salary) AS avg_salary,
    MIN(salary) AS min_salary,
    MAX(salary) AS max_salary
FROM employees;
```

---

# GROUP BY and HAVING

## GROUP BY Basics

```sql
-- Count employees per department
SELECT department, COUNT(*) AS emp_count
FROM employees
GROUP BY department;

-- Average salary per department
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;

-- Multiple columns
SELECT department, job_title, COUNT(*) AS count
FROM employees
GROUP BY department, job_title;
```

## HAVING Clause

```sql
-- Departments with more than 5 employees
SELECT department, COUNT(*) AS count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;

-- Departments with average salary > 75000
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 75000;

-- Complex HAVING
SELECT department, COUNT(*) AS count, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING COUNT(*) > 3 AND AVG(salary) > 70000;
```

## ORDER BY with GROUP BY

```sql
SELECT department, COUNT(*) AS count, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC;
```

---

# Joins

## INNER JOIN

```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;

-- Multiple conditions
SELECT e.name, p.project_name
FROM employees e
INNER JOIN projects p ON e.id = p.employee_id AND e.is_active = TRUE;
```

## LEFT JOIN (LEFT OUTER JOIN)

```sql
-- All employees, including those without department
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id;

-- Find employees without department
SELECT e.name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id
WHERE d.dept_id IS NULL;
```

## RIGHT JOIN (RIGHT OUTER JOIN)

```sql
-- All departments, even if no employees
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id;
```

## FULL OUTER JOIN

```sql
-- All from both tables
SELECT e.name, d.department_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.dept_id;

-- Note: MySQL doesn't support FULL OUTER JOIN directly
-- Use UNION of LEFT and RIGHT JOIN instead
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id
UNION
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id;
```

## CROSS JOIN

```sql
-- Cartesian product
SELECT e.name, p.project_name
FROM employees e
CROSS JOIN projects p;
-- Result: every employee with every project
```

## Self Join

```sql
-- Find employees and their managers
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

## Multiple Joins

```sql
SELECT 
    e.name,
    d.department_name,
    p.project_name,
    pr.name AS project_role
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id
INNER JOIN employee_projects ep ON e.id = ep.employee_id
INNER JOIN projects p ON ep.project_id = p.id
INNER JOIN project_roles pr ON ep.role_id = pr.id;
```

---

# Subqueries and Complex Queries

## Subqueries in WHERE

```sql
-- Employees earning more than average
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

-- Employees in specific departments
SELECT name
FROM employees
WHERE dept_id IN (
    SELECT dept_id FROM departments WHERE budget > 100000
);
```

## Subqueries in FROM

```sql
SELECT * FROM (
    SELECT name, salary, salary * 12 AS annual FROM employees
) AS annual_data
WHERE annual > 900000;
```

## Subqueries in SELECT

```sql
SELECT 
    name,
    salary,
    (SELECT AVG(salary) FROM employees) AS avg_salary,
    salary - (SELECT AVG(salary) FROM employees) AS diff_from_avg
FROM employees;
```

## EXISTS Operator

```sql
-- Find employees with projects
SELECT name
FROM employees e
WHERE EXISTS (
    SELECT 1 FROM projects p WHERE p.employee_id = e.id
);

-- Find employees without projects
SELECT name
FROM employees e
WHERE NOT EXISTS (
    SELECT 1 FROM projects p WHERE p.employee_id = e.id
);
```

## CASE Expression

```sql
-- Simple CASE
SELECT 
    name,
    CASE department
        WHEN 'IT' THEN 'Information Technology'
        WHEN 'HR' THEN 'Human Resources'
        ELSE 'Other'
    END AS dept_full_name
FROM employees;

-- Searched CASE
SELECT 
    name,
    salary,
    CASE
        WHEN salary < 50000 THEN 'Junior'
        WHEN salary < 80000 THEN 'Mid-Level'
        WHEN salary < 120000 THEN 'Senior'
        ELSE 'Executive'
    END AS level
FROM employees;
```

## UNION

```sql
-- Combine results (remove duplicates)
SELECT name FROM employees WHERE department = 'IT'
UNION
SELECT name FROM employees WHERE salary > 100000;

-- Keep duplicates
SELECT name FROM employees WHERE department = 'IT'
UNION ALL
SELECT name FROM employees WHERE salary > 100000;
```

---

# Views and Indexes

## Creating Views

```sql
CREATE VIEW high_earners AS
SELECT id, name, salary, department
FROM employees
WHERE salary > 80000;

-- Use the view
SELECT * FROM high_earners;

-- Update view
ALTER VIEW high_earners AS
SELECT id, name, salary, department
FROM employees
WHERE salary > 100000;

-- Drop view
DROP VIEW high_earners;
```

## Indexes

### Creating Indexes

```sql
-- Single column index
CREATE INDEX idx_email ON employees(email);

-- Composite index
CREATE INDEX idx_dept_salary ON employees(department, salary);

-- Unique index
CREATE UNIQUE INDEX idx_ssn ON employees(social_security_number);

-- Full-text index (for text search)
CREATE FULLTEXT INDEX idx_description ON products(description);
```

### Using Indexes

```sql
-- These queries benefit from indexes
SELECT * FROM employees WHERE email = 'john@example.com';
SELECT * FROM employees WHERE department = 'IT' AND salary > 75000;
```

### Managing Indexes

```sql
-- View indexes
SHOW INDEX FROM employees;

-- Drop index
DROP INDEX idx_email ON employees;

-- Analyze table for optimization
ANALYZE TABLE employees;
```

---

# Transactions

## Basic Transactions

```sql
-- Start transaction
BEGIN;

-- Or use START TRANSACTION
START TRANSACTION;

-- Execute queries
UPDATE employees SET salary = salary + 5000 WHERE id = 1;
UPDATE employees SET salary = salary - 5000 WHERE id = 2;

-- Commit changes
COMMIT;

-- Or rollback
ROLLBACK;
```

## Savepoints

```sql
BEGIN;

INSERT INTO employees (name, email, salary) VALUES ('John', 'john@ex.com', 75000);
SAVEPOINT sp1;

UPDATE employees SET salary = 80000 WHERE id = 1;
SAVEPOINT sp2;

DELETE FROM employees WHERE id = 5;

-- Rollback to savepoint
ROLLBACK TO sp1;

COMMIT;
```

## Transaction Isolation Levels

```sql
-- Set isolation level
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

-- View current level
SELECT @@transaction_isolation;
```

---

# Stored Procedures and Functions

## Creating Stored Procedures

```sql
CREATE PROCEDURE GetEmployeesByDept(IN dept_name VARCHAR(100))
BEGIN
    SELECT * FROM employees
    WHERE department = dept_name;
END;

-- Call procedure
CALL GetEmployeesByDept('IT');
```

### Procedure with Parameters

```sql
CREATE PROCEDURE UpdateSalary(IN emp_id INT, IN new_salary DECIMAL(10,2))
BEGIN
    UPDATE employees
    SET salary = new_salary
    WHERE id = emp_id;
END;

-- Call with parameters
CALL UpdateSalary(1, 85000);
```

### Procedure with OUT Parameters

```sql
CREATE PROCEDURE GetAvgSalary(IN dept_name VARCHAR(100), OUT avg_sal DECIMAL(10,2))
BEGIN
    SELECT AVG(salary) INTO avg_sal
    FROM employees
    WHERE department = dept_name;
END;

-- Call and get result
CALL GetAvgSalary('IT', @avg_salary);
SELECT @avg_salary;
```

## Creating Functions

```sql
CREATE FUNCTION GetBonus(salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
READS SQL DATA
BEGIN
    DECLARE bonus DECIMAL(10,2);
    IF salary > 100000 THEN
        SET bonus = salary * 0.10;
    ELSEIF salary > 80000 THEN
        SET bonus = salary * 0.05;
    ELSE
        SET bonus = salary * 0.02;
    END IF;
    RETURN bonus;
END;

-- Use function
SELECT name, salary, GetBonus(salary) AS bonus FROM employees;
```

---

# SQL Optimization

## Query Optimization Tips

### 1. Use Specific Columns

```sql
-- Bad
SELECT * FROM employees;

-- Good
SELECT id, name, email FROM employees;
```

### 2. Use Indexes

```sql
-- Create indexes on frequently searched columns
CREATE INDEX idx_email ON employees(email);
CREATE INDEX idx_dept ON employees(department);
```

### 3. EXPLAIN Analysis

```sql
-- Analyze query execution
EXPLAIN SELECT * FROM employees WHERE email = 'john@example.com';

-- Detailed analysis
EXPLAIN EXTENDED SELECT * FROM employees WHERE department = 'IT';
```

### 4. Avoid Functions in WHERE

```sql
-- Bad (doesn't use index)
SELECT * FROM employees WHERE YEAR(hire_date) = 2023;

-- Good (uses index)
SELECT * FROM employees 
WHERE hire_date BETWEEN '2023-01-01' AND '2023-12-31';
```

### 5. Denormalization for Performance

```sql
-- Sometimes duplicating data for speed is justified
CREATE TABLE employee_summary AS
SELECT 
    e.id,
    e.name,
    COUNT(p.id) AS project_count,
    AVG(e.salary) AS avg_salary
FROM employees e
LEFT JOIN projects p ON e.id = p.employee_id
GROUP BY e.id, e.name;
```

### 6. Batch Operations

```sql
-- Bad (multiple individual inserts)
INSERT INTO employees VALUES (1, 'John', 75000);
INSERT INTO employees VALUES (2, 'Jane', 82000);

-- Good (single batch insert)
INSERT INTO employees VALUES 
(1, 'John', 75000),
(2, 'Jane', 82000);
```

---

# Practice Problems

## Problem 1: Employee Database

### Schema

```sql
CREATE TABLE departments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL UNIQUE,
    budget DECIMAL(12,2)
);

CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    salary DECIMAL(10,2),
    dept_id INT,
    hire_date DATE,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);

CREATE TABLE projects (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);

CREATE TABLE employee_projects (
    employee_id INT,
    project_id INT,
    hours INT,
    PRIMARY KEY (employee_id, project_id),
    FOREIGN KEY (employee_id) REFERENCES employees(id),
    FOREIGN KEY (project_id) REFERENCES projects(id)
);
```

### Sample Queries

**Q1: Total salary by department**
```sql
SELECT d.name, SUM(e.salary) AS total_salary
FROM departments d
LEFT JOIN employees e ON d.id = e.dept_id
GROUP BY d.id, d.name;
```

**Q2: Employees earning above average**
```sql
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees)
ORDER BY salary DESC;
```

**Q3: Department with highest average salary**
```sql
SELECT d.name, AVG(e.salary) AS avg_salary
FROM departments d
JOIN employees e ON d.id = e.dept_id
GROUP BY d.id, d.name
ORDER BY avg_salary DESC
LIMIT 1;
```

**Q4: Employees on multiple projects**
```sql
SELECT e.name, COUNT(p.id) AS project_count
FROM employees e
JOIN employee_projects p ON e.id = p.employee_id
GROUP BY e.id, e.name
HAVING COUNT(p.id) > 1;
```

**Q5: Departments without employees**
```sql
SELECT d.name
FROM departments d
WHERE NOT EXISTS (
    SELECT 1 FROM employees e WHERE e.dept_id = d.id
);
```

---

## Problem 2: E-Commerce Database

### Schema

```sql
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    country VARCHAR(50)
);

CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    price DECIMAL(8,2),
    category VARCHAR(50),
    stock INT
);

CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    order_date DATE,
    total DECIMAL(10,2),
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);

CREATE TABLE order_items (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(8,2),
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

### Sample Queries

**Q1: Total sales by product**
```sql
SELECT p.name, SUM(oi.quantity) AS units_sold, SUM(oi.quantity * oi.price) AS total_sales
FROM products p
LEFT JOIN order_items oi ON p.id = oi.product_id
GROUP BY p.id, p.name
ORDER BY total_sales DESC;
```

**Q2: Top 5 customers by spending**
```sql
SELECT c.name, SUM(o.total) AS total_spent
FROM customers c
JOIN orders o ON c.id = o.customer_id
GROUP BY c.id, c.name
ORDER BY total_spent DESC
LIMIT 5;
```

**Q3: Products never ordered**
```sql
SELECT name FROM products
WHERE id NOT IN (SELECT DISTINCT product_id FROM order_items);
```

**Q4: Average order value by country**
```sql
SELECT c.country, AVG(o.total) AS avg_order_value
FROM customers c
JOIN orders o ON c.id = o.customer_id
GROUP BY c.country
ORDER BY avg_order_value DESC;
```

**Q5: Customers who haven't ordered**
```sql
SELECT name FROM customers
WHERE id NOT IN (SELECT DISTINCT customer_id FROM orders);
```

---

## Problem 3: Student Management System

### Schema

```sql
CREATE TABLE courses (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    credits INT,
    instructor VARCHAR(100)
);

CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    enrollment_date DATE
);

CREATE TABLE enrollments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    course_id INT,
    marks INT,
    grade VARCHAR(2),
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id) REFERENCES courses(id)
);
```

### Sample Queries

**Q1: Average marks per course**
```sql
SELECT c.name, AVG(e.marks) AS avg_marks
FROM courses c
JOIN enrollments e ON c.id = e.course_id
GROUP BY c.id, c.name
ORDER BY avg_marks DESC;
```

**Q2: Student with highest GPA**
```sql
SELECT s.name, AVG(e.marks) AS avg_marks
FROM students s
JOIN enrollments e ON s.id = e.student_id
GROUP BY s.id, s.name
ORDER BY avg_marks DESC
LIMIT 1;
```

**Q3: Failing grades (marks < 40)**
```sql
SELECT DISTINCT s.name
FROM students s
JOIN enrollments e ON s.id = e.student_id
WHERE e.marks < 40;
```

**Q4: Course with most students**
```sql
SELECT c.name, COUNT(e.student_id) AS student_count
FROM courses c
JOIN enrollments e ON c.id = e.course_id
GROUP BY c.id, c.name
ORDER BY student_count DESC
LIMIT 1;
```

---

## Problem 4: Hospital Management

### Schema

```sql
CREATE TABLE doctors (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    specialty VARCHAR(100),
    salary DECIMAL(10,2)
);

CREATE TABLE patients (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    age INT,
    disease VARCHAR(100)
);

CREATE TABLE appointments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    patient_id INT,
    doctor_id INT,
    appointment_date DATE,
    status VARCHAR(20),
    FOREIGN KEY (patient_id) REFERENCES patients(id),
    FOREIGN KEY (doctor_id) REFERENCES doctors(id)
);

CREATE TABLE prescriptions (
    id INT PRIMARY KEY AUTO_INCREMENT,
    appointment_id INT,
    medication VARCHAR(100),
    dosage VARCHAR(50),
    FOREIGN KEY (appointment_id) REFERENCES appointments(id)
);
```

### Sample Queries

**Q1: Appointments per doctor**
```sql
SELECT d.name, COUNT(a.id) AS appointment_count
FROM doctors d
LEFT JOIN appointments a ON d.id = a.doctor_id
GROUP BY d.id, d.name
ORDER BY appointment_count DESC;
```

**Q2: Most common diseases**
```sql
SELECT disease, COUNT(*) AS count
FROM patients
GROUP BY disease
ORDER BY count DESC;
```

**Q3: Doctors with highest patient load**
```sql
SELECT d.name, COUNT(DISTINCT a.patient_id) AS unique_patients
FROM doctors d
JOIN appointments a ON d.id = a.doctor_id
GROUP BY d.id, d.name
ORDER BY unique_patients DESC;
```

**Q4: Medications prescribed by specialty**
```sql
SELECT d.specialty, p.medication, COUNT(*) AS count
FROM doctors d
JOIN appointments a ON d.id = a.doctor_id
JOIN prescriptions p ON a.id = p.appointment_id
GROUP BY d.specialty, p.medication
ORDER BY d.specialty, count DESC;
```

---

## Problem 5: Library Management

### Schema

```sql
CREATE TABLE members (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    email VARCHAR(100),
    join_date DATE
);

CREATE TABLE books (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100),
    author VARCHAR(100),
    isbn VARCHAR(13) UNIQUE,
    total_copies INT,
    available_copies INT
);

CREATE TABLE borrowings (
    id INT PRIMARY KEY AUTO_INCREMENT,
    member_id INT,
    book_id INT,
    borrow_date DATE,
    return_date DATE,
    FOREIGN KEY (member_id) REFERENCES members(id),
    FOREIGN KEY (book_id) REFERENCES books(id)
);
```

### Sample Queries

**Q1: Most borrowed books**
```sql
SELECT b.title, COUNT(br.id) AS borrow_count
FROM books b
JOIN borrowings br ON b.id = br.book_id
GROUP BY b.id, b.title
ORDER BY borrow_count DESC
LIMIT 10;
```

**Q2: Currently borrowed books (not returned)**
```sql
SELECT m.name, b.title, br.borrow_date
FROM borrowings br
JOIN members m ON br.member_id = m.id
JOIN books b ON br.book_id = b.id
WHERE br.return_date IS NULL
ORDER BY br.borrow_date;
```

**Q3: Member borrowing history**
```sql
SELECT m.name, COUNT(br.id) AS total_borrows
FROM members m
LEFT JOIN borrowings br ON m.id = br.member_id
GROUP BY m.id, m.name
ORDER BY total_borrows DESC;
```

**Q4: Books available for borrowing**
```sql
SELECT title, author, available_copies
FROM books
WHERE available_copies > 0
ORDER BY available_copies DESC;
```

---

**Last Updated:** May 3, 2026

This comprehensive SQL guide covers everything from fundamentals to advanced optimization techniques with practical examples and problems.

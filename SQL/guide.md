# SQL Complete Guide

## ðŸ“Š SQL Basics

### What is SQL?
**SQL (Structured Query Language)** is a standard language for:
- Creating and managing databases
- Inserting, updating, and deleting data
- Querying data with filters and aggregations
- Controlling data access and security

### Data Types

| Type | Description | Examples |
|------|-------------|----------|
| **INT, BIGINT, SMALLINT** | Integer numbers | 42, -100, 9999 |
| **DECIMAL, FLOAT, DOUBLE** | Decimal numbers | 3.14, 99.99 |
| **VARCHAR(n)** | Variable-length string | 'John', 'Description' |
| **CHAR(n)** | Fixed-length string | 'M' (gender) |
| **TEXT** | Large text | Long articles, comments |
| **DATE** | Date | 2024-05-03 |
| **TIME** | Time | 14:30:00 |
| **DATETIME** | Date and time | 2024-05-03 14:30:00 |
| **BOOLEAN** | True/False | TRUE, FALSE |

### Database and Table Creation

```sql
-- Create database
CREATE DATABASE company_db;
USE company_db;

-- Create table
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    designation VARCHAR(50),
    salary DECIMAL(10, 2),
    department VARCHAR(50),
    hire_date DATE,
    is_active BOOLEAN DEFAULT TRUE
);

-- Create table with foreign key
CREATE TABLE projects (
    project_id INT PRIMARY KEY AUTO_INCREMENT,
    project_name VARCHAR(100),
    employee_id INT,
    start_date DATE,
    FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```

---

## ðŸ“ CRUD Operations

### CREATE (INSERT)

```sql
-- Insert single record
INSERT INTO employees (name, designation, salary, department, hire_date)
VALUES ('John Doe', 'Developer', 50000, 'IT', '2020-01-15');

-- Insert multiple records
INSERT INTO employees (name, designation, salary, department)
VALUES 
    ('Alice Smith', 'Manager', 60000, 'Sales'),
    ('Bob Johnson', 'Analyst', 45000, 'Finance'),
    ('Carol White', 'Designer', 48000, 'Design');

-- Insert with default values
INSERT INTO employees (name, designation)
VALUES ('David Brown', 'Intern');
```

### READ (SELECT)

```sql
-- Select all columns
SELECT * FROM employees;

-- Select specific columns
SELECT name, designation, salary FROM employees;

-- With WHERE clause
SELECT * FROM employees WHERE salary > 50000;
SELECT * FROM employees WHERE department = 'IT';
SELECT * FROM employees WHERE salary BETWEEN 40000 AND 60000;

-- Multiple conditions
SELECT * FROM employees 
WHERE department = 'IT' AND salary > 50000;

SELECT * FROM employees 
WHERE department = 'IT' OR department = 'HR';

-- LIKE pattern matching
SELECT * FROM employees WHERE name LIKE 'John%';  -- Starts with John
SELECT * FROM employees WHERE name LIKE '%Smith%'; -- Contains Smith
SELECT * FROM employees WHERE name LIKE '_ar_';    -- 4 chars, has 'ar'

-- ORDER BY
SELECT * FROM employees ORDER BY salary DESC;
SELECT * FROM employees ORDER BY name ASC;
SELECT * FROM employees ORDER BY department, salary DESC;

-- LIMIT
SELECT * FROM employees LIMIT 5;      -- First 5 records
SELECT * FROM employees LIMIT 10 OFFSET 5;  -- Skip 5, get 10

-- DISTINCT
SELECT DISTINCT department FROM employees;

-- IN clause
SELECT * FROM employees WHERE id IN (1, 3, 5);

-- IS NULL / IS NOT NULL
SELECT * FROM employees WHERE department IS NULL;
SELECT * FROM employees WHERE department IS NOT NULL;
```

### UPDATE

```sql
-- Update single record
UPDATE employees 
SET salary = 55000 
WHERE id = 1;

-- Update multiple columns
UPDATE employees 
SET salary = 65000, designation = 'Senior Developer' 
WHERE name = 'John Doe';

-- Update multiple records
UPDATE employees 
SET salary = salary * 1.1 
WHERE department = 'IT';

-- Conditional update
UPDATE employees 
SET is_active = FALSE 
WHERE hire_date < '2015-01-01';
```

### DELETE

```sql
-- Delete specific record
DELETE FROM employees WHERE id = 5;

-- Delete multiple records
DELETE FROM employees WHERE salary < 40000;

-- Delete all records (be careful!)
DELETE FROM employees;

-- TRUNCATE (faster, cannot rollback)
TRUNCATE TABLE employees;
```

---

## ðŸ” Advanced SELECT

### Aggregate Functions

```sql
-- COUNT
SELECT COUNT(*) FROM employees;              -- Total records
SELECT COUNT(department) FROM employees;     -- Non-null departments

-- SUM
SELECT SUM(salary) FROM employees;
SELECT SUM(salary) FROM employees WHERE department = 'IT';

-- AVG
SELECT AVG(salary) FROM employees;
SELECT AVG(salary) FROM employees WHERE department = 'Sales';

-- MIN, MAX
SELECT MIN(salary), MAX(salary) FROM employees;
SELECT MIN(hire_date) FROM employees;

-- Combining aggregates
SELECT 
    COUNT(*) as total_employees,
    AVG(salary) as avg_salary,
    MIN(salary) as min_salary,
    MAX(salary) as max_salary
FROM employees;
```

### GROUP BY and HAVING

```sql
-- Group by department
SELECT department, COUNT(*) as emp_count
FROM employees
GROUP BY department;

-- With aggregate
SELECT department, AVG(salary) as avg_salary
FROM employees
GROUP BY department;

-- HAVING clause (filter groups)
SELECT department, AVG(salary) as avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;

-- Multiple grouping
SELECT department, designation, COUNT(*) as count
FROM employees
GROUP BY department, designation;

-- Complex example
SELECT 
    department,
    COUNT(*) as emp_count,
    AVG(salary) as avg_salary,
    MAX(salary) as max_salary
FROM employees
WHERE is_active = TRUE
GROUP BY department
HAVING COUNT(*) > 1
ORDER BY avg_salary DESC;
```

### Joins

```sql
-- INNER JOIN (only matching records)
SELECT e.name, e.designation, p.project_name
FROM employees e
INNER JOIN projects p ON e.id = p.employee_id;

-- LEFT JOIN (all from left, matching from right)
SELECT e.name, p.project_name
FROM employees e
LEFT JOIN projects p ON e.id = p.employee_id;

-- RIGHT JOIN (all from right, matching from left)
SELECT e.name, p.project_name
FROM employees e
RIGHT JOIN projects p ON e.id = p.employee_id;

-- FULL OUTER JOIN (all from both)
SELECT e.name, p.project_name
FROM employees e
FULL OUTER JOIN projects p ON e.id = p.employee_id;

-- CROSS JOIN (Cartesian product)
SELECT e.name, p.project_name
FROM employees e
CROSS JOIN projects p;

-- Self join
SELECT e1.name, e2.name as manager
FROM employees e1
JOIN employees e2 ON e1.manager_id = e2.id;
```

### Subqueries

```sql
-- Subquery in WHERE
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

-- Subquery in FROM
SELECT * FROM (
    SELECT name, salary * 12 as annual_salary
    FROM employees
) AS annual_data
WHERE annual_salary > 600000;

-- Subquery with IN
SELECT name
FROM employees
WHERE department IN (
    SELECT department FROM employees WHERE salary > 60000
);

-- EXISTS
SELECT name
FROM employees e
WHERE EXISTS (
    SELECT 1 FROM projects p WHERE p.employee_id = e.id
);
```

### UNION

```sql
-- UNION (removes duplicates)
SELECT name FROM employees WHERE department = 'IT'
UNION
SELECT name FROM employees WHERE salary > 60000;

-- UNION ALL (keeps duplicates)
SELECT name FROM employees WHERE department = 'IT'
UNION ALL
SELECT name FROM employees WHERE salary > 60000;
```

---

## ðŸ” Data Integrity and Constraints

```sql
-- PRIMARY KEY
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100)
);

-- FOREIGN KEY
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    order_date DATE,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- UNIQUE constraint
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    sku VARCHAR(20) UNIQUE,
    name VARCHAR(100) NOT NULL
);

-- CHECK constraint
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age >= 18),
    salary DECIMAL(10, 2) CHECK (salary > 0)
);

-- DEFAULT values
CREATE TABLE logs (
    id INT PRIMARY KEY AUTO_INCREMENT,
    message VARCHAR(255),
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

## ðŸ”¨ Useful SQL Functions

### String Functions

```sql
SELECT UPPER(name) FROM employees;           -- Uppercase
SELECT LOWER(name) FROM employees;           -- Lowercase
SELECT LENGTH(name) FROM employees;          -- String length
SELECT SUBSTRING(name, 1, 5) FROM employees; -- Extract substring
SELECT CONCAT(name, ' - ', designation) FROM employees;
SELECT TRIM(name) FROM employees;            -- Remove spaces
SELECT REPLACE(name, 'John', 'Jon') FROM employees;
```

### Date Functions

```sql
SELECT CURDATE();                            -- Current date
SELECT CURTIME();                            -- Current time
SELECT NOW();                                -- Current date and time
SELECT DATE_ADD(hire_date, INTERVAL 1 YEAR) FROM employees;
SELECT DATEDIFF(CURDATE(), hire_date) FROM employees;
SELECT YEAR(hire_date), MONTH(hire_date), DAY(hire_date) FROM employees;
```

### Mathematical Functions

```sql
SELECT ABS(-10);                             -- Absolute value
SELECT ROUND(3.14159, 2);                    -- Round to 2 decimals
SELECT CEIL(3.2);                            -- Ceiling
SELECT FLOOR(3.8);                           -- Floor
SELECT POWER(2, 3);                          -- 2^3 = 8
SELECT SQRT(16);                             -- Square root = 4
```

---

## ðŸ“š Views and Indexes

### Views

```sql
-- Create view
CREATE VIEW high_earners AS
SELECT name, salary, department
FROM employees
WHERE salary > 60000;

-- Query view
SELECT * FROM high_earners;

-- Drop view
DROP VIEW high_earners;
```

### Indexes

```sql
-- Create index
CREATE INDEX idx_name ON employees(name);
CREATE INDEX idx_dept_salary ON employees(department, salary);

-- Drop index
DROP INDEX idx_name ON employees;
```

---

## ðŸ”„ Transactions

```sql
-- Basic transaction
BEGIN;
UPDATE employees SET salary = salary + 5000 WHERE id = 1;
UPDATE employees SET salary = salary - 5000 WHERE id = 2;
COMMIT;

-- Rollback example
BEGIN;
DELETE FROM employees WHERE id = 100;
ROLLBACK;  -- Undo the delete

-- SAVEPOINT
BEGIN;
INSERT INTO employees VALUES (10, 'John', 'Developer', 50000);
SAVEPOINT sp1;
UPDATE employees SET salary = 55000 WHERE id = 10;
ROLLBACK TO sp1;  -- Only rollback to savepoint
COMMIT;
```

---


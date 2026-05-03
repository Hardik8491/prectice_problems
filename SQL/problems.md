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


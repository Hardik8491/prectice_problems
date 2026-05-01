# 🧑‍💼 Employee Overtime Bonus System

## 📌 Problem Statement

You are required to design a system to manage employee overtime and calculate bonuses based on eligibility.

### 📝 Requirements:

1. Create a class `Employee` with the following attributes:
   - `name` → Employee name
   - `designation` → Job role
   - `salary` → Monthly salary (integer)
   - `overtimeStatus` → Boolean (initially False)
   - `overtimeContribute` → Dictionary storing month and overtime days

2. Create a class `Organization` with:
   - A list of employees (`emp_list`)

3. Implement the following methods:

   ### 🔹 `checkEligibility(m)`
   - Calculate total overtime days for each employee
   - If total overtime > `m` (threshold), mark employee as eligible:
     ```
     overtimeStatus = True
     ```

   ### 🔹 `bonus(k)`
   - Calculate total salary of eligible employees
   - Multiply by bonus factor `k`
   - Print the result

---

## 📥 Input Format

1. Number of employees `n`
2. For each employee:
   - Name
   - Designation
   - Salary
   - Number of months
   - For each month:
     - Month name
     - Overtime days
3. Overtime threshold `m`
4. Bonus multiplier `k`

---

## 📤 Output

- Print total bonus amount

---

## ✅ Solution Code

```python
class Employee:
    def __init__(self, name, designation, salary, overtimeStatus, overtimeContribute):
        self.name = name
        self.designation = designation
        self.salary = salary
        self.overtimeStatus = overtimeStatus
        self.overtimeContribute = overtimeContribute


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


# MAIN
n = int(input("Enter number of employees: "))
emp_list = []

for _ in range(n):
    name = input("Name: ")
    designation = input("Designation: ")
    salary = int(input("Salary: "))
    months_size = int(input("Months count: "))

    overtimeContribute = {}

    for _ in range(months_size):
        month = input("Month: ")
        days = int(input("Overtime days: "))
        overtimeContribute[month] = days

    emp = Employee(name, designation, salary, False, overtimeContribute)
    emp_list.append(emp)

m = int(input("Enter overtime threshold: "))
k = int(input("Enter bonus multiplier: "))

org = Organization(emp_list)
org.checkEligibility(m)
org.bonus(k)
````

---

## 🧠 Key Concepts Covered

* Object-Oriented Programming (OOP)
* Class and Object usage
* List of objects
* Dictionary handling
* Aggregation logic (`sum`)
* Conditional filtering
* Real-world modeling problem

---

## 💡 Example

### Input:

```
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
```

### Output:

```
100000
```

---

## 🚀 Notes

* Only employees with overtime > threshold are eligible
* Bonus = (sum of eligible salaries) × multiplier

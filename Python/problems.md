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



---

# TCS Practice Questions (Converted from Files)

## Practice Problem 1: 10thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Employee` class with attributes: `employee_name,designation,salary,overTimeContribution,overTimeStatus`.
   - Implement methods: `checkElegibility(m)`
2. Create `Organization` class with attributes: `employee_list`.
   - Implement methods: `checkElegibility(m)`

### Input / Output Examples:
```
Input:
4
Hello Good Morning
abcd123Fghy
India
progoti.c

Output:
Valid:  2
Invalid:  2

Input:
5
Sunita
Faculty
23000
2
jan
4
March
6
Arun
Admin
30000
3
Feb
4
March
12
June
10
Dipak
Admin
25000
3
Jan
12
July
5
Aug
3
Balen
HR
12000
3
Jan
12
July
5
Aug
3
Tarun
HR
78000
3
Jan
12
July
5
Aug
3
18
100

```

### Solution Code:
```python
'''n = int(input())
l = []
for i in range(n):
    l.append(input())
for i in range(len(l)):
    count1 = 0
    count2 = 0
    for j in l:
       
        if j.isidentifier() or (j.isspace()):
                count1 +=1
        else:
            count2 +=1
            # print("Invalid: ",j)

print("Valid: ",count1)
print("Invalid: ",count2)
'''
'''

Input:
4
Hello Good Morning
abcd123Fghy
India
progoti.c

Output:
Valid:  2
Invalid:  2

'''


# 35 Marks question [Python Assessment Test given in TCS Explore]

class Employee:
    def __init__(self,employee_name,designation,salary,overTimeContribution,overTimeStatus):
        self.employee_name = employee_name
        self.designation = designation
        self.salary = salary
        self.overTimeContribution = overTimeContribution
        self.overTimeStatus = overTimeStatus
        
class Organization:
    def __init__(self,employee_list):
        self.employee_list = employee_list
    def checkElegibility(self,m):
       for i in employee_list:
            s = sum(i.overTimeContribution.values())
            if s >m:
                i.overTimeStatus = True
            print(f"{i.employee_name} {i.overTimeStatus} {s}")
    def bonus(self,k):
        l4 = []
        for i in employee_list:
            if i.overTimeStatus == True:
                l4.append(sum(i.overTimeContribution.values()))
        total = sum(l4)
        tm = total*k
        if tm:
            return tm
        else:
            # print("0")
            return 0
n = int(input())
employee_list = []
for i in range(n):
    employee_name = input()
    designation = input()
    salary = int(input())
    overTimeStatus = False
    overTimeContribution = {}
    for i in range(int(input())):
        monthname = input()
        hours = int(input())
        overTimeContribution[monthname] = hours
    EmployeeObj = Employee(employee_name,designation,salary,overTimeContribution,overTimeStatus)
    employee_list.append(EmployeeObj)
m = int(input())
k = int(input())
Organizationobj = Organization(employee_list)
ans = Organizationobj.checkElegibility(m)
# print(ans)
ans2 = Organizationobj.bonus(k)
if ans2:
    print(ans2)
else:
    print(ans2)




        
"""

Input:
5
Sunita
Faculty
23000
2
jan
4
March
6
Arun
Admin
30000
3
Feb
4
March
12
June
10
Dipak
Admin
25000
3
Jan
12
July
5
Aug
3
Balen
HR
12000
3
Jan
12
July
5
Aug
3
Tarun
HR
78000
3
Jan
12
July
5
Aug
3
18
100

"""
```

---

## Practice Problem 2: 11thJune

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Store` class with attributes: `username,list1`.
   - Implement methods: `findSpiciestPepper()`, `SortPepperByprice()`

### Input / Output Examples:
```
Input:
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

Output:

Spiciest Pepper :
nupur with green of SHI : 42350

Sorted Pepper by price :
corona
32.0
greenchilli
43.0
nupur
90.0

Input:
3
32
12
43 
mayank
54
2
33
nupur
56
1
21
xyz

Output:
Max players by fights
mayank
sort players by rank
32
54
56

```

### Solution Code:
```python
class Pepper :
    def __init__(self,name,color,SHI,price):
        self.name = name
        self.color = color
        self.SHI = SHI
        self.price = price
class Store:
    def __init__(self,username,list1):
        self.username = username
        self.list1 = list1
    def findSpiciestPepper(self):
        l1 = []
        for i in list1:
            l1.append(i.SHI)
        m = max(l1)
        for j in list1:
            if j.SHI >= 14000 and j.SHI == m:
                print(f"{j.name} with {j.color} of SHI : {j.SHI}")
                # print(j.name)
                # print(j.color)
                # print(j.SHI)
                # print(j.price)
        else:
            return None


    def SortPepperByprice(self):
        l2 = sorted(list1 , key = lambda  x : x.price , reverse = False)
        for i in l2:
            print(i.name)
            print(i.price)
        else:
            return None

n = int(input())
list1 = []
for i in range(n):
    name = input()
    color = input()
    SHI = int(input())
    price = float(input())
    objpepper = Pepper(name,color,SHI,price)
    list1.append(objpepper)
# username = input()
objStore = Store('Mayank',list1)
print("\n")
print("Spiciest Pepper :")
ans1 = objStore.findSpiciestPepper()
print("\n")
print("Sorted Pepper by price :")
ans2 = objStore.SortPepperByprice()
    



'''
Input:
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

Output:

Spiciest Pepper :
nupur with green of SHI : 42350

Sorted Pepper by price :
corona
32.0
greenchilli
43.0
nupur
90.0

'''


# class wweplayer:
#     def __init__(self,rank,fights,weight,name):
#         self.rank = rank
#         self.fights = fights
#         self.weight = weight
#         self.name = name
# class wweLeague:
#     def __init__(self,leaguename , list1):
#         self.leaguename = leaguename
#         self.list1 = list1
#     def findmaxplayerbyfights(self):
#         l1 = []
#         for i in list1:
#             l1.append(i.fights)
#         m = max(l1)
#         for i in list1:
#             if i.fights == m:
#                 print(i.name)
#         # # l1 = []
#         # for i in list1:
#         #     s = sorted(list1, key=lambda x:x.fights ,reverse=True)
#         # if s == []:
#         #     return None
#         # else:
#         #     for i in s:
#         #         print(i.rank)
#         #         print(i.fights)
#         #         print(i.weight)
#         #         print(i.name)

#         # s = sorted(self.list1, key=lambda x: x.fights, reverse=True)
#         # if not s:
#         #     return None
#         # else:
#         #     for i in s:
#         #         print(i.rank)
#         #         print(i.fights)
#         #         print(i.weight)
#         #         print(i.name)

#         # max_fights = 0
#         # max_player = None
#         # for i in self.list1:
#         #     if i.fights > max_fights:
#         #         max_fights = i.fights
#         #         max_player = i

#         # if max_player is None:
#         #     return None
#         # else:
#         #     print("Player with the maximum number of fights:")
#         #     print(f"Rank: {max_player.rank}")
#         #     print(f"Fights: {max_player.fights}")
#         #     print(f"Weight: {max_player.weight}")
#         #     print(f"Name: {max_player.name}")
            
#     def sortPlayerbyRank(self):
#         # sorted in assending order 
#         l3 = []
#         for i in self.list1:
#             l3.append(i.rank)
#         # x = l3.sort()
#         l3.sort()
#         for i in l3:
#             print(i)

#         # sorted in decending order
# #         sorted_players = sorted(self.list1, key=lambda x: x.rank, reverse=True)
# #         for player in sorted_players:
# #             print(f"Rank: {player.rank}")
# #             print(f"Fights: {player.fights}")
# #             print(f"Weight: {player.weight}")
# #             print(f"Name: {player.name}")
            
# n = int(input())
# list1 = []
# for i in range(n):
#     rank = int(input())
#     fights = int(input())
#     weight = int(input())
#     name = input()
#     obj1 = wweplayer(rank,fights,weight,name)
#     list1.append(obj1)
# obj2 = wweLeague("Mayank's League",list1)
# print("Max players by fights")
# ans1 = obj2.findmaxplayerbyfights()
# print("sort players by rank")
# ans2 = obj2.sortPlayerbyRank()


'''   
Input:
3
32
12
43 
mayank
54
2
33
nupur
56
1
21
xyz

Output:
Max players by fights
mayank
sort players by rank
32
54
56

'''
```

---

## Practice Problem 3: 11thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
4          
Hello Good Morning
abcd123Fghy
India
progoti.c
India

Output:
Position of the searched string is:2

```

### Solution Code:
```python
def indexcheck(m):
    for j in range(len(l)):
        if l[j].lower() ==m.lower():
            return j

n = int(input())
l = []
for i in range(n):
    l.append(input())

m = input()
ans = indexcheck(m)
if ans:
    print(f"Position of the searched string is:{ans}")    
else:
    print("Not found")



'''
Input:
4          
Hello Good Morning
abcd123Fghy
India
progoti.c
India

Output:
Position of the searched string is:2

'''





# string = input()
# n = int(input())

# if n <= 0:
#     print("Error: N should be greater than 0.")
# else:
#     middle = len(string) // 2
#     start = middle - n // 2
#     end = start + n
#     print(string[start:end] if end <= len(string) else string[start:])





'''

The code first prompts the user to enter a string and an integer 'n'.

It then checks whether 'n' is greater than 0. If 'n' is less than or equal to 0, it prints an error message and exits the program.

If 'n' is greater than 0, the code calculates the middle index of the string using the formula: middle = len(string) // 2. This formula calculates the floor division of the length of the string by 2, which gives the index of the middle character in the string.

The code then calculates the starting index for the 'n' characters using the formula: start = middle - n // 2. This formula calculates the floor division of 'n' by 2 and subtracts it from the middle index, which gives the index of the first character to be included in the substring.

The code then calculates the ending index for the 'n' characters using the formula: end = start + n. This formula adds 'n' to the starting index, which gives the index of the last character to be included in the substring.

Finally, the code prints the substring starting from the calculated starting index and up to the calculated ending index, or up to the end of the string if the requested characters are not available.

'''
```

---

## Practice Problem 4: 12thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
Hyper12345Lower100

Output:
['HyperLower',12345100]

Input:
arr = [1,2,2,1,1,3]

Output:
True

Output:
20

```

### Solution Code:
```python
# Question 1

'''

Input:
Hyper12345Lower100

Output:
['HyperLower',12345100]

'''
'''
strng = input()

final = []
alpha = ''.join(i for i in strng if i.isalpha())
num = ''.join(i for i in strng if i.isdigit())
if len(alpha)!=0:
    final.append(alpha)
if len(num)!=0:
    final.append(int(num))
print(final)

'''

# Question 2

'''
Input:
arr = [1,2,2,1,1,3]

Output:
True

'''

'''arr = [1,2,2,1,1,3]
dic = {}
l1 = []
for i in arr:
    if i in dic:
        dic[i] += 1
    else:
        dic[i] =1
for k ,v in dic.items():
    l1.append(v)
print(len(set(l1))==len(l1))
        '''

# Question 3 

# nums = [6,4,5,1]
# l1 = []
# for i in range(len(nums)):
#     # print(i)
#     for j in range(i+1,len(nums)):
#         # print("j = ",j)
#         l1.append((nums[i]-1)*(nums[j]-1))
# print(max(l1))


# or 


nums = [6,4,5,1]
l = len(nums)
for i in nums:
    nums.sort()
    l1 = ((nums[l-1]-1)*(nums[l-2]-1))
print(l1)

'''

Output:
20

'''
```

---

## Practice Problem 5: 13thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Output:
Let's take LeetCode Contest
s ' t e L e k a t e d o C t e e L t s e t n o C

Output:
Let's take LeetCode contest
s'teL ekat edoCteeL tsetnoc
8

```

### Solution Code:
```python
# Wrong approach for this problem

'''
s = "Let's take LeetCode Contest"
print(s)

for i in s:
    l = s.split()
#print(l)
x = len(l)
#print(x)
m = []
for i in range(x):
    for j in l:
        lx =[]
        for k in j:
            lx.append(k)

        lx.reverse()

        m += lx
    #print(m)
    final = " ".join(m)

    print(final)

    break
 '''   

'''

Output:
Let's take LeetCode Contest
s ' t e L e k a t e d o C t e e L t s e t n o C

'''


# right approach for this problem 



s = "Let's take LeetCode contest"
print(s)
l = s.split()
l1 = []
for i in l:
    l1.append(i[::-1])
ss = ' '.join(l1)
print(ss)
l.sort()
print(len(l[0]))



'''

Output:
Let's take LeetCode contest
s'teL ekat edoCteeL tsetnoc
8

'''
```

---

## Practice Problem 6: 14thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
A quick brown fox jumps over the lazy dog

Output:
YES

Input:
1 2 3
4 5 6
7 8 9

Output:
['1', '2', '3'] ['4', '5', '6'] ['7', '8', '9']
90 Degree Rotation
7 4 1
8 5 2
9 6 3
180 Degree Rotation
9 8 7
6 5 4
3 2 1

```

### Solution Code:
```python
# Python3 program to
# Check if the string is pangram

# Pangram string is a string which contains all the letters of English Alphabats in it where repeatation of words is allowed 
# for Exapmle "A quick brown fox jumps over the lazy dog" is a pangram string

def ispangram(str):
	alphabet = "abcdefghijklmnopqrstuvwxyz"
	for i in alphabet:
		if i not in str.lower():
			return False
	return True
# string = "A quick brown fox jumps over the lazy dog"
string = "abcdefghijklg"
if (ispangram(string))==True:
	print("Yes")
else:
	print("No")

'''s = "A quick brown fox jumps over the lazy dog"
s = "abcdefghijkl"
l1 = []
alphabat = "abcdefghijklmnopqrstuvwxyz"
for i in s:
    if i.isalpha()==True:
        l1.append(i)
print(l1)
f = ''.join(l1)
print(f)
for i in alphabat:
    if i not in f.lower():
        print("No")
    else:
        print("Yes")
    break
'''


# Another Approach for this question 


s = input().split()
j = ''.join(s)
# print(j)
l = []
for i in j:
    l.append(i.lower())
# print(l)
l1 = list(set(l))
# print(l1)
if len(l1) == 26:
    print("YES")
else:
    print("NO")

'''

Input:
A quick brown fox jumps over the lazy dog

Output:
YES

'''

"""
# 2D matrix rotation

l1 = input().split()
l2 = input().split()
l3 = input().split()
print(l1,l2,l3)
print("90 Degree Rotation")
for i in range(3):
    print(l3[i],l2[i],l1[i])
print("180 Degree Rotation")
for i in range(3):
    j = 0
    if i==0:
        print(l3[j+2],l3[j+1],l3[j])
    elif i==1:
        print(l2[j+2],l2[j+1],l2[j])
    else:
        print(l1[j+2],l1[j+1],l1[j])
	
	
"""

'''

Input:
1 2 3
4 5 6
7 8 9

Output:
['1', '2', '3'] ['4', '5', '6'] ['7', '8', '9']
90 Degree Rotation
7 4 1
8 5 2
9 6 3
180 Degree Rotation
9 8 7
6 5 4
3 2 1

'''
```

---

## Practice Problem 7: 14thMarch_nightoutPractice

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
4
Hello GoodMorning
abcd123Fghy
India
Progoti.c
India

Output:
The position of the searched string is:  2

Input:
3
malayalam
radar
nitish

Output:

```

### Solution Code:
```python
# Find the index of the given string in the list

'''n = int(input())
# print(n)
l = []
for i in range(n):
    l.append(input())
m = input()
print("The position of the searched string is: ",l.index(m))
'''

'''
Input:
4
Hello GoodMorning
abcd123Fghy
India
Progoti.c
India

Output:
The position of the searched string is:  2

'''

# Another Method for the same Problem
'''
n = int(input())
# print(n)
l = []
for i in range(n):
    l.append(input())
m = input()
for i in range(0,len(l)):
    if l[i].lower() == m.lower():
        print("The position of the searched string is: ",i)
'''


# Print All Palindrom Strings present in the list 

'''

n = int(input())
l =[]
for i in range(n):
    l.append(input())
for i in l:
    if i == i[::-1]:
        print(i)
        
'''



'''
Input:
3
malayalam
radar
nitish

Output:

'''


'''
def check(l):
    l1 = []
    for i in l:
        if i == i[::-1]:
            l1.append(i)
    return l1

n = int(input())
l =[]
for i in range(n):
    l.append(input())

if check(l):
    for i in check(l):
        print(i)
else:
    print("Not Found !")
'''

"""

Create a function count_words() which takes a string as input and creates a dictionary with a word in the string as a key and its value as the number of times the word is repeated in the string. It should return the dictionary.
eg: “hello hi hello world hello” 
dict={hello:3,hi:1,word:1}

Create another function max_accurance_word() which takes a string as input and returns the word which is occurring a maximum number of times in the string. Use the count_words function inside this function.

"""


# Code taken from WEB

def count_words(string):
    l=string.split()
    s=set(l)
    d={}
    for i in s:
        x=l.count(i)
        d[i]=x
    return d
def max_occurance(string):
    d=count_words(string)
    l1=[]
    for i in d.values():
        l1.append(i)
    max1=max(l1)
    for i in d.keys():
        if d[i]==max1:
            return i
string=input() 
print(max_occurance(string))
```

---

## Practice Problem 8: 15thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Icecream` class with attributes: `id,price,name,quantityInGms,category`.
   - Implement methods: `findMinimumIcecreambyprice_list(IcecreamList)`, `sortIcecreamByid()`
2. Create `IcecreamStore` class with attributes: `IcecreamList`.
   - Implement methods: `findMinimumIcecreambyprice_list(IcecreamList)`, `sortIcecreamByid()`

### Input / Output Examples:
```
Input:
02
01
10
vanila
200
indian
02
20
chocobar
300
italian

Output:
vanila
[1, 2]

```

### Solution Code:
```python
# Icecream Question to find minimum icecream by price and to return sorted list of id's of icecreams 

class Icecream:
    def __init__(self,id,price,name,quantityInGms,category):
        self.id = id
        self.price = price
        self.name = name
        self.qualityInGms = quantityInGms
        self.category = category

class IcecreamStore:
    def __init__(self,IcecreamList):
        # self.IcecreamStoreName = IcecreamStoreName
        self.IcecreamList = IcecreamList
    def findMinimumIcecreambyprice_list(self,IcecreamList):
        dic = {}
        for i in IcecreamList:
            dic[i.name] = i.price
        print(dic)
        m = min(dic.values())
        names=[]
        for k in dic:
            if(dic[k] == m):
                names.append(k)
        names.sort()
        if(len(names)>0):
            return names[0]
        else:
            return "no icecream found"

    def sortIcecreamByid(self):
       l = []
       flag = 0
       for i in IcecreamList:
           l.append(i.id)
           flag = 1
       l.sort()
       if flag ==0:
           return None
       else:
           return l

n = int(input())
IcecreamList = []
for i in range(n):
    id = int(input())
    price = int(input())
    name = input()
    quantityInGms = int(input())
    category = input()
    icecreamObj = Icecream(id,price,name,quantityInGms,category)
    IcecreamList.append(icecreamObj)

ans1 = IcecreamStore(IcecreamList)
print(ans1.findMinimumIcecreambyprice_list(IcecreamList))
print(ans1.sortIcecreamByid())

'''
Input:
02
01
10
vanila
200
indian
02
20
chocobar
300
italian

Output:
vanila
[1, 2]

'''
```

---

## Practice Problem 9: 15thMarch_nightoutPractice

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `CricketPlayer` class with attributes: `cplayerName , cplayedCountry , cplayerAge,cpCountryFrom`.
   - Implement methods: `countPlayers(country)`, `getPlayerPlayedForMaxCountry()`
2. Create `Solution` class with attributes: `listOfPlayers`.
   - Implement methods: `countPlayers(country)`, `getPlayerPlayedForMaxCountry()`

### Input / Output Examples:
```
Input 1:
2
Mayank
2
Af
Br
21
India
Nupur
1
br
22
India
af   

Output:
No Country Found !
['Mayank']
Mayank

Input 2:
2
Mayank
2
Af
Br
21
India
Nupur
1
br
22
India
india   

Output:
2
['Mayank']
Mayank

```

### Solution Code:
```python
class CricketPlayer:
    def __init__(self,cplayerName , cplayedCountry , cplayerAge,cpCountryFrom):
        self.cplayerName = cplayerName
        self.cplayedCountry = cplayedCountry
        self.cplayerAge = cplayerAge
        self.cpCountryFrom = cpCountryFrom
        
class Solution:
    def __init__(self,listOfPlayers):
        self.listOfPlayers = listOfPlayers
    def countPlayers(self,country):
        count = 0
        for i in listOfPlayers:
            if i.cpCountryFrom.lower() == country.lower():
                count+=1
        return count
    def getPlayerPlayedForMaxCountry(self):
        dic = {}
        for i in listOfPlayers:
            dic[i.cplayerName] = len(i.cplayedCountry)
        # return (dic)
        m = max(dic.values())
        l2 = []
        for j in dic:
            if dic[j] == m:
                l2.append(j)
        l2.sort()
        print(l2)
        if len(l2)>0:
            return l2[0]
        else:
            return "no players found"
        
n = int(input())
listOfPlayers = []
for i in range(n):
    cplayerName = input()
    cplayedCountry = []
    for j in range(int(input())):
        cplayedCountry.append(input())
    cplayerAge = int(input())
    cpCountryFrom = input()
    objCricketPlayer = CricketPlayer(cplayerName , cplayedCountry , cplayerAge,cpCountryFrom)
    listOfPlayers.append(objCricketPlayer)
country = input()
objSolution = Solution(listOfPlayers)
ans = objSolution.countPlayers(country)

if ans:
    print(ans) 
else:
    print("No Country Found !")
# print(objSolution.countPlayers(country))
print(objSolution.getPlayerPlayedForMaxCountry())


'''
Input 1:
2
Mayank
2
Af
Br
21
India
Nupur
1
br
22
India
af   

Output:
No Country Found !
['Mayank']
Mayank

Input 2:
2
Mayank
2
Af
Br
21
India
Nupur
1
br
22
India
india   

Output:
2
['Mayank']
Mayank
'''
```

---

## Practice Problem 10: 16thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Container` class with attributes: `id,length,breadth,height,pricePerSq`.
   - Implement methods: `volume()`, `findCCost(value)`, `findLargestC()`
2. Create `PackagingCompany` class with attributes: `listOfContainer`.
   - Implement methods: `findCCost(value)`, `findLargestC()`

### Input / Output Examples:
```
Input:
2
1
2
3
4
10
2
5
6
7
20
1

Output:
Price Of Container with id 1 is :  240
2 210

```

### Solution Code:
```python
# This is a 35 marks python coding question on classes asked in TCS IPA exams 
# In this question the problem is to find out the cost of the container by asking id from the user and to find the id and volume of the largest container

class Container:
    def __init__(self,id,length,breadth,height,pricePerSq):
        self.id = id
        self.length = length
        self.breadth = breadth
        self.height = height
        self.pricePerSq = pricePerSq
    def volume(self):
        v = (self.length*self.breadth*self.height)
        
        return v
class PackagingCompany:
    def __init__(self,listOfContainer):
        self.listOfContainer = listOfContainer
    def findCCost(self,value):
        for i in listOfContainer:
            if i.id == value:
                call = i.volume()
                cost = (call * i.pricePerSq)
                return cost
            else:
                return None 
    def findLargestC(self):
        l1 = []
        for i in listOfContainer:
            call = i.volume()
            l1.append(call)
        # print(l1)
        m = max(l1)
        l2 = []
        for i in self.listOfContainer:
            call = i.volume()
            if call == m:
                l2.append(i.id)
                l2.append(call)
        return l2

n = int(input())
listOfContainer = []
for i in range(n):
    id = int(input())
    length = int(input())
    breadth = int(input())
    height = int(input())
    pricePerSq = int(input())
    objContainer = Container(id,length,breadth,height,pricePerSq)
    listOfContainer.append(objContainer)


value = int(input())
packagingCompanyObj = PackagingCompany(listOfContainer)
ans1 = packagingCompanyObj.findCCost(value)
if ans1:
    print(f"Price Of Container with id {value} is : ",ans1)
else:
    print("No Container")
ans2 = packagingCompanyObj.findLargestC()
for i in range(len(ans2)):
    print(ans2[i],end=' ')



'''

Input:
2
1
2
3
4
10
2
5
6
7
20
1

Output:
Price Of Container with id 1 is :  240
2 210
'''
```

---

## Practice Problem 11: 16thjuly

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Album` class with attributes: `aname,sname,atrack,atype`.
   - Implement methods: `m1()`
2. Create `song` class with attributes: `list1`.
   - Implement methods: `m1()`

### Input / Output Examples:
```
Input:
3
Mayank
lforgetable    
13
pop
bohemia
ldanali
5
rock
nupur
bohiman rampasi
2
digital

Output:
Mayank
bohemia

Input:
3
malayalam
radar
nitish

Output:
malayalam
radar

```

### Solution Code:
```python
'''class Album:
   def __init__(self,aname,sname,atrack,atype):
      self.sname = sname
      self.aname = aname
      self.atrack = atrack
      self.atype = atype
class song:
   def __init__(self,list1):
      self.list1 = list1
   def m1(self):
      L2 = []
      for i in list1:
         if i.aname[0].lower() == 'L'.lower() and i.atrack >= 5 and i.atype.lower() != 'Digital'.lower() :
            L2.append(i.sname)
      if L2 == []:
         print('No Albums found')
      else: 
         for j in L2:
            print(j)

list1 = []
for i in range(int(input())):
   sname = input()
   aname = input() 
   atrack = int(input())
   atype = input()
   obj1 = Album(aname,sname,atrack,atype)
   list1.append(obj1)
obj2 = song(list1)
ans = obj2.m1()

'''
'''
Input:
3
Mayank
lforgetable    
13
pop
bohemia
ldanali
5
rock
nupur
bohiman rampasi
2
digital

Output:
Mayank
bohemia

'''


# Print All Palindrom Strings present in the list 



n = int(input())
l =[]
for i in range(n):
    l.append(input())
for i in l:
    if i == i[::-1]:
        print(i)
        




'''
Input:
3
malayalam
radar
nitish

Output:
malayalam
radar
'''
```

---

## Practice Problem 12: 17thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Service` class with attributes: `serviceId,regNo,model,mileage,isInsured,paymentRecvd`.
   - Implement methods: `getTotalPaymentOfInsuredCars(ManufacturerName,stateCode,statename,mName)`
2. Create `ServiceCentre` class with attributes: `mileagedict,serviceList`.
   - Implement methods: `getTotalPaymentOfInsuredCars(ManufacturerName,stateCode,statename,mName)`

### Input / Output Examples:
```
4
101
MA1234
Tata Indica
15
yes
2500
102
MA472367
Honda City
18
yes
35000
103
UK4321
Honda Bravo
17
yes
5600
104
MA2221
Tata Nano
12
yes
2300
5
Tata Indica
15
Tata Nano
12
Honda City
20
Honda bravo
17
Hyundai Accent
18
tata 
ma

Output:
MA TATA 4800.0
103#UK4321#Honda Bravo#17
101#MA1234# ata indica#15
104#MA2221#Tata Nano#12

```

### Solution Code:
```python
class Service:
    def __init__(self,serviceId,regNo,model,mileage,isInsured,paymentRecvd):
        self.serviceId = serviceId
        self.regNo = regNo
        self.model = model
        self.mileage = mileage
        self.isInsured = isInsured
        self.paymentRecvd = paymentRecvd


class ServiceCentre:
    def __init__(self,mileagedict,serviceList):
        self.mileagedict = mileagedict
        self.serviceList = serviceList
    def getTotalPaymentOfInsuredCars(self,ManufacturerName,stateCode,statename,mName):
        l=[]
        for i in serviceList:
            # if mName ==
            pass
        # for i in serviceList:
        #     if i.isInsured.lower() == 'yes'.lower():
        #         l.append(i.paymentRecvd)
        #     s = sum(l)
        #     print(s)

serviceList = []
n = int(input())
for i in range(n):
    serviceId = int(input())
    regNo = input()
    model = input()
    mileage = int(input())
    isInsured = input()
    paymentRecvd = float(input())
    Serviceobj = Service(serviceId,regNo,model,mileage,isInsured,paymentRecvd)
    serviceList.append(Serviceobj)

m = int(input())
for i in range(m):
    ManufacturerName = input()
    stateCode = int(input())

mileagedict = {}
for i in serviceList:
    mileagedict[i.model] = i.mileage
print(mileagedict)



mName = input()
statename = input()

'''

4
101
MA1234
Tata Indica
15
yes
2500
102
MA472367
Honda City
18
yes
35000
103
UK4321
Honda Bravo
17
yes
5600
104
MA2221
Tata Nano
12
yes
2300
5
Tata Indica
15
Tata Nano
12
Honda City
20
Honda bravo
17
Hyundai Accent
18
tata 
ma

Output:
MA TATA 4800.0
103#UK4321#Honda Bravo#17
101#MA1234# ata indica#15
104#MA2221#Tata Nano#12

 '''
```

---

## Practice Problem 13: 18thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `iqtest` class with attributes: `id,name,mage,page`.
   - Implement methods: `iqcalc()`
2. Create `hex` class with attributes: `l`.
   - Implement methods: `iqcalc()`

### Input / Output Examples:
```
Input:
3
27    
lavish
20
13
08
darlish
17
13
16
shona
22
11

Output:
lavish : 153.84615384615387
darlish : 130.76923076923077
shona : 200.0

```

### Solution Code:
```python
class iqtest:
    def __init__(self,id,name,mage,page):
        self.id = id
        self.name = name
        self.mage = mage
        self.page = page

class hex:
    def __init__(self,l):
        self.l=l

    def iqcalc(self):
        for i in l:
            iq = (i.mage/i.page)*100
            print(f"{i.name} : {iq}")

l = []
for i in range(int(input())):
    id = int(input())
    name = input()
    mage = int(input())
    page = int(input())
    obj = iqtest(id,name,mage,page)
    l.append(obj)
hexobj = hex(l)
ans1 = hexobj.iqcalc()
'''

Input:
3
27    
lavish
20
13
08
darlish
17
13
16
shona
22
11

Output:
lavish : 153.84615384615387
darlish : 130.76923076923077
shona : 200.0

'''
```

---

## Practice Problem 14: 20thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Solution Code:
```python
# ninja to digital praction questions 
'''
will work on it
when i'll spare time for that

'''
```

---

## Practice Problem 15: 21stApril

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Solution Code:
```python
'''

# 35 marks ninja to digital asked in 22 march 2023 question

n1 = int(input())
s = input().split(" ")


n2 = int(input())
s1 = input().split(" ")

l1 = []
for i in s:
    if i in s1:
        pass
    else:
        l1.append(i)
ans = ''
for i in l1:
    ans = ans + i + ' '
print("Missing songs :",ans)
            
# print("Songs Of Old Playlist : ",s)
# print("Songs Of Old Playlist : ",s1)

'''

'''

input 
8 
1 2 3 4 5 6 7 8 
5
2 5 7 8 6

output
1 3 4


'''

# Ipa 15 marks question asked on 30th march 2023

s = input()
counta = 0
countn = 0 
for i in s:
    if i.isalpha():
        counta +=1
    elif i.isdigit():
        countn +=1
if counta > countn and countn!=0:
    print("Alphabets :",counta)
    print("Numbers :",countn)
elif countn > counta and counta!=0:
    print("Numbers :",countn)
    print("Alphabets :",counta)
elif counta > countn and countn ==0:
    print("Alphabets :",counta)
elif countn > counta and counta==0:
    print("Numbers :",countn)

    

'''
input 1 :
23455fdf

Output 1:
Numbers : 5
Alphabets : 3

input 2 :
dsfg23

Output2:
Alphabets : 4
Numbers : 2

input 3 :
342345

Output 3:
Numbers : 6

input 4 :
dfdg

Output 4:
Alphabets : 4
'''
```

---

## Practice Problem 16: 21stApril_Afternoon_practice

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
hello worldaeiu 123

Output:
hll wrld 123
3

```

### Solution Code:
```python
# TCS IPA 9 APRIL 15 MARKS QUESTION

s1 = input()
s = s1.split(" ")
l1 = []
length = len(s)
vowels = ['a','e','i','o','u']
for i in s1:
    if i in vowels:
        pass
    else:
        l1.append(i)
x = ''
for i in l1:
    x += i
print(x)
print(length)


"""
Input:
hello worldaeiu 123

Output:
hll wrld 123
3
"""
```

---

## Practice Problem 17: 23rdMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Account` class with attributes: `branch_name , accountList`.
   - Implement methods: `m1(wAmount)`, `m2(ucardNumber , upin, uwAmount )`
2. Create `ATM` class with attributes: `branch_name , accountList`.
   - Implement methods: `m2(ucardNumber , upin, uwAmount )`

### Solution Code:
```python
class Account:
    def __init__(self, cardNumber, pin, balance, wAmount, accountType) :
        self.cardNumber = cardNumber
        self.pin = pin
        self.balance = balance
        self.wAmount = wAmount
        self. accountType = accountType
    def m1 (self, wAmount):
        if wAmount <= self.balance:
            nbalance = self.balance - uwAmount
            self.balance = nbalance
        return nbalance 
class ATM:
    def __init__(self,branch_name , accountList):
        self.branch_name = branch_name
        self.accountList = accountList
    def m2 (self, ucardNumber , upin, uwAmount ): 
        for i in self.accountList:
            if i.cardNumber == ucardNumber and i.pin == upin:
                call = i.m1 (uwAmount )
                print(f"{i.cardNumber} {call} {uwAmount}")
                break
        else:
            print ( "No account Exists")
    def m3 (self, uaccountType) :
        dic = {}
        for i in self.accountList:
            if i.accountType.lower () == uaccountType. lower ( ) :
                dic[i.cardNumber] = i.balance
        return dic
accountList = []
for i in range (int (input ( ) ) ) :
    cardNumber = int (input ( ))
    pin = int (input ( ))
    balance = float (input ( ))
    wAmount = float (input ( ) )
    accountType = input ( )
    objAccount = Account ( cardNumber, pin, balance, wAmount, accountType )
    accountList.append (objAccount)
ucardnumber = int (input () )
upin = int (input ( ))
uwAmount = float (input ( ) )
uaccountType = input ( )

objATM = ATM( 'Delhi' , accountList)
ans1 = objATM. m2(ucardnumber, upin, uwAmount )
ans2 = objATM.m3(uaccountType )
if ans1:
    print(ans1)

if ans2:
    for i in ans2:
        print(i,ans2[i])




"""
Input 2:
2
12345
12
30.0
10.0
salary
45678
98
400.0
200.0
salary
12345
12
10
salary

Output 2:
12345 20.0 10.0
12345 20.0
45678 400.0


Input 2:
2
12345
12
30.0
10.0
salary
45678
98
400.0
200.0
salary
34532
34
12
salary

Output 2:
No account Exists
12345 30.0
45678 400.0

"""
```

---

## Practice Problem 18: 24thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
3
3
1
Hamlet
shakesphere
2
Macbeth
SHAKESPHERE
3
othello
Shakesphere
A-10
gomtinagar
lucknow
u.p.
201876
3
1
A Christmas Carol.
Charles Dickens
2
Bleak House
Charles Dickens
3
Oliver Twist
Charles Dickens
A-770
rajamandi
agra
u.p.
2018763
3
1
The adventures of sherlock holmes
sherlock holmes
2
The return of sherlock holmes
sherlock holmes
3
The sign of the four
sherlock holmes
A-660
Khairatabad
lucknow
u.p.
201876
lucknow

Output:
SHAKESPHERE 3

```

### Solution Code:
```python
'''
Write the code to define a class to create a Book object with the below attributes:

book id, book name, the name of the author of book.



Define the method to initialize the attributes when a Book object is created.


Write the code to define a Class to Create a Library object with the below attributes:

a list of Book type
an address of the Library , a dictionary in the format as follows:
{street: 'A-10', area:”gomitnagar”,city: 'Lucknow', state: 'UP', zip: 1090034}


Define a method to initialize the attributes when a Library object is created.



Define another method inside the class as below:

The method will find the count of books for each author from the book List of the Library class and returns a dictionary having the author name and bookCount (count of books) as key : value pairs. The search for author name should be case insensitive and return result with author name in UPPER case only.


Define a method outside both the classes.

This method will take name of a city and a list of Library objects as parameters and return the list of books which are present in the libraries of the given list which has the given city name as city in the address. If there is no Library in the given list which has the given city name as city in the address, the method should return None else it will return the list of books in descending order of book id for each library object with matching city i.e. If the city is matching with the library object1 and library object3, the method will display the list of books from library object1 in descending order of book id and then it will display the list of books from library object3 in descending order of book id. Please refer the sample input and output below for more clarity.


Note : All String Comparison should be case insensitive.



Instructions to write main function:

You would require to write the main section completely, hence please follow the below instructions for the same.

You would require to write the main program which is in line to the "sample input description section" mentioned below and to read the data in the same sequence.

Create the respective objects of the classes defined referring to the below instructions.



Main Function Instructions:



A. Create a list of Library objects which will be passed as argument while calling the function in main. To create the list:

Read a number for the count of Library objects to be created and added to the list.

Create a library object to be added to the list. To create the library object, do the following:

Read a number for the count of book objects to be added to the list of book objects for the library objects.

Create a book object after reading the data (book Id, book Name, author Name) related to it and add to the list of book objects. This point repeats for the count of Book objects to be created as per point #A.2.1.

Read values for the Address of the Library object. Attributes of the address are street, area, city, state and zip. Considering these attributes as keys, store the values read as key : value pairs in a dictionary for the address.

Create a Library object by passing the list of Book objects and dictionary created above and add it to the library list. This repeats for the number of Library objects to be created (considered in the first line of input) as per point #A.1.

B. Read a string value as input depicting city to be passed as argument to the second function(function defined outside the class).

C. Call the method to find count of books author wise mentioned above from the main section using the first element of the List of Library objects created in point #A(i.e the First library Object created)

D. Display the values returned by the above function. Display the author names and count of books returned by the function as per the requirement given.

E. Call the second function from the main section, by passing the city name and the list of Library objects created above.

F. Display the list of book names returned by the second function.

- If function returns None, then display “No Book Found” (excluding the quotes).


Sample Input (below) description:

The first input taken in the main section is the number of Library Objects to be created(suppose n).

The next set of inputs are related to n Library objects to be created as follows:

Count of Book objects(Suppose m) to be created and added to the list of books for the Library.

The next set of inputs are values for attributes of m books -bookId, bookName, authorName (for each book object taken one after other and is repeated for m number of book objects).

Next set of values are for the following keys of the address for the Library object .

street
area
city
state
zip
Last line of input represents the City Name, supplied as a argument to the second function.



You can use/refer the below given sample input and output for more details of the format for input and output.



Consider below sample input and output to test your code:

Sample Input :

3
3
1
Hamlet
shakesphere
2
Macbeth
SHAKESPHERE
3
othello
Shakesphere
A-10
gomtinagar
lucknow
u.p.
201876
3
1
A Christmas Carol.
Charles Dickens
2
Bleak House
Charles Dickens
3
Oliver Twist
Charles Dickens
A-770
rajamandi
agra
u.p.
2018763
3
1
The adventures of sherlock holmes
sherlock holmes
2
The return of sherlock holmes
sherlock holmes
3
The sign of the four
sherlock holmes
A-660
Khairatabad
lucknow
u.p.
201876
lucknow


Output :

SHAKESPHERE 3
['othello', 'Macbeth', 'Hamlet', 'The sign of the four', 'The return of sherlock holmes', 'The adventures of sherlock holmes']


'''

class book:
    def __init__(self,id , name,author):
        self.id = id
        self.name = name
        self.author = author
class library:
    def __init__(self,book_list,address):
        self.book_list = book_list
        self.address = address
    def bookCount(self):
        l3 = []
        count = 0
        for i in range(len(book_list)):
            for j in book_list:
                l3.append(j.author)
                break
            # print(l3)
        # k = set(l3)
        # print(k)
        print(f"{j.author.upper()} {l3.count('Shakesphere')}")
        

book_list = []
n = int(input())
for j in range(n):
    m = int(input())
    for i in range(m):
        id = int(input())
        name = input()
        author = input()
        address = {}
    
    street = input()
    area = input()
    city = input()
    state = input()
    zip= int(input())
    address[street] = street 
    address[area] = area 
    address[city] = city 
    address[state] = state 
    address[zip] = zip

    objBook = book(id,name,author)
    book_list.append(objBook)

city = input()
libobj = library(book_list,address)
ans1 = libobj.bookCount()
if ans1:
    print(ans1)

'''
"""

Input:
3
3
1
Hamlet
shakesphere
2
Macbeth
SHAKESPHERE
3
othello
Shakesphere
A-10
gomtinagar
lucknow
u.p.
201876
3
1
A Christmas Carol.
Charles Dickens
2
Bleak House
Charles Dickens
3
Oliver Twist
Charles Dickens
A-770
rajamandi
agra
u.p.
2018763
3
1
The adventures of sherlock holmes
sherlock holmes
2
The return of sherlock holmes
sherlock holmes
3
The sign of the four
sherlock holmes
A-660
Khairatabad
lucknow
u.p.
201876
lucknow

Output:
SHAKESPHERE 3

"""
```

---

## Practice Problem 19: 25thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Sponsor` class with attributes: `sName,sCompany,stieup,sCategory`.

### Input / Output Examples:
```
Input:
2     
Mayank
TCS
2      
google
apple
IT
Nupur
cogniant
1
microsoft
Education  
education

Output:
Nupur
Mayank

Input:
abc def4 5$

Output:
6 2 2

```

### Solution Code:
```python
# practice 

class Sponsor:
    def __init__(self,sName,sCompany,stieup,sCategory):
        self.sName = sName
        self.sCompany = sCompany
        self.stieup = stieup
        self.sCategory = sCategory
def getSponsor(listSponsor,usCategory):
    for i in listSponsor:
        if i.sCategory.lower() == usCategory.lower():
            print(i.sName)
def maxTieup(listSponsor):
    l1 =[]
    for i in listSponsor:
        l = len(i.stieup)
        l1.append(l)
    # print(l1)
    m = max(l1)
    # print(m)
    for i in listSponsor:
        if len(i.stieup) == m:
            print(i.sName)
listSponsor = []
for i in range(int(input())):
    sName = input()
    sCompany = input()
    stieup = []
    for j in range(int(input())):
        stieup.append(input())
    sCategory = input()
    obj = Sponsor(sName,sCompany,stieup,sCategory)
    listSponsor.append(obj)
usCategory = input()
ans = getSponsor(listSponsor,usCategory)
ans2 = maxTieup(listSponsor)

'''

Input:
2     
Mayank
TCS
2      
google
apple
IT
Nupur
cogniant
1
microsoft
Education  
education

Output:
Nupur
Mayank

'''

'''

#Another Question for practice

n = input()     
l = n.split("$")
countSpace =0
countLower =0
countNumber=0
for i in range(len(l)):
    for j in l[i]:
        if j.isspace():
            countSpace +=1
        elif j.islower():
            countLower +=1
        elif j.isdigit():
            countNumber +=1
print(f"{countLower} {countNumber} {countSpace}")

'''
'''
Input:
abc def4 5$

Output:
6 2 2
'''
```

---

## Practice Problem 20: 25thMarchNightOut

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Movie` class with attributes: `id,director,rating,budget`.
   - Implement methods: `findAvgBudgetByDirector(user_director)`
2. Create `Solution` class with attributes: `list_movie`.
   - Implement methods: `findAvgBudgetByDirector(user_director)`

### Input / Output Examples:
```
Input 1:
5
1
2
3
4
6

Output:
Second largest:  4
Second Smallest:  2


Input 2:
3

Output:
N should be greater than 3

Input:
4
101
gvm
4
100
102
shankar
5
500
103
shankar
3
50
104
gvm
5
300
gvm
5
300

Output:
200.0
104 gvm 5 300

```

### Solution Code:
```python
n = int(input())
l1 = []
if n>3:
    for i in range(n):
        l1.append(int(input()))
    l1.sort()
#     print(l1)
    n=len(l1)
    for j in l1:
        print("Second largest: ",l1[n-2])
        print("Second Smallest: ",l1[j])
        break

else:
    print("N should be greater than 3")

    
"""
Input 1:
5
1
2
3
4
6

Output:
Second largest:  4
Second Smallest:  2


Input 2:
3

Output:
N should be greater than 3

""" 

'''
class Movie:
    def __init__(self,id,director,rating,budget):
        self.id = id
        self.director = director
        self.rating = rating
        self.budget = budget
class Solution:
    def __init__(self,list_movie):
        self.list_movie = list_movie
    def findAvgBudgetByDirector(self,user_director):
        avg = 0
        count = 0
        for i in list_movie:
            if i.director.lower() == user_director.lower():
                count +=1
                avg += i.budget
        avg = avg/count
        return avg
    def getMoviebyratingandbudget(self,user_rating,user_budget):
        for i in list_movie:
            if i.rating == user_rating and i.budget == user_budget and i.budget%i.rating ==0:
                # print(i)
                print(i.id , i.director , i.rating , i.budget)
        
n = int(input())
list_movie = []
for i in range(n):
    id = int(input())
    director = input()
    rating = int(input())
    budget = int(input())
    objMovie = Movie(id,director,rating,budget)
    list_movie.append(objMovie)
user_director = input()
user_rating = int(input())
user_budget = int(input())
objSolution = Solution(list_movie)
ans1 = objSolution.findAvgBudgetByDirector(user_director)
if ans1:
    print(ans1)
else:
    print("No movie of this director")
ans2 = objSolution.getMoviebyratingandbudget(user_rating,user_budget)
if ans2:
    print(ans2)
'''

'''

Input:
4
101
gvm
4
100
102
shankar
5
500
103
shankar
3
50
104
gvm
5
300
gvm
5
300

Output:
200.0
104 gvm 5 300

'''
```

---

## Practice Problem 21: 26thApril

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Solution Code:
```python

```

---

## Practice Problem 22: 26thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
1,2,3,4,5,6 ,23, 09

Output:
1 3

Input:
5
1
10000
Electric
available
2
20000
Diesel
NotAvailable 
3
30000
Electric
Available
4
20000
petrol
available
5
30000
Electric
Available

Output:
['ELECTRIC', 'DIESEL', 'ELECTRIC', 'PETROL', 'ELECTRIC']
Electric : 3
Diesel : 0
Petrol : 1

```

### Solution Code:
```python
'''

n = input().split(",")
l = []
for i in n:
    l.append(i)
for i in range(len(l)):
    print(l[0],l[i+2])
    break

'''
"""

Input:
1,2,3,4,5,6 ,23, 09

Output:
1 3

"""
'''
l1 = []
l2 = []
for i in range(int(input())):
    serial = int(input())
    km = int(input())
    type = input().upper()
    availability = input().upper()
    l1.append(type)
    l2.append(availability)
print(l1)
# l3 = set(l1) set does not work while indexing so it should not be used here
l3 = []
for i in l1:
    if i in l3:
        pass
    else:
        l3.append(i)
print(l3)
l4 = []
for i in l3:
    c = 0
    for j in range(len(l2)):
        print(l2[j])
        if l1[j].lower() == i.lower() and l2[j].lower() == 'Available'.lower():
                c +=1
    l4.append(c)
for i in range(len(l3)):
    print(l3[i].capitalize(),":",l4[i])
'''


"""

Input:
5
1
10000
Electric
available
2
20000
Diesel
NotAvailable 
3
30000
Electric
Available
4
20000
petrol
available
5
30000
Electric
Available

Output:
['ELECTRIC', 'DIESEL', 'ELECTRIC', 'PETROL', 'ELECTRIC']
Electric : 3
Diesel : 0
Petrol : 1

"""

'''l = []
for i in range(int(input())):
    l.append(input())
n = input()
for i in range(len(l)):
    if l[i].lower() == n.lower():
        print("INDEX : ",i)
'''

'''

4
Good morning
abcdefg
India
mayank@tcs.com
india

'''
'''
n = input()
counta = 0
counts = 0
for i in n:
    if i.isalpha() == True :
        counta +=1
    elif i.isspace() == True:
        counts +=1
print(f"Numbre of spaces are : {counts}")
print(f"Numbre of letters are : {counta}")

'''

'''
Good morning
Numbre of spaces are : 1
Numbre of letters are : 11
'''

'''n = input()
v = ['a','e','i','o','u']
# v = 'aeiouAEIOU'
count = 0
l1 = []
for i in n:
    if i.isalpha():
        if i.lower() in v:
            count+=1
print("Number of vovels are :",count)
'''

'''
Good morning
Number of vovels are : 4
'''

'''
n = input()
s = 0
for i in n:
    s = s+(int(i))
print(s)
if s%3==0:
    print("True")
else:
    print("False")
'''

'''
333
9
True

'''


'''
l = []
for i in range(int(input())):
    n = input().split()
    l +=n
# print(l)
s = input()
c = 0
for i in l:
    if i.lower() == s.lower():
        c +=1
if c:
    print(c)
else:
    print("Target Not Found")

'''
'''
4
Hello World!
hi I am Hello
hello this is Hello
Tcs Explore
hello

4
'''
```

---

## Practice Problem 23: 26thMarchNightOut

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Doctor` class with attributes: `docId,name,spec,consultfee`.
   - Implement methods: `searchbyDocName(userName)`, `calc(userSpec)`
2. Create `Hospital` class with attributes: `Docdb`.
   - Implement methods: `searchbyDocName(userName)`, `calc(userSpec)`

### Input / Output Examples:
```
Input:
5
90901
Govind
ENT
500
90902
Madhuri
dermitologist
700
90903
Divya
Gynaecologist       
600
90904
Suryam
Cardiologist
900
90905
Madhuri
Cardiologist
1000
Madhuri
cardiologist

Output:

90902 Madhuri dermitologist 700
90905 Madhuri Cardiologist 1000
1900

Input:
4
123
HP
windows
35000
5
124
Apple
Mac Os
70000
5
125
Dell
Ubuntu
30000
4
126 
HP
windows
40000
4
HP

Output:

2
123 5
126 4

Input:
Hey There!

Output:
e hr!

```

### Solution Code:
```python
'''

class Doctor:
    def __init__(self,docId,name,spec,consultfee):
        self.docId = docId
        self.name = name
        self.spec = spec
        self.consultfee = consultfee
class Hospital:
    def __init__(self,Docdb):
        self.Docdb = Docdb
        # self.listDoc = listDoc
    def searchbyDocName(self,userName):
        for i in Docdb.values():
            for j in i:
                if j.name.lower() == userName.lower():
                    print(j.docId , j.name , j.spec , j.consultfee)
    def calc(self,userSpec):
        for i in Docdb.values():
            c = 0
            for j in i:
                if j.spec.lower() == userSpec.lower():
                    c += j.consultfee
            return c 


listDoc = []
for i in range(int(input())):
    docId = int(input())
    name = input()
    spec = input()
    consultfee = int(input())
    Docdb = {}
    hospitalSerialNumber = '02213'
    objDoc = Doctor(docId,name,spec,consultfee)
    listDoc.append(objDoc)
    Docdb[hospitalSerialNumber] = listDoc
userName = input()
userSpec = input()
objHospital = Hospital(Docdb)
ans1 = objHospital.searchbyDocName(userName)
ans2 = objHospital.calc(userSpec)
if ans2:
    print(ans2)
else:
    print("No Doctor Found!")



'''
'''
Input:
5
90901
Govind
ENT
500
90902
Madhuri
dermitologist
700
90903
Divya
Gynaecologist       
600
90904
Suryam
Cardiologist
900
90905
Madhuri
Cardiologist
1000
Madhuri
cardiologist

Output:

90902 Madhuri dermitologist 700
90905 Madhuri Cardiologist 1000
1900

'''

class laptop:
    def __init__(self,id,brand,osType,price,rating):
        self.id = id
        self.brand = brand 
        self.osType = osType
        self.price = price
        self.rating = rating
class Solution:
    def __init__(self,list):
        self.list = list
    def CountLaptop(slef,userBrand):
        c = 0
        for i in list:
            if i.brand.lower()== userBrand.lower():
                c+=1
        return c
    def SearchLaptopbyosType(self,userOs):
        l1 = []
        for i in list:
            if i.osType.lower() == userOs.lower():
                l1.append(i)
            # l2 = l1.sort()
        for j in l1:
            print(f"{j.id} {j.rating}")
            # print(j.id,j.rating)

                
list = []
for i in range(int(input())):
    id = int(input())
    brand =  input()
    osType = input()
    price = float(input())
    rating = int(input())
    objLaptop = laptop(id,brand,osType,price,rating)
    list.append(objLaptop)
userBrand = input()
userOs = input()
objSol = Solution(list)
ans1 = objSol.CountLaptop(userBrand)
if ans1:
    print(ans1)
else:
    print("No Laptop found")

ans2 = objSol.SearchLaptopbyosType(userOs)



'''
Input:
4
123
HP
windows
35000
5
124
Apple
Mac Os
70000
5
125
Dell
Ubuntu
30000
4
126 
HP
windows
40000
4
HP

Output:

2
123 5
126 4
'''

'''
n = input()
j = ''
for i in range(len(n)):
    if i%2 == 0:
        pass
    else:
        j += n[i]
print(j)
        # print(n[i],end="") 

'''

'''

Input:
Hey There!

Output:
e hr!

'''
```

---

## Practice Problem 24: 27thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `pan` class with attributes: `id , material,brand,price,capacity`.
   - Implement methods: `CostliestPan(userMaterial)`, `discounted(userBrand)`
2. Create `Solution` class with attributes: `list`.
   - Implement methods: `CostliestPan(userMaterial)`, `discounted(userBrand)`

### Input / Output Examples:
```
Input 1:
5
3
4
3
7
4
3

Output:
2

```

### Solution Code:
```python
class pan:
    def __init__(self,id , material,brand,price,capacity):
        self.id = id 
        self.material = material
        self.brand = brand
        self.price = price
        self.capacity = capacity
class Solution:
    def __init__(self,list):
        self.list = list
    def CostliestPan(self,userMaterial):
        l = []
        for i in list:
            if i.material.lower() == userMaterial.lower():
                l.append(i.price)
        for j in l:
            if j == max(l):
                return i.id
            
    def discounted(self,userBrand):
        for i in list:
            if i.brand.lower() == userBrand.lower() and 1000 > i.capacity > 500:
                i.price -= ((i.price*20)/100)
                return i.price
            elif i.brand.lower() == userBrand.lower() and i.capacity >1000:
                i.price -= ((i.price*26)/100)
                return i.price
list = []
for i in range(int(input())):
    id = input()
    material = input()
    brand = input()
    price = int(input())
    capacity = int(input())
    objPan = pan(id,material,brand,price,capacity)
    list.append(objPan)
userMaterial = input()
userBrand = input()
objSol = Solution(list)
ans1 = objSol.CostliestPan(userMaterial)
ans2 = objSol.discounted(userBrand)
if ans1:
    print(ans1)
else:
    print("No pan of this Material Found !")
if ans2:
    print(ans2)
else:
    print("No pan found of thid brand !")


'''  
Input 1:
5
id23
brass
a
200
120
id24
copper
b
300
1130
id25
chromium
c
400
640
id26
steel
d
500
950
id27
steel
e
800
950
steel
d

Output 1:
id27
400.0

################

Input 2:
5
id23
brass
a
200
120
id24
copper
b
300
1130
id25
chromium
c
400
640
id26
steel
d
500
950
id27
steel
e
800
950
gold 
d

Output 2:
No pan of this Material Found !
400.0
'''

# def find_second_index(nums, num_to_find):
#     first_index = nums.index(num_to_find)  # find the first occurrence of the number
#     second_index = nums.index(num_to_find, first_index+1) # find the second occurrence of the number
#     return second_index

# # Example usage
# my_list = [3, 7, 2, 5, 2, 8, 2, 9]
# num = 2
# second_index = find_second_index(my_list, num)
# print("The second occurrence of", num, "is at index", second_index)

'''

l = []
for i in range(int(input())):
    l.append(int(input()))
n = int(input())
first= l.index(n)
second = l.index(n,first+1)
print(second)

'''

'''
Input 1:
5
3
4
3
7
4
3

Output:
2

'''
```

---

## Practice Problem 25: 27thMarchNightout

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Player` class with attributes: `id,name,runs,playerType,matchType`.
   - Implement methods: `findPlayerWithLowestRun(userPlayerType)`, `findPlayerbyMatchType(userMatchType)`
2. Create `Solution` class with attributes: `list`.
   - Implement methods: `findPlayerWithLowestRun(userPlayerType)`, `findPlayerbyMatchType(userMatchType)`

### Input / Output Examples:
```
4
11
Sachin
100
International
one Day
12
Shewag
133
International
Test
13 
Varun
78
State
Test
14
Ashwin
67
State
One Day
State
One Day

Output:
Lowest Run Player : 67
11
14

```

### Solution Code:
```python
class Player:
    def __init__(self,id,name,runs,playerType,matchType):
        self.id = id 
        self.name= name
        self.runs = runs 
        self.playerType= playerType
        self.matchType = matchType
class Solution:
    def __init__(self,list):
        self.list = list

    def findPlayerWithLowestRun(self,userPlayerType):
        l=[]
        for i in list:
            if i.playerType.lower() == userPlayerType.lower():
                l.append(i.runs)
            # m = min(l)
        if l == []:
            print("Not Found")
        else:
            m = min(l)
            return m
    def findPlayerbyMatchType(self,userMatchType):
        l1 = []
        for i in list:
            if i.matchType.lower() == userMatchType.lower():
                l1.append(i.id)
            l1.sort()
        return l1

list = []
for i in range(int(input())):
    id = int(input())
    name = input()
    runs = int(input())
    playerType  = input()
    matchType = input()
    objPlayers = Player(id,name,runs,playerType,matchType)
    list.append(objPlayers)

userPlayerType = input()
userMatchType = input()
objSol = Solution(list)
ans1 = objSol.findPlayerWithLowestRun(userPlayerType)
ans2 = objSol.findPlayerbyMatchType(userMatchType)
if ans1:
    print("Lowest Run Player :",ans1)
else:
    print("All are Equal")
if ans2:
    for i in ans2:
        print(i)
else:
    print("Player Not Found")


'''
4
11
Sachin
100
International
one Day
12
Shewag
133
International
Test
13 
Varun
78
State
Test
14
Ashwin
67
State
One Day
State
One Day

Output:
Lowest Run Player : 67
11
14

'''
```

---

## Practice Problem 26: 29thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `sim` class with attributes: `id,cname,balance,rateperSec,circle`.
   - Implement methods: `TransferCustomerCircle(userCircle1,userCircle2)`

### Input / Output Examples:
```
5
1
raj
100
1.5
KOL
2
chetan
200
1.6
AHD
3
asha
150
1.7
MUM
4
kiran
50
2.2
AHD
5
vijay
130
1.8
AHD
AHD
KOL


Output:
4 kiran KOL 2.2
5 vijay KOL 1.8
2 chetan KOL 1.6

```

### Solution Code:
```python
class sim:
    def __init__(self,id,cname,balance,rateperSec,circle):
        self.id = id
        self.cname = cname
        self.balance = balance
        self.rateperSec = rateperSec
        self.circle = circle
class Solution :
    def __init__(self,list):
        self.list = list
    def TransferCustomerCircle(self,userCircle1,userCircle2):
        l1 = []
        for i in list:
            if i.circle.lower() == userCircle1.lower():
                i.circle = userCircle2
                l1.append(i)
        if l1 ==[]:
            return 0
        else:
            l1.sort(key = lambda x:x.rateperSec , reverse=True)
            for i in l1:
                print(f"{i.id} {i.cname} {i.circle} {i.rateperSec}")
            
list = []
for i in range(int(input())):
    id = int(input())
    cname = input()
    balance = float(input())
    rateperSec = float(input())
    circle = input()
    objsim = sim(id,cname,balance,rateperSec,circle)
    list.append(objsim)
userCircle1 = input()
userCircle2 = input()
objsol = Solution(list)
ans1 = objsol.TransferCustomerCircle(userCircle1,userCircle2)



'''
5
1
raj
100
1.5
KOL
2
chetan
200
1.6
AHD
3
asha
150
1.7
MUM
4
kiran
50
2.2
AHD
5
vijay
130
1.8
AHD
AHD
KOL


Output:
4 kiran KOL 2.2
5 vijay KOL 1.8
2 chetan KOL 1.6
'''
```

---

## Practice Problem 27: 2ndMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
5
23
87
45
12
75        
[12, 23, 45, 75, 87]

Output:
Second Largest Number :  75

Input:
33

Output:
True

Input:
4
Hello Good Morning
abcd123Fghy
India
progoti.c

Output:
Valid strings: 2 
Invalid strings: 2

```

### Solution Code:
```python
#1 use of split() and replace() function 


'''

strng = input()
l = strng.split()
j=[]
# print(l)
for i in l:
    if 'il' in i:
        k = i.replace('il','')
        # print(k)
        j.append(k)
    else:
        j.append(i)

s = ''
for i in j:
    s = s+i+' '
print(s)

    
'''

'''
input:
Mayank is happyil

output:
Mayank is happy

'''

#2 finding the second largest number in the list

'''

n = int(input())
l=[]
for i in range(n):
    l.append(int(input()))
# print(l)
for i in l:
    l.sort()
    
print(l)
print("Second Largest Number : ",l[-2])

'''

'''
Input:
5
23
87
45
12
75        
[12, 23, 45, 75, 87]

Output:
Second Largest Number :  75
'''

#3 Calculate the sum of digits of an integer input

"""

n = (input())
s=0
for i in n:
    s += int(i)
# print(s)
if s%3==0:
    print('True')
else:
    print("False")


"""


"""
Input:
33

Output:
True
"""


#4 Print the position or index of the given string

"""
n = int(input())
l=[]
for i in range(n):
    l.append(input())
print(l)
m = input()
for i in range(len(l)):
    if l[i] == m:
        print(i)
        break

"""

#5 check palindrome in list of strings and return it 

'''

n = int(input())
l=[]
for i in range(n):
    l.append(input())

for i in l:
    if i == i[::-1]:
        print("Palindrome Word = ",i)

'''
def count_valid_strings(string_list):
    valid_count = 0
    invalid_count = 0
    
    for string in string_list:
        if all(char.isalpha() or char.isspace() for char in string):
            valid_count += 1
        else:
            invalid_count += 1
    
    print(f"Valid strings: {valid_count} ")
    print(f"Invalid strings: {invalid_count} ")
# string_list = ["This is a valid string", "So is this!", "No$#t valid", "This is a    l s o valid"]
string_list = []
for i in range(int(input())):
    string_list.append(input())

count_valid_strings(string_list)

'''
Input:
4
Hello Good Morning
abcd123Fghy
India
progoti.c

Output:
Valid strings: 2 
Invalid strings: 2

'''
```

---

## Practice Problem 28: 30thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `area` class with attributes: `id,name,type`.
   - Implement methods: `Ssort(userType)`
2. Create `Solution` class with attributes: `list`.
   - Implement methods: `Ssort(userType)`

### Input / Output Examples:
```
Input:
3
101
Mayank
beach
2
Nupur
Mountain   
104
Gavish
beach
beach

Output:
104 Gavish beach
101 Mayank beach

```

### Solution Code:
```python
def countn(n):
    count1 = 0
    count2 = 0
    for i in n:
        if i.isdigit():
            count1+=1
        elif i.isalpha():
            count2 +=1
    if count1>count2:
        print("Number:", count1)
        print("Alphabets:", count2)
    else:
        print("Alphabets:", count2)
        print("Number:", count1)
n = input()
ans = countn(n)
if ans:
    print(ans)

'''
Input 1:
Sachin1234

Output 1:
Alphabets: 6
Number: 4

###############

Input 2:
12345678Sachi

Output 2:
Number: 8
Alphabets: 5

'''

'''

class area:
    def __init__(self,id,name,type):
        self.id = id
        self.name = name
        self.type = type
class Solution:
    def __init__(self,list):
        self.list = list
    def Ssort(self,userType):
        l1 = []
        for i in list:
            if i.type.lower() == userType.lower():
                l1.append(i)
        l2 = sorted(l1,key=lambda x:x.id ,reverse=True)
        for j in l2:
            print(f"{j.id} {j.name} {j.type}")
list = []
for i in range(int(input())):
    id = int(input())
    name = input()
    type = input()
    obj1 = area(id,name,type)
    list.append(obj1)
userType = input()
obj2 = Solution(list)
ans = obj2.Ssort(userType)

'''
'''
Input:
3
101
Mayank
beach
2
Nupur
Mountain   
104
Gavish
beach
beach

Output:
104 Gavish beach
101 Mayank beach
'''
```

---

## Practice Problem 29: 31thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Area` class with attributes: `id,name,type`.
   - Implement methods: `c1(userType)`
2. Create `Solution` class with attributes: `list`.
   - Implement methods: `c1(userType)`

### Input / Output Examples:
```
Input:
5
101
Mayank
Beach
102
Sachin
beach
103
Nidhi
mountain
104
Gavish
beach
105
tanishq
desert
beach

Output:
104 Gavish beach
102 Sachin beach
101 Mayank Beach

Input 1:
Sachin123Attkan

Output:
Alphabets:12
Numbers:3

Input 2:
123456sac

Output:
Number:6
Alphabets:3

```

### Solution Code:
```python
'''class Area:
    def __init__(self,id,name,type):
        self.id = id
        self.name = name
        self.type = type
class Solution:
    def __init__(self,list):
        self.list = list
    def c1(self,userType):
        l1 = []
        for i in list:
            if i.type.lower() == userType.lower():
                l1.append(i)
            l2 = sorted(l1,key = lambda x:x.id , reverse=True)
        for i in l2:
            print(f"{i.id} {i.name} {i.type}")
list=[]
for i in range(int(input())):
    id = int(input())
    name = input()
    type = input()
    objArea = Area(id,name,type)
    list.append(objArea)
userType = input()
objSol = Solution(list)
ans = objSol.c1(userType)
'''
'''

Input:
5
101
Mayank
Beach
102
Sachin
beach
103
Nidhi
mountain
104
Gavish
beach
105
tanishq
desert
beach

Output:
104 Gavish beach
102 Sachin beach
101 Mayank Beach
'''


def count(n):
    c1 = 0
    c2 = 0
    for i in n:
        if i.isdigit():
            c1 +=1
        elif i.isalpha():
            c2 +=1
    if c1 > c2 :
        print(f"Number:{c1}")
        print(f"Alphabets:{c2}")
    else:
        print(f"Alphabets:{c2}")
        print(f"Numbers:{c1}")
n = input()
ans = count(n)

'''
Input 1:
Sachin123Attkan

Output:
Alphabets:12
Numbers:3

Input 2:
123456sac

Output:
Number:6
Alphabets:3
'''
```

---

## Practice Problem 30: 3rdApril

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Area` class with attributes: `id,name,type`.
   - Implement methods: `c1(userType)`, `c2(string1)`
2. Create `Solution` class with attributes: `list`.
   - Implement methods: `c1(userType)`, `c2(string1)`

### Solution Code:
```python
class Area:
    def __init__(self,id,name,type):
        self.id = id
        self.name = name 
        self.type = type 
class Solution:
    def __init__(self,list):
        self.list = list
    def c1(self,userType):
        l1 = []
        for i in list:
            if i.type.lower() == userType.lower():
                l1.append(i)
            l2 = sorted(l1 ,key=lambda x:x.id ,reverse=True)
        for j in l2:
            print(f"{j.id} {j.name} {j.type}")
    def c2(self,string1):
        c1 = 0
        c2 = 0
        for i in string1:
            if i.isdigit():
                c1 +=1
            elif i.isalpha():
                c2 +=1
        if c1>c2:
            print(f"Numbers:{c1}")
            print(f"Alphabets{c2}")
        else:
            print(f"Alphabets{c2}")
            print(f"Numbers:{c1}")

list = []
for i in range(int(input())):
    id = int(input())
    name = input()
    type = input()
    obj1 = Area(id,name,type)
    list.append(obj1)
userType = input()
string1 = input()
obj2 = Solution(list)
ans1 = obj2.c1(userType)
print("\n#########################\n")
ans2 = obj2.c2(string1)
```

---

## Practice Problem 31: 3rdMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
sample input 1:
3                 
hello Mayank
Hello monu
Good Morning
['hello', 'Mayank', 'Hello', 'monu', 'Good', 'Morning']
hello

Output:
Count Of Given Word :  2


sample input 2:
3                 
hello Mayank
Hello monu
Good Morning      
['hello', 'Mayank', 'Hello', 'monu', 'Good', 'Morning']
gavish

Output:
Not Found

```

### Solution Code:
```python
# Count the number of prime in the given list using sympy module

"""
from sympy import *

n = int(input())
l=[]
for i in range(n):
    l.append(int(input()))

print(l)
count = 0
for i in l:
    if(isprime(i) == True):
        count +=1

    else:
        # print("notFound !")
        pass

print("Total Prime numbers in the list are = ",count)

"""


# Count the number of prime in the given list without using sympy module


'''

n = int(input())
l = []
for i in range(n):
    l.append(int(input()))

prime = []
for i in range(0,len(l)):
    for j in range(2,l[i]):
        if l[i]%j==0:
            # print("Not Prime")
            pass
            break
    else:
        prime.append(l[i])
    count = len(prime)
print(prime)
print(count)

'''

# count the number of time a given word repeated in users input string 

n = int(input())
l=[]
for i in range(n):
    j = (input().split(" "))
    l= l+j
print(l)
word = input()
count = 0
for i in l:
    if i.lower() == word.lower():
        count+=1
if count!=0:
    print("Count Of Given Word : ",count)
else:
    print("Not Found")


"""

sample input 1:
3                 
hello Mayank
Hello monu
Good Morning
['hello', 'Mayank', 'Hello', 'monu', 'Good', 'Morning']
hello

Output:
Count Of Given Word :  2


sample input 2:
3                 
hello Mayank
Hello monu
Good Morning      
['hello', 'Mayank', 'Hello', 'monu', 'Good', 'Morning']
gavish

Output:
Not Found

"""
```

---

## Practice Problem 32: 4thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Create `Scholar` class with attributes: `scholarId,scholarName,State,marks_list`.
   - Implement methods: `F1(list_Scholar,g)`
2. Create `ScholarResult` class with attributes: `attributes`.
   - Implement methods: `F1(list_Scholar,g)`

### Input / Output Examples:
```
Input:
hello hi word hello

Output:
hello

Sample Input 1 :
3
01
Mayank
Haryana 
99
98
89
02
Nupur
Delhi
87
98
99
03
rohan  
goa
57
84
34
c

Output:
3 rohan   175 C goa
goa 100: 0

#####################

Sample Input 2 :
3
01
Mayank
Haryana 
99
98
89
02
Nupur
Delhi
87
98
99
03
rohan  
goa
57
84
34
A
 
Output:
2 Nupur 284 A Delhi
1 Mayank 286 A Haryana 
goa 100: 0

```

### Solution Code:
```python
# print the word which occured the maximum time in the string

# 15 Marks Question
'''


strng = input()
l = strng.split()
setj = set(l)
# print(setj)
dict = {}
for i in setj:
    count = 0
    for j in l:
        if j.lower() == i.lower():
            count = count+1
    dict[i] = count
# print(dict)
l1 = []
for i in dict:
    l1.append(dict[i])
# print(l1)
m = max(l1)
for i in dict:
    if dict[i] == m:
        print(i)

'''




"""
Input:
hello hi word hello

Output:
hello

"""



#  35 Marks Question 
#scholar

class Scholar:
    def __init__(self,scholarId,scholarName,State,marks_list):
        self.scholarId = scholarId
        self.scholarName = scholarName
        self.State = State
        self.marks_list = marks_list
    
class ScholarResult:
    def F1(self,list_Scholar,g):
        ScholarGrade = []
        percentList = []
        TM = []
        for i in list_Scholar:
            s = 0
            for j in i.marks_list:
                s = s+int(j)
            TM.append(s)
            percentList.append(int(s/3))
        # print(percentList)
        k = 0
        
        for i in list_Scholar:
            dict = {}
            dict["scholarId"] = i.scholarId
            dict["scholarName"] = i.scholarName
            dict["TM"] = TM[k]
            if percentList[k] >=80:
                dict["G"] = "A"
            elif percentList[k] >=60 and percentList[k]<=80:
                dict["G"] = "B"
            elif percentList[k] >=50 and percentList[k] <=60:
                dict["G"] = "C"
            elif percentList[k] <50:
                dict["G"] = "D"
            dict["State"] = i.State
            ScholarGrade.append(dict)
            k+=1
        TM1= []
        for i in ScholarGrade:
            if i['G'].upper ()==g.upper ():
                TM1.append(i['TM'])
        if len (TM1)==0:
            print ("None")
        for i in TM1 [::-1]:
            for j in ScholarGrade:
                if i == j["TM"]:
                    print(j["scholarId"],j["scholarName"],j["TM"],j["G"],j["State"])
        ST=[]
        for j in ScholarGrade:
            ST.append(j["State"])
        ST = list (set (ST))
        ST = sorted (ST)
        # print (ST)
        kl =0
        for kl in ST:
            l5=[]
        for j in ScholarGrade:
            if j["State"] == kl:
                l5.append(j)
        P=0
        f=0
        for i in l5:
            if i["G"] in "ABC":
                P = P+1
            else:
                f =f+1
        k3=int ((P/len (l5) *100))
        k4 =int ((f/len (l5) *100))
        k5=str (k3) +": "+str (k4)
        print (kl, k5)
                    

            
        # print(ScholarGrade)
            
        

n = int(input())

list_Scholar = []
for i in range(n):
    scholarId = int(input())
    scholarName = input()
    State = input()
    marks_list = []
    for i in range(3):
        marks_list.append(int(input()))
    ScholarObj = Scholar(scholarId,scholarName,State,marks_list)
    list_Scholar.append(ScholarObj)

g = input()
SRobj = ScholarResult()
SRobj.F1(list_Scholar,g)

# for i in list_Scholar:
#     print(i.scholarId , i.scholarName ,i.State,i.marks_list)

# print(marks_list)


'''

Sample Input 1 :
3
01
Mayank
Haryana 
99
98
89
02
Nupur
Delhi
87
98
99
03
rohan  
goa
57
84
34
c

Output:
3 rohan   175 C goa
goa 100: 0

#####################

Sample Input 2 :
3
01
Mayank
Haryana 
99
98
89
02
Nupur
Delhi
87
98
99
03
rohan  
goa
57
84
34
A
 
Output:
2 Nupur 284 A Delhi
1 Mayank 286 A Haryana 
goa 100: 0
'''
```

---

## Practice Problem 33: 5thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
input 1:
2
MayankStudio
Ironman
200
Hindi
GavishStudio
Thor
300
Hindi

Output:
Movie Not Found

##########################
 
intput 2:
2
MayankStudio
Ironman
6000
english
GavishStudio
Thor
300
Hindi

output:
Ironman MayankStudio

input:
3
11
2
-3
20
7
5
-9
7
6

Output:
[11, 7, 6]
[-3, 7, -9]
19

```

### Solution Code:
```python
# 35 Marks Question Of TCS IPA held on 25 Feb 2023

'''

class Film :
    def __init__(self,filmStudio , filmName,Price,Language):
        self.filmStudio = filmStudio
        self.filmName = filmName
        self.price = price
        self.Language = Language
    def search_print(self,list):
        flag = 0
        for i in list:
            if i.Language.lower() == 'English'.lower() and i.price >= 500:
                flag = 1
                print(i.filmName , i.filmStudio)
               
        if flag==0:
            print("Movie Not Found")
        # else:


n = int(input())
list = []
for i in range(n):
    filmStudio = input()
    filmName = input()
    price = int(input())
    Language = input()

    FilmObj = Film(filmStudio , filmName,price,Language)
    list.append(FilmObj)
FilmObj.search_print(list)


'''

"""

input 1:
2
MayankStudio
Ironman
200
Hindi
GavishStudio
Thor
300
Hindi

Output:
Movie Not Found

##########################
 
intput 2:
2
MayankStudio
Ironman
6000
english
GavishStudio
Thor
300
Hindi

output:
Ironman MayankStudio
"""

# Ninja To digital Level Question 

# Finding Sum Of Diagonal of Matrix of 3*3 and Substract their values 

'''

n = int(input())
matirx = []
for i in range(n*n):
    matirx.append(int(input()))
diagonal1 = []
diagonal2 = []

diagonal1.append(matirx[0])
diagonal1.append(matirx[4])
diagonal1.append(matirx[8])

diagonal2.append(matirx[2])
diagonal2.append(matirx[4])
diagonal2.append(matirx[6])

print(diagonal1)
print(diagonal2)
s1 = sum(diagonal1)
s2 = sum(diagonal2)

ans = abs(abs(s1)-abs(s2))
print(ans)


'''

'''

input:
3
11
2
-3
20
7
5
-9
7
6

Output:
[11, 7, 6]
[-3, 7, -9]
19

'''
#Another Method to Solve this
# Finding Sum Of Diagonal of Matrix of 3*3 and Substract their values

l = []
for i in range (int (input ( ) )):
    j =input().split(" ")
    l=l+j
s =0
for i in range (len (l)) :
    if i == 0 or i==4 or i==8:
        s=s+int (l[i])
s1=0
for i in range (len (l)) :
    if i==2 or i==4 or i==6:
        s1=s1+int(l[i])
print (abs (abs (s)-abs (s1)))



'''
input:
3
11 2 -3
20 7 5
-9 7 6

output:
19

'''
```

---

## Practice Problem 34: 6thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
7
2
8
2
8
3
5
7
4
1
2

Output:
Numbers of Rats 7
Each Rat consume 2 units :
8 Houses with units available :  [2, 8, 3, 5, 7, 4, 1, 2]
Here is the count of houses :  4

```

### Solution Code:
```python
# Accenture Python Coding question 11 august 2021

r = int(input())
unit = int(input())
n = int(input())
arr = []
for i in range(n):
    arr.append(int(input()))

print("Numbers of Rats",r)
print(f"Each Rat consume {unit} units :" )
print(f"{n} Houses with units available : ",arr)

totalunitrequired = unit*r

s =0 
j = 0
for i in arr:
    if s>totalunitrequired:
        # print(j)
        break
    else:
        s+=i
        j+=1


print("Here is the count of houses : ",j)



"""

Input:
7
2
8
2
8
3
5
7
4
1
2

Output:
Numbers of Rats 7
Each Rat consume 2 units :
8 Houses with units available :  [2, 8, 3, 5, 7, 4, 1, 2]
Here is the count of houses :  4

"""


# WIPRO Python question on COUNTING PAIR OF COLOR OF SOCKS previous year asked 2022 slot


"""

l1 = []
n = int(input())
for i in range(n):
    l1.append(int(input()))
print(n)
print(l1)
l2 = set(l1)
s = 0
for i in l2:
    s = s +int((l1.count(i)/2))
print(s)

"""
    
    
    
    
"""
input:
9
10
20
20
10
10
30
50
10
20
output:
9
[10, 20, 20, 10, 10, 30, 50, 10, 20]
3
"""
```

---

## Practice Problem 35: 6thMay

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
4
john
barcelona
55
5
Ramu
kkr
60
4
Ravi
cbs
80
5
Lalit
csk
56
6
14

Output:
Ramu
Ravi

```

### Solution Code:
```python
'''
def m (n1,n2):
    l3 = []
    
    for i in n1:
        if i in n2:
            l3.append(i)
    l4 = set(l3)
    # return l4
    s = ''
    if len(l4) == 0:
        print("No number Found !")
    else:
        for i in l4:
            s = s+(i) +' '
        print("Answers:",s)
                

n1 = input().split(",")
n2 = input().split(",")
l1 = []
# for i in n1:
#     l1.append(int(input()))

l2 = []
# for i in range(n2):
#     l2.append(int(input()))

ans = m(n1,n2)
# s = ''
# if len(ans) == 0:
#     print("No number Found !")
# else:
#     for i in ans:
#         s = s+str(i) +' '
#         print("Answers: ",s)

# another approach


# x=input()
# y=input()
# x1 =x.split(",")
# y1 =y.split(",")
# l1=[]
# l2=[]
# for i in x1:        
#     if i in l1:
#         pass
#     else:
#         l1.append(i)
# for i in y1:
#     if i in l2:
#         pass
#     else:
#         l2.append(i)
# l3=[]
# for i in l1:
#     if i in l2:
#         l3.append(i)
# s=''
# if len(l3)==0:
#     print('No Number Found')
# else:
#     for i in l3:
#         s= s+i+" "
#     print(s)

'''


class C1:
    def __init__(self,runnername,nameofclub,distance,time):
        self.runnername = runnername
        self.nameofclub = nameofclub
        self.distance = distance
        self.time = time
class C2:
    def __init__(self,list):
        self.list = list
    def m1(self,userpace):
        l2 = []
        for i in list:
            pace = (i.distance / i.time )
            if pace > userpace:
                l2.append(i.runnername)
        if len(l2) == 0:
            print("Not Found")
        else:
            for i in l2:
                print(i)



n = int(input())
list= []
for i in range(n):
    runnername = input()
    nameofclub = input()
    distance = int(input())
    time = int(input())
     
    obj1 = C1(runnername,nameofclub,distance,time)
    list.append(obj1)
userpace = int(input())
obj2 = C2(list)
ans = obj2.m1(userpace)



'''
Input:
4
john
barcelona
55
5
Ramu
kkr
60
4
Ravi
cbs
80
5
Lalit
csk
56
6
14

Output:
Ramu
Ravi

'''
```

---

## Practice Problem 36: 7thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Output:
hi

```

### Solution Code:
```python
print("hi")

"""

Output:
hi

"""
```

---

## Practice Problem 37: 9thMarch

### Problem Statement
Design a system to model the entities and implement the required business logic.

### Requirements:
1. Write a program to solve the problem based on the provided input and output format.

### Input / Output Examples:
```
Input:
500 

Output:
4555

Explaination:

4*5*5*5 = 500

```

### Solution Code:
```python
n = int(input())
l = []
if n >9:
    for i in range(9,1,-1):
        while n%i == 0:
            l.append(i)
            n = n/i
        # break
    j = l[::-1]
    s = ''
    for i in j:
        s = s+str(i)
    print(int(s))
else:
    print(n+10)



'''

Input:
500 

Output:
4555

Explaination:

4*5*5*5 = 500

'''
```

---


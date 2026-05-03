# 📚 Complete Learning Guide: UNIX, Python & SQL

## 📑 Table of Contents
1. [UNIX Complete Guide](#unix-complete-guide)
2. [Python Complete Guide](#python-complete-guide)
3. [SQL Complete Guide](#sql-complete-guide)
4. [Interview Questions](#interview-questions)

---

# UNIX Complete Guide

## 🖥️ Operating Systems Fundamentals

### What is an Operating System?
An Operating System is software that manages hardware resources and enables communication between users and the computer.

**Four Basic Components:**
1. **Hardware** – CPU, memory, I/O devices
2. **Operating System** – Controls and coordinates hardware usage
3. **Application Programs** – Define how resources are used
4. **Users** – People who interact with the system

### Types of Operating Systems

| OS Type | Description |
|---------|-------------|
| **Single User, Single Tasking** | One task at a time, one user (e.g., DOS) |
| **Single User, Multitasking** | Multiple tasks/processes by one user |
| **Multi-programming** | Multiple programs run concurrently |
| **Real-Time OS** | Responds to events within predetermined time |
| **Embedded OS** | Built into devices, specific to hardware |

### OS Functions
- Controlling and allocating memory
- Prioritizing system requests
- Controlling input/output devices
- Facilitating networking
- Managing files

---

## 🐧 UNIX Introduction

### What is UNIX?
UNIX is a powerful, portable operating system developed by Ken Thompson and Ritchie, originally written in assembly and later rewritten in C for portability.

**Key Facts:**
- Supports multiple programming languages (C, Fortran, Java, Ada, etc.)
- Open-source and widely used in servers
- Basis for Linux and macOS
- Known for "Do one thing and do it well" philosophy

### Features of UNIX

| Feature | Description |
|---------|-------------|
| **Multi-user** | Multiple users can work simultaneously |
| **Multitasking** | Multiple processes run concurrently |
| **Portability** | Written in C, runs on various platforms |
| **Everything is a File** | Even devices are treated as files |
| **Configuration in Text** | Settings stored in readable text files |
| **Small Programs** | Single-purpose utilities combined for power |
| **Pipe & Filter** | Programs can be chained together |
| **Background Processing** | Tasks run without blocking the terminal |

### UNIX Architecture

```
┌─────────────────────────────────────┐
│          User Interface             │
│      (Shell, Utilities)             │
├─────────────────────────────────────┤
│         System Calls                │
├─────────────────────────────────────┤
│          Kernel                     │
│  (Memory, Process, File Management) │
├─────────────────────────────────────┤
│          Hardware                   │
│  (CPU, Memory, I/O Devices)         │
└─────────────────────────────────────┘
```

### The UNIX Kernel

**Definition:** Collection of C programs managing system resources and computer internals.

**Functions:**
- Allocates time and memory to programs
- Handles file storage and communications
- Interacts with hardware via device drivers
- Provides services to programs
- Manages memory and access control
- Maintains file system
- Handles interrupts and resource allocation

### System Calls
System calls are functions that programs use to request kernel services.

**Categories:**
1. **File-related:** `create`, `open`, `read`, `write`, `lseek`, `dup`
2. **Process-related:** `fork`, `exec`, `wait`, `exit`
3. **Inter-process communication:** `pipe`, `msgget`, `msgsnd`

---

## 📂 UNIX File System

### File System Hierarchy

**Root Directory (/):** The top level of the file system

**Key Directories:**
- `/bin` – Essential binary executable programs
- `/sbin` – System binaries (for administrators)
- `/etc` – Configuration files
- `/home` – User home directories
- `/usr` – User-oriented programs and files
- `/dev` – Device files (terminals, printers, disks)
- `/var` – Variable data (logs, temporary files)
- `/tmp` – Temporary files
- `/root` – Root user's home directory

### File Types

| Type | Description |
|------|-------------|
| **Ordinary Files** | Regular data files, text files, executables |
| **Directory Files** | Contain other files and directories |
| **Special Files** | Device files, pipes, sockets |

### Pathnames

**Absolute Pathname:** File location from root `/`
```bash
/home/user/documents/file.txt
```

**Relative Pathname:** File location from current directory
```bash
documents/file.txt    # if current dir is /home/user
../file.txt          # parent directory
```

### File Naming Rules
- Up to 255 characters (typically)
- Can contain: letters, digits, dot (.), hyphen (-), underscore (_)
- Case-sensitive (file.txt ≠ FILE.txt)
- No spaces (use underscore or hyphen)
- No special characters like *, ?, [, ]

### Inode Structure

An **inode** is a 64-byte disk record maintaining permanent file attributes.

**Inode Contains:**
- Owner and group identifiers
- File type and size
- Number of file links
- Creation, access, and modification times
- Access permissions (read/write/execute)
- Reference count (open file count)
- 13 pointers to data blocks

---

## 👥 Users and Access Rights

### User Types

| User Type | Description | UID |
|-----------|-------------|-----|
| **Root** | System administrator, full permissions | 0 |
| **System** | Special accounts for services | 1-999 |
| **Regular** | Normal users with limited permissions | 1000+ |

### File Permissions

**Three Permission Levels:**

| Level | Owner | Group | Others |
|-------|-------|-------|--------|
| **Symbolic** | u | g | o |

**Three Permission Types:**

| Symbol | Name | File Meaning | Directory Meaning |
|--------|------|--------------|-------------------|
| **r** | Read | View file contents | List directory contents |
| **w** | Write | Modify file | Create/delete files in dir |
| **x** | Execute | Run as program | Enter/access directory |

### Permission Examples

```bash
-rw-r--r--    Regular file, owner can read/write, others read only
drwxr-xr-x    Directory, owner all rights, others can enter
-rwx------    File, only owner can do anything (most secure)
```

### Changing Permissions

**Symbolic Mode:**
```bash
chmod u+x file.txt              # Owner: add execute
chmod g-w file.txt              # Group: remove write
chmod o=r file.txt              # Others: only read
chmod a+r file.txt              # All: add read
```

**Octal Mode:**
```
r = 4, w = 2, x = 1

chmod 755 file.txt    # Owner: 7(rwx), Group: 5(r-x), Others: 5(r-x)
chmod 644 file.txt    # Owner: 6(rw-), Group: 4(r--), Others: 4(r--)
chmod 700 file.txt    # Owner: 7(rwx), Group: 0(---), Others: 0(---)
```

### Groups
- Unix supports grouping of user accounts
- Each user belongs to at least one group
- Groups are useful for managing file permissions collectively
- Group permissions can be granted/revoked for multiple users at once

---

## ⌨️ UNIX Basic Commands

### Directory Navigation

```bash
pwd                    # Print working directory (current location)
cd /path/to/dir       # Change directory
cd ~                  # Go to home directory
cd ..                 # Go to parent directory
cd -                  # Go to previous directory
```

### File and Directory Listing

```bash
ls                    # List files in current directory
ls -l                 # Long format (detailed)
ls -a                 # Show hidden files (. prefix)
ls -la                # Long format + hidden files
ls -R                 # Recursive (show subdirectories)
ls -S                 # Sort by file size
ls -t                 # Sort by modification time
```

### File Viewing and Manipulation

```bash
cat filename          # Display file contents
cat file1 file2       # Display multiple files
more filename         # View file page by page
less filename         # Better than 'more' (scroll backward)
head -n 10 file       # Show first 10 lines
tail -n 10 file       # Show last 10 lines
tail -f logfile       # Follow file (updates in real-time)
```

### File Creation and Editing

```bash
touch file.txt        # Create empty file
cat > file.txt        # Create/overwrite file (Ctrl+D to save)
cat >> file.txt       # Append to file (Ctrl+D to save)
vi filename           # Edit with vi editor
nano filename         # Edit with nano editor
```

### File Operations

```bash
cp source.txt dest.txt        # Copy file
cp -r source_dir dest_dir     # Copy directory recursively
mv oldname.txt newname.txt    # Move/rename file
rm file.txt                   # Delete file
rm -r directory/              # Delete directory and contents
rm -i file.txt                # Delete with confirmation
```

### Directory Operations

```bash
mkdir dirname                 # Create directory
mkdir -p dir1/dir2/dir3      # Create nested directories
rmdir dirname                 # Remove empty directory
rmdir -r dirname             # Remove directory recursively
```

### File Search

```bash
find . -name "*.txt"         # Find files by name
find . -type f               # Find all regular files
find . -type d               # Find all directories
find . -size +10M            # Find files larger than 10MB
find . -mtime -3             # Find files modified in last 3 days
find . -perm 755             # Find files by permission
find . -name "*.txt" -exec rm {} \;  # Find and delete
```

### File Comparison

```bash
diff file1.txt file2.txt     # Show differences between files
cmp file1.txt file2.txt      # Compare files byte by byte
comm file1.txt file2.txt     # Compare sorted files
```

### Information Commands

```bash
whoami                # Current user
who                   # All logged-in users
uname -a             # System information
uname -s             # Kernel name
uname -r             # Kernel release
date                 # Current date and time
echo "text"          # Print text
```

### Text Processing

```bash
wc file.txt          # Count lines, words, characters
wc -l file.txt       # Count lines only
grep "pattern" file  # Search for pattern in file
grep -r "text" .     # Recursive search in directory
tr 'a' 'b' < file    # Translate/replace characters
cut -d: -f1 file     # Extract columns
sort file.txt        # Sort lines
sort -n numbers.txt  # Sort numerically
uniq file.txt        # Remove consecutive duplicates
```

### Disk and Memory

```bash
df                   # Disk space usage
df -h                # Human-readable disk space
du -sh dirname       # Directory size
free                 # Memory usage
top                  # Real-time process monitor
```

### Process Management

```bash
ps                   # List running processes
ps aux               # All processes with details
kill PID             # Terminate process
kill -9 PID          # Force kill process
bg                   # Run job in background
fg                   # Bring job to foreground
jobs                 # List background jobs
```

---

## 🔀 Filters and Pipes

### What is a Filter?
A **filter** is a program that:
1. Takes input from standard input (stdin)
2. Processes the data
3. Sends output to standard output (stdout)

### Common Filters

#### head - First Lines
```bash
head -n 10 file.txt       # First 10 lines (default is 10)
head -c 100 file.txt      # First 100 bytes
cat file | head -5        # First 5 lines via pipe
```

#### tail - Last Lines
```bash
tail -n 10 file.txt       # Last 10 lines
tail -c 100 file.txt      # Last 100 bytes
tail -f logfile.txt       # Follow/monitor file updates
```

#### sort - Sort Lines
```bash
sort file.txt             # Sort alphabetically
sort -n numbers.txt       # Sort numerically
sort -r file.txt          # Reverse sort
sort -u file.txt          # Remove duplicates while sorting
sort -t',' -k2 file.csv   # Sort by 2nd column (comma-separated)
```

#### uniq - Remove Duplicates
```bash
uniq file.txt             # Remove consecutive duplicates
uniq -c file.txt          # Count occurrences
uniq -d file.txt          # Show only duplicates
uniq -u file.txt          # Show only unique lines
```

#### grep - Search Text
```bash
grep "pattern" file.txt   # Find lines containing pattern
grep -i "pattern" file    # Case-insensitive search
grep -v "pattern" file    # Show lines NOT containing pattern
grep -c "pattern" file    # Count matching lines
grep -n "pattern" file    # Show line numbers
grep "^pattern" file      # Lines starting with pattern
grep "pattern$" file      # Lines ending with pattern
```

#### cut - Extract Columns
```bash
cut -c 1-5 file.txt       # Characters 1-5
cut -c 3- file.txt        # From character 3 to end
cut -d: -f1 /etc/passwd   # 1st field (colon-delimited)
cut -d, -f2,3 file.csv    # Columns 2,3 (comma-delimited)
```

#### tr - Translate Characters
```bash
tr 'a' 'b' < file.txt     # Replace 'a' with 'b'
tr 'a-z' 'A-Z' < file     # Convert lowercase to uppercase
tr -d 'a' < file.txt      # Delete all 'a' characters
tr -s ' ' < file.txt      # Squeeze multiple spaces to one
```

#### wc - Word/Line Count
```bash
wc file.txt               # Lines, words, characters
wc -l file.txt            # Count lines only
wc -w file.txt            # Count words only
wc -c file.txt            # Count characters only
```

### Pipes (|)
**Pipe** connects output of one command to input of another.

```bash
cat file.txt | wc -l              # Count lines in file
cat file.txt | grep "pattern"     # Search in file
cat file.txt | sort | uniq        # Sort and remove duplicates
ps aux | grep "python"            # Find python processes
cat file.txt | head -5 | tail -2  # Lines 4-5
```

**Practical Examples:**
```bash
# Find all .txt files with "error" in content
find . -name "*.txt" | xargs grep "error"

# Sort users by login count
who | cut -d' ' -f1 | sort | uniq -c | sort -rn

# Get top 5 largest files
find . -type f -exec ls -lS {} + | head -6
```

---

## 🐚 Shell Scripting

### What is a Shell Script?
A **shell script** is a file containing a sequence of commands to be executed by the shell interpreter.

### Shebang Line
The first line of a shell script specifies which interpreter to use:

```bash
#!/bin/sh        # Use /bin/sh shell (POSIX)
#!/bin/bash      # Use bash shell
#!/bin/ksh       # Use Korn shell
```

### Variables

```bash
# Define variable
name="John"
age=25

# Use variable
echo "Name: $name"
echo "Age: $age"

# Read from user
read -p "Enter your name: " username

# Command substitution
current_date=$(date)
echo "Today is $current_date"
```

### Arithmetic Operators

```bash
# Arithmetic operations
result=$((2 + 3))          # Addition
result=$((10 - 5))         # Subtraction
result=$((4 * 5))          # Multiplication
result=$((20 / 4))         # Division
result=$((20 % 3))         # Modulus (remainder)
```

### Conditional Statements

#### if...fi
```bash
if [ condition ]; then
    echo "Condition is true"
fi
```

#### if...else...fi
```bash
if [ condition ]; then
    echo "True branch"
else
    echo "False branch"
fi
```

#### if...elif...else...fi
```bash
if [ condition1 ]; then
    echo "First condition true"
elif [ condition2 ]; then
    echo "Second condition true"
else
    echo "All conditions false"
fi
```

#### case...esac
```bash
case $variable in
    pattern1)
        echo "Matched pattern1"
        ;;
    pattern2)
        echo "Matched pattern2"
        ;;
    *)
        echo "No match"
        ;;
esac
```

### Comparison Operators

**Numeric Comparison:**
```bash
-eq     # Equal
-ne     # Not equal
-gt     # Greater than
-lt     # Less than
-ge     # Greater than or equal
-le     # Less than or equal

# Example
if [ $age -gt 18 ]; then
    echo "Adult"
fi
```

**String Comparison:**
```bash
=       # Equal
!=      # Not equal
-z      # String is zero length (empty)
-n      # String is non-zero length

# Example
if [ "$name" = "John" ]; then
    echo "Hello John"
fi
```

**File Tests:**
```bash
-f      # File exists and is regular file
-d      # File exists and is directory
-r      # File is readable
-w      # File is writable
-x      # File is executable
-s      # File exists and has size > 0

# Example
if [ -f "$filename" ]; then
    echo "File exists"
fi
```

### Loops

#### while Loop
```bash
counter=1
while [ $counter -le 5 ]; do
    echo "Count: $counter"
    counter=$((counter + 1))
done
```

#### for Loop
```bash
for i in 1 2 3 4 5; do
    echo "Number: $i"
done

# Loop through files
for file in *.txt; do
    echo "Processing $file"
done

# C-style for loop
for ((i=1; i<=5; i++)); do
    echo "Count: $i"
done
```

#### until Loop
```bash
counter=1
until [ $counter -gt 5 ]; do
    echo "Count: $counter"
    counter=$((counter + 1))
done
```

### Functions

```bash
# Define function
greet() {
    echo "Hello, $1!"
}

# Call function
greet "John"

# Function with return value
add() {
    return $((1 + 2))
}

# Function with local variables
calculate() {
    local num1=$1
    local num2=$2
    echo $((num1 + num2))
}

result=$(calculate 5 3)
echo "Sum: $result"
```

### Input/Output

```bash
# Output
echo "Hello"
printf "Name: %s, Age: %d\n" "John" 25

# Input
read name
read -p "Enter age: " age

# Redirection
echo "text" > file.txt      # Write (overwrite)
echo "text" >> file.txt     # Append
command < input.txt         # Read from file
command > output.txt 2>&1   # Redirect stdout and stderr
```

### Environment Variables

```bash
# View all environment variables
env
printenv

# Common variables
$HOME       # Home directory
$USER       # Current user
$PWD        # Current working directory
$PATH       # Search path for commands
$SHELL      # Current shell
$RANDOM     # Random number
$?          # Exit status of last command
```

### Wild Card Characters

| Pattern | Meaning |
|---------|---------|
| `*` | Matches any number of characters |
| `?` | Matches exactly one character |
| `[abc]` | Matches any one of a, b, or c |
| `[a-z]` | Matches any character a through z |
| `[!abc]` | Matches any character except a, b, c |

```bash
ls *.txt              # All .txt files
ls file?.txt          # file1.txt, fileA.txt, etc.
ls [aeiou]*           # Files starting with vowel
ls /bin/[a-c]*        # Files in /bin starting with a, b, or c
```

### Script Example

```bash
#!/bin/bash

# Employee Overtime System
echo "=== Employee Overtime System ==="

# Variables
employee_name="John"
base_salary=50000
overtime_hours=15

# Check overtime eligibility
if [ $overtime_hours -gt 10 ]; then
    overtime_bonus=$((overtime_hours * 500))
    total_salary=$((base_salary + overtime_bonus))
    echo "Employee: $employee_name"
    echo "Overtime Hours: $overtime_hours"
    echo "Overtime Bonus: $overtime_bonus"
    echo "Total Salary: $total_salary"
else
    echo "Employee not eligible for overtime bonus"
fi
```

---

## ⚙️ Process Management and Job Scheduling

### Processes
A **process** is a running instance of a program with:
- Process ID (PID)
- Parent Process ID (PPID)
- Owner (user)
- Priority level
- State (running, sleeping, zombie)
- Resource usage

### Process States

| State | Description |
|-------|-------------|
| **Running** | Currently executing on CPU |
| **Sleeping** | Waiting for I/O or event |
| **Stopped** | Suspended, not executing |
| **Zombie** | Terminated but not cleaned up |
| **Defunct** | Dead but still in process table |

### Process Commands

```bash
ps                    # List current processes
ps aux                # All processes with details
ps -u username        # Processes of specific user
ps -p PID             # Info about specific PID
pgrep pattern         # Find PID by process name
pkill pattern         # Kill process by name
```

### Background and Foreground

```bash
# Run command in background
command &

# Bring background job to foreground
fg %job_number

# Send to background
Ctrl+Z then type: bg

# List background jobs
jobs

# Wait for all background jobs
wait
```

### Priority Management

```bash
# Set priority at startup
nice -n 10 command    # Lower priority (nice value 0-19)
nice -n -10 command   # Higher priority (negative = higher)

# Change running process priority
renice -n 5 -p PID    # Increase nice value
```

### Job Control

```bash
# Schedule command to run later
at 14:30
at> command
at> Ctrl+D

# Schedule recurring commands
crontab -e            # Edit cron jobs
# Format: minute hour day month weekday command
0 2 * * * /backup.sh  # Run backup at 2 AM daily
*/5 * * * * check.sh  # Run check every 5 minutes
```

---

## 📝 VI Editor Guide

### Modes in VI

| Mode | Description | How to Enter |
|------|-------------|--------------|
| **Command Mode** | Execute commands | Press Esc (default) |
| **Insert Mode** | Edit text | Press `i`, `a`, `o`, etc. |
| **Ex Mode** | Line commands | Press `:` from command mode |

### Starting VI

```bash
vi filename           # Open/create file
vi +10 filename       # Open at line 10
vi +/pattern file     # Open and search for pattern
vi -R filename        # Open read-only
```

### Moving Around (Command Mode)

```bash
h, j, k, l           # Left, down, up, right (or arrows)
w                    # Next word
b                    # Previous word
0                    # Start of line
$                    # End of line
G                    # End of file
1G                   # Start of file
nG                   # Go to line n
```

### Inserting Text (Enter Insert Mode)

```bash
i                    # Insert before cursor
I                    # Insert at start of line
a                    # Append after cursor
A                    # Append at end of line
o                    # New line below
O                    # New line above
```

### Deleting Text (Command Mode)

```bash
x                    # Delete character under cursor
dw                   # Delete word
dd                   # Delete entire line
d$                   # Delete to end of line
d0                   # Delete to start of line
```

### Copying and Pasting

```bash
yy                   # Copy (yank) current line
yw                   # Copy word
p                    # Paste after cursor
P                    # Paste before cursor
```

### Searching

```bash
/pattern             # Search forward
?pattern             # Search backward
n                    # Next match
N                    # Previous match
:%s/old/new/g        # Replace all old with new
```

### Saving and Exiting (Ex Mode)

```bash
:w                   # Save (write)
:w filename          # Save as
:q                   # Quit
:q!                  # Quit without saving
:wq                  # Save and quit
:x                   # Save and quit (same as :wq)
```

---

# Python Complete Guide

## 🐍 Python Basics

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

## 🏗️ Object-Oriented Programming (OOP)

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

## 📚 File Handling

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

## 🔧 Common Libraries

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

# SQL Complete Guide

## 📊 SQL Basics

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

## 📝 CRUD Operations

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

## 🔍 Advanced SELECT

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

## 🔐 Data Integrity and Constraints

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

## 🔨 Useful SQL Functions

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

## 📚 Views and Indexes

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

## 🔄 Transactions

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
    - BIOS → Bootloader → Kernel → Init → User login

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

## 🚀 Study Tips

1. **UNIX**: Practice commands daily, understand pipes and filters
2. **Python**: Write code regularly, focus on data structures and OOP
3. **SQL**: Design schemas, write complex queries, understand joins

---

## 📖 Quick Reference

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

## 📞 Support and Resources

- UNIX Documentation: `man command_name`
- Python Official Docs: https://docs.python.org/3/
- SQL Tutorials: https://www.w3schools.com/sql/
- Online IDE: Repl.it, LeetCode, HackerRank

---

**Last Updated:** May 3, 2026

This comprehensive guide covers the fundamentals and advanced concepts of UNIX, Python, and SQL. Use it as a reference for learning, interviews, and problem-solving!

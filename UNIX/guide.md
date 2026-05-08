# UNIX Complete Guide

## ðŸ–¥ï¸ Operating Systems Fundamentals

### What is an Operating System?
An Operating System is software that manages hardware resources and enables communication between users and the computer.

**Four Basic Components:**
1. **Hardware** â€“ CPU, memory, I/O devices
2. **Operating System** â€“ Controls and coordinates hardware usage
3. **Application Programs** â€“ Define how resources are used
4. **Users** â€“ People who interact with the system

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

## ðŸ§ UNIX Introduction

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
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚          User Interface             â”‚
â”‚      (Shell, Utilities)             â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚         System Calls                â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚          Kernel                     â”‚
â”‚  (Memory, Process, File Management) â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚          Hardware                   â”‚
â”‚  (CPU, Memory, I/O Devices)         â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
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

## ðŸ“‚ UNIX File System

### File System Hierarchy

**Root Directory (/):** The top level of the file system

**Key Directories:**
- `/bin` â€“ Essential binary executable programs
- `/sbin` â€“ System binaries (for administrators)
- `/etc` â€“ Configuration files
- `/home` â€“ User home directories
- `/usr` â€“ User-oriented programs and files
- `/dev` â€“ Device files (terminals, printers, disks)
- `/var` â€“ Variable data (logs, temporary files)
- `/tmp` â€“ Temporary files
- `/root` â€“ Root user's home directory

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
- Case-sensitive (file.txt â‰  FILE.txt)
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

## ðŸ‘¥ Users and Access Rights

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

## âŒ¨ï¸ UNIX Basic Commands

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

## ðŸ”€ Filters and Pipes

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

## ðŸš Shell Scripting

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

## âš™ï¸ Process Management and Job Scheduling

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

## ðŸ“ VI Editor Guide

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

Complete AWK Functions Guide - Zero to Advanced

Table of Contents

1. Introduction to AWK
2. String Functions (Complete)
3. Math Functions (Complete)
4. Array Functions (Complete)
5. I/O Functions (Complete)
6. Time Functions
7. Bit Manipulation Functions
8. Type Conversion Functions
9. Special Variables
10. Practical Examples

---

Introduction to AWK

AWK is a pattern-directed scanning and processing language. Named after creators: Aho, Weinberger, Kernighan.

Basic Structure

```bash
awk 'BEGIN { initialization } pattern { action } END { cleanup }' file
```

Running AWK

```bash
# Method 1: Command line
awk '{print $1}' file.txt

# Method 2: From script
awk -f script.awk file.txt

# Method 3: One-liner with variables
awk -v var=10 '{print $1 * var}' file.txt
```

---

String Functions (Complete)

1. length() - Get string length

```bash
# Basic usage
awk '{print length($0)}' file.txt  # Length of each line
awk '{print length($1)}' file.txt  # Length of first field

# With variable
awk '{len = length($2); print "Field 2 has", len, "characters"}'

# Count empty lines
awk 'length($0) == 0 {count++} END {print "Empty lines:", count}' file.txt

# Validate minimum length
awk 'length($1) >= 5 {print $1}' file.txt

# Characters per word
awk '{for(i=1;i<=NF;i++) print length($i)}' file.txt
```

2. substr(s, start, length) - Extract substring

```bash
# Extract from position to end
awk '{print substr($1, 3)}' file.txt  # From 3rd char to end
awk '{print substr($1, 2, 5)}' file.txt  # 5 chars from position 2

# Get first 3 characters
awk '{print substr($0, 1, 3)}' file.txt

# Get last 3 characters
awk '{print substr($0, length($0)-2)}' file.txt

# Extract domain from email
awk '{print substr($1, index($1,"@")+1)}' emails.txt

# Extract based on positions
echo "John Doe 30" | awk '{name = substr($0, 1, 8); age = substr($0, 9); print name, age}'

# Dynamic extraction
awk '{start = index($0, "error"); if(start) print substr($0, start)}' log.txt
```

3. index(s, t) - Find position of substring

```bash
# Find position (returns 1-based index)
awk '{print index($0, "error")}' file.txt

# Check if string contains pattern
awk 'index($0, "warning") > 0 {print NR, $0}' file.txt

# Extract after a specific pattern
awk '{
    pos = index($0, "=");
    if(pos > 0) print substr($0, pos+1)
}' config.txt

# Multiple occurrences (find all positions)
awk '{
    line = $0;
    pattern = "a";
    pos = 1;
    while(pos = index(line, pattern)) {
        print "Found at:", pos;
        line = substr(line, pos+1);
    }
}' file.txt

# Extract between two patterns
awk '{
    start = index($0, "[");
    end = index($0, "]");
    if(start && end && end > start) {
        print substr($0, start+1, end-start-1)
    }
}' file.txt
```

4. split(s, array, delimiter) - Split string into array

```bash
# Basic split on space
awk '{split($0, arr, " "); print arr[1]}' file.txt

# Split on comma
awk '{split($0, fields, ","); print fields[1], fields[3]}' csvfile.txt

# Split with regex delimiter
awk '{split($0, parts, /[ ,;:]+/); print parts[2]}' file.txt

# Count number of fields after split
awk '{n = split($0, arr, ","); print "CSV has", n, "fields"}'

# Split and loop
awk '{
    split($0, words, " ");
    for(i in words)
        print i ":", words[i]
}'

# Split multiple times
awk '{
    split($1, first, "-");
    split($2, last, "-");
    print first[1], last[1]
}'

# Split into array and use length
awk '{n = split($0, arr, " "); for(i=1;i<=n;i++) print arr[i]}'

# Preserve split count
awk '{n = split($0, arr); for(i=1;i<=n;i++) if(arr[i] ~ /^[A-Z]/) print arr[i]}'

# Split with empty fields preserved
echo "a,,b,c" | awk '{n = split($0, arr, ",", seps); for(i=1;i<=n;i++) print arr[i]}'
```

5. tolower(string) - Convert to lowercase

```bash
# Case-insensitive comparison
awk 'tolower($1) == "admin" {print $0}' file.txt

# Standardize data
awk '{$1 = tolower($1); print}' file.txt

# Convert whole line
awk '{print tolower($0)}' file.txt

# Case-insensitive search
awk 'tolower($0) ~ /error/ {print}' log.txt

# Convert first character only
awk '{print toupper(substr($1,1,1)) tolower(substr($1,2))}' names.txt

# Create index keys
awk '{key = tolower($1); data[key] = $0} END {for(k in data) print k, data[k]}'
```

6. toupper(string) - Convert to uppercase

```bash
# Convert field to uppercase
awk '{$3 = toupper($3); print}' file.txt

# Make CSV headers uppercase
awk 'NR==1 {for(i=1;i<=NF;i++) $i = toupper($i)} {print}' data.csv

# Generate SQL query
awk '{print "INSERT INTO users VALUES("\"" toupper($1) "\", " $2 ");"}' users.txt

# Environment variable style
awk '{print toupper($1) "=" $2}' config.txt
```

7. sub(regex, replacement, target) - Replace first match

```bash
# Replace first occurrence
awk '{sub("old", "new"); print}' file.txt

# Replace in specific field
awk '{sub(/old/, "new", $2); print}' file.txt

# Conditional replace
awk '/pattern/ {sub(/old/, "new")} {print}' file.txt

# Count replacements
awk '{count += sub(/a/, "b"); print} END {print count}' file.txt

# Replace with variable
awk -v old="foo" -v new="bar" '{sub(old, new); print}' file.txt

# Use capture groups
awk '{sub(/([0-9]+)/, "NUM_\\1"); print}' file.txt

# Replace first word only
awk '{sub(/^[a-zA-Z]+/, "WORD"); print}' file.txt
```

8. gsub(regex, replacement, target) - Replace all matches

```bash
# Replace globally
awk '{gsub(/[0-9]/, "#"); print}' file.txt

# Remove all spaces
awk '{gsub(/ /, ""); print}' file.txt

# Replace multiple patterns
awk '{gsub(/[[:punct:]]/, ""); print}' file.txt

# Count total replacements
awk '{count += gsub(/[aeiou]/, "X"); print} END {print "Vowels replaced:", count}'

# Collapse multiple spaces
awk '{gsub(/ +/, " "); print}' file.txt

# Escape special characters
awk '{gsub(/\./, "_"); print}' filenames.txt

# Replace in array
awk '{
    split($0, arr, " ");
    for(i in arr) gsub(/[^0-9]/, "", arr[i]);
    print arr[1], arr[2]
}'

# Remove HTML tags
awk '{gsub(/<[^>]*>/, ""); print}' webpage.html

# Clean CSV fields
awk '{gsub(/^"|"$/, "", $1); gsub(/^"|"$/, "", $2); print}' data.csv
```

9. match(string, regex, array) - Regular expression match

```bash
# Check if matches
awk 'match($0, /error/) {print "Found error at line", NR}'

# Get match position and length
awk '{
    if(match($0, /[0-9]+/)) {
        print "Match at:", RSTART;
        print "Length:", RLENGTH;
        print "Value:", substr($0, RSTART, RLENGTH);
    }
}'

# Extract capture groups with array
awk '{
    match($0, /([a-z]+)=([0-9]+)/, arr);
    print "Key:", arr[1];
    print "Value:", arr[2];
}'

# Extract email addresses
awk '{
    while(match($0, /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/)) {
        print substr($0, RSTART, RLENGTH);
        $0 = substr($0, RSTART+RLENGTH);
    }
}'

# Extract IP addresses
awk 'match($0, /[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/) {
    ip = substr($0, RSTART, RLENGTH);
    print "IP:", ip;
}'

# Extract quoted strings
awk '{
    while(match($0, /"[^"]*"/)) {
        print substr($0, RSTART+1, RLENGTH-2);
        $0 = substr($0, RSTART+RLENGTH);
    }
}'

# Multiple matches with positions
awk '{
    pos = 1;
    line = $0;
    while(match(line, /[aeiou]/)) {
        print "Vowel at global position:", pos + RSTART - 1;
        pos += RSTART;
        line = substr(line, RSTART+RLENGTH);
    }
}'
```

10. sprintf(format, expr1, expr2...) - Format string

```bash
# Number formatting
awk '{num = sprintf("%05d", $1); print num}' file.txt

# Floating point precision
awk '{val = sprintf("%.2f", $1/3); print val}' file.txt

# Hexadecimal conversion
awk '{hex = sprintf("0x%X", $1); print hex}' file.txt

# Build formatted output
awk '{
    line = sprintf("%-10s %3d %8.2f", $1, $2, $3);
    print line
}'

# Create filenames
awk '{filename = sprintf("data_%04d.txt", NR); print filename > filename}'

# SQL insert statements
awk '{sql = sprintf("INSERT INTO table VALUES('\''%s'\'', %d);", $1, $2); print sql}'

# JSON output
awk '{
    json = sprintf("{\"name\":\"%s\",\"age\":%d}", $1, $2);
    print json
}'

# Left and right alignment
awk '{print sprintf("%-20s %20s", $1, $2)}' file.txt

# Format with leading zeros
awk '{print sprintf("%03d-%02d-%04d", $1, $2, $3)}' dates.txt

# Scientific notation
awk '{print sprintf("%10.2e", $1)}' numbers.txt
```

11. strtonum(str) - Convert string to number

```bash
# Convert hex string
awk '{num = strtonum("0x" $1); print num}' hex.txt

# Convert octal
awk '{num = strtonum("0" $1); print num}' octal.txt

# Handle different number formats
awk '{
    if($1 ~ /^0x/) print strtonum($1);
    else if($1 ~ /^0/) print strtonum($1);
    else print $1 + 0;
}'

# Auto-detect and convert
awk '{sum += strtonum($1)} END {print sum}'
```

12. asort(s, d) - Sort array by value

```bash
# Sort array values
awk '{
    arr[NR] = $1
}
END {
    n = asort(arr)
    for(i=1;i<=n;i++) print arr[i]
}'

# Sort with original indices lost
awk '{
    a[NR] = $1
}
END {
    n = asort(a, b)
    for(i=1;i<=n;i++) print i, b[i]
}'

# Sort strings
awk '{
    words[$1] = length($1)
}
END {
    n = asort(words)
    for(i=1;i<=n;i++) print words[i]
}'
```

13. asorti(s, d) - Sort array by index

```bash
# Sort by key
awk '{
    data[$1] = $2
}
END {
    n = asorti(data, sorted)
    for(i=1;i<=n;i++) print sorted[i], data[sorted[i]]
}'

# Reverse sort (by index)
awk '{
    data[$1] = $2
}
END {
    n = asorti(data, sorted)
    for(i=n;i>=1;i--) print sorted[i], data[sorted[i]]
}'
```

---

Math Functions (Complete)

1. sqrt(x) - Square root

```bash
# Basic sqrt
awk '{print sqrt($1)}' numbers.txt

# Pythagorean theorem
awk '{c = sqrt($1^2 + $2^2); print c}'

# Check perfect squares
awk 'sqrt($1) == int(sqrt($1)) {print $1, "is perfect square"}'

# Distance between points
awk '{dist = sqrt(($2-$1)^2 + ($4-$3)^2); print dist}'

# Standard deviation
awk '{
    sum += $1; sum_sq += $1^2; n++
}
END {
    mean = sum/n;
    sd = sqrt((sum_sq - (sum^2)/n)/(n-1));
    print "Mean:", mean, "SD:", sd
}'
```

2. rand() - Random number (0 to 1)

```bash
# Generate random number
awk 'BEGIN{print rand()}'

# Need srand for different values
awk 'BEGIN{srand(); print rand()}'

# Random integer between 1 and 100
awk 'BEGIN{srand(); print int(rand() * 100) + 1}'

# Randomly sample lines
awk 'BEGIN{srand()} rand() < 0.1 {print}' largefile.txt

# Generate random password
awk 'BEGIN{
    srand();
    chars = "abcdefghijklmnopqrstuvwxyz0123456789";
    len = length(chars);
    for(i=1;i<=8;i++) {
        printf substr(chars, int(rand() * len) + 1, 1);
    }
    print "";
}'

# Random shuffle lines
awk 'BEGIN{srand()} {print rand(), $0}' file.txt | sort -n | cut -d' ' -f2-

# Monte Carlo pi approximation
awk 'BEGIN{
    srand();
    n=1000000;
    for(i=1;i<=n;i++) {
        x=rand(); y=rand();
        if(x*x + y*y <= 1) count++;
    }
    pi=4*count/n;
    print pi
}'
```

3. srand([expr]) - Set random seed

```bash
# Seed with time
awk 'BEGIN{srand(); print rand()}'

# Seed with specific value for reproducible results
awk 'BEGIN{srand(42); print rand(); print rand()}'

# Seed with process ID
awk 'BEGIN{srand(12345); for(i=1;i<=5;i++) print rand()}'

# Generate same sequence
awk 'BEGIN{srand(1); for(i=1;i<=3;i++) print rand()}'
awk 'BEGIN{srand(1); for(i=1;i<=3;i++) print rand()}'  # Same output

# Random without seed (not recommended)
awk 'BEGIN{for(i=1;i<=5;i++) print rand()}'  # Same each run
```

4. int(x) - Integer part (truncates toward zero)

```bash
# Truncate decimal
awk '{print int($1)}' numbers.txt

# Floor (int works like floor for positive numbers)
awk '{print int($1)}'

# Integer division
awk '{result = int($1 / $2); print result}'

# Round to nearest integer
awk '{rounded = int($1 + 0.5); print rounded}'

# Check if integer
awk 'int($1) == $1 {print $1, "is integer"}'

# Extract whole and fractional parts
awk '{whole = int($1); fraction = $1 - whole; print whole, fraction}'

# Modulo with int
awk '{result = $1 - int($1/5)*5; print result}'
```

5. sin(x) - Sine (x in radians)

```bash
# Basic sine
awk '{print sin($1)}' angles.txt

# Sine degrees conversion
awk '{rad = $1 * 3.14159/180; print sin(rad)}' degrees.txt

# Wave generation
awk 'BEGIN{for(i=0;i<=360;i+=10) print i, sin(i*3.14159/180)}'

# Fourier transform simulation
awk '{
    for(f=1;f<=10;f++) {
        magnitude[f] += $1 * sin(f * $2 * 3.14159/180);
    }
}
END {
    for(f=1;f<=10;f++) print f, magnitude[f]
}'
```

6. cos(x) - Cosine (x in radians)

```bash
# Basic cosine
awk '{print cos($1)}'

# Law of cosines
awk '{c = sqrt($1^2 + $2^2 - 2*$1*$2*cos($3)); print c}'

# Dot product
awk '{dot = $1*$3 + $2*$4; norm = sqrt($1^2+$2^2)*sqrt($3^2+$4^2);
      cos_angle = dot/norm; print cos_angle}'

# Generate cosine wave
awk 'BEGIN{for(i=0;i<=360;i+=10) print i, cos(i*3.14159/180)}'
```

7. atan2(y, x) - Arc tangent (returns radians)

```bash
# Calculate angle from coordinates
awk '{angle = atan2($2, $1) * 180/3.14159; print angle}'

# Cartesian to polar
awk '{r = sqrt($1^2 + $2^2); theta = atan2($2, $1); print r, theta}'

# Direction between points
awk '{dx = $3-$1; dy = $4-$2; heading = atan2(dy, dx); print heading}'

# Slope to angle
awk '{angle = atan2($2, 1) * 180/3.14159; print "Slope", $1, "=", angle, "degrees"}'
```

8. log(x) - Natural logarithm (base e)

```bash
# Natural log
awk '{print log($1)}' numbers.txt

# Log base 10
awk '{print log($1)/log(10)}' numbers.txt

# Log base 2
awk '{print log($1)/log(2)}' numbers.txt

# Exponential growth
awk '{growth = exp(log($1) * $2); print growth}'

# Entropy calculation
awk '{sum+=$1} END {
    for(i in data) {
        p = data[i]/sum;
        entropy -= p * log(p)/log(2);
    }
    print entropy
}'
```

9. exp(x) - Exponential (e^x)

```python
# Basic exponential
awk '{print exp($1)}' numbers.txt

# Compound interest
awk '{amount = $1 * exp($2 * $3); print "$" amount}' # P, rate, time

# Normal distribution
awk '{x = $1; pdf = (1/sqrt(2*3.14159)) * exp(-x*x/2); print pdf}'

# Logistic function
awk '{logistic = 1/(1+exp(-$1)); print logistic}'
```

10. Additional Math Operations

```bash
# No built-in pow, use ** or ^
awk '{print $1 ** 2}'  # Square
awk '{print $1 ^ 3}'   # Cube

# Absolute value (no built-in, use ternary)
awk '{abs = ($1 < 0) ? -$1 : $1; print abs}'

# Min/Max (no built-in)
awk '{min = ($1 < min) ? $1 : min; max = ($1 > max) ? $1 : max} END {print min, max}'

# Rounding (no built-in)
awk '{rounded = int($1 + 0.5); print rounded}'

# Ceiling (no built-in)
awk '{ceil = ($1 > int($1)) ? int($1)+1 : $1; print ceil}'

# Floor (use int for positive, otherwise adjust)
awk '{floor = ($1 >= 0) ? int($1) : int($1)-1; print floor}'

# Factorial implementation
awk 'function fact(n) {return n<=1 ? 1 : n*fact(n-1)} {print fact($1)}'

# Fibonacci
awk 'function fib(n) {return n<=1 ? n : fib(n-1)+fib(n-2)} {print fib($1)}'
```

---

Array Functions (Complete)

1. Using Arrays

```bash
# Associative arrays (any index type)
awk '{count[$1]++} END {for(name in count) print name, count[name]}'

# Numeric arrays
awk '{
    arr[NR] = $1
}
END {
    for(i=1;i<=NR;i++) print arr[i]
}'

# Multi-dimensional (simulated with string concatenation)
awk '{matrix[$1","$2] = $3} END {print matrix["1,2"]}'

# Check if key exists
awk '{
    if("admin" in users) print "admin exists";
    else print "not found"
}'

# Delete element
awk '{delete arr[$1]} END {for(i in arr) print i}'

# Delete entire array
awk '{delete arr} END {print length(arr)}'
```

2. split() - Already covered in string functions

```bash
# Separator preservation
awk '{n = split($0, arr, /[ ,]+/, seps); for(i=1;i<=n;i++) print arr[i], seps[i]}'

# Split with regex
awk '{n = split($0, arr, /[[:space:]]+/); print arr[2]}'

# Split into named array
awk '{
    split($0, fields, "|");
    name = fields[1];
    age = fields[2];
    print name, age
}'
```

3. length(array) - Get array size

```bash
# Count unique values
awk '{unique[$1]++} END {print "Unique:", length(unique)}'

# Check if array empty
awk '{count[$1]++} END {if(length(count)==0) print "No data"}'
```

4. delete - Remove array elements

```bash
# Delete single element
awk '{arr[$1] = $2} END {delete arr["old"]; for(i in arr) print i}'

# Delete entire array
awk '{arr[$1] = $2} END {delete arr; print length(arr)}'

# Conditional deletion
awk '{
    arr[NR] = $1
}
END {
    for(i in arr) if(arr[i] < 0) delete arr[i]
    for(i in arr) print arr[i]
}'
```

---

I/O Functions (Complete)

1. print - Output

```bash
# Basic print
awk '{print}' file.txt
awk '{print $0}' file.txt

# Print with separator
awk '{print $1, $2}' file.txt  # Space separator
awk '{print $1 "," $2}' file.txt  # No separator

# Print with literal text
awk '{print "Name:", $1, "Age:", $2}'

# Print to file
awk '{print $0 > "output.txt"}' file.txt

# Append to file
awk '{print $0 >> "log.txt"}' file.txt

# Print to different files based on condition
awk '{print > ($1 ~ /^A/ ? "a.txt" : "other.txt")}' file.txt
```

2. printf - Formatted output

```bash
# Format specifiers
awk '{printf "%s\n", $1}' file.txt
awk '{printf "%-10s %5d %8.2f\n", $1, $2, $3}'

# Escape characters
awk '{printf "Line %d:\t%s\n", NR, $0}'

# Dynamic width
awk '{width = length($1); printf "%*s\n", width+2, $1}'

# Print without newline
awk '{printf "Processing..."; printf "done\n"}'

# Hexadecimal
awk '{printf "0x%X\n", $1}'

# Octal
awk '{printf "0%o\n", $1}'

# Scientific notation
awk '{printf "%10.2e\n", $1}'

# Right align
awk '{printf "%10s\n", $1}'

# Left align
awk '{printf "%-10s\n", $1}'

# Zero padding
awk '{printf "%05d\n", $1}'

# Plus sign for positive numbers
awk '{printf "%+d\n", $1}'
```

3. getline - Read next line (advanced)

```bash
# Basic getline
awk '{getline; print $0}' file.txt  # Skip every other line

# Getline into variable
awk '{getline line; print "Previous:", $0, "Next:", line}'

# Getline from file
awk 'BEGIN {while(getline < "data.txt") count++} END {print count}'

# Getline with pipe
awk 'BEGIN {while("ls" | getline) print "File:", $0}'

# Check return value
awk '{
    if((getline) <= 0) print "End of file or error"
}'

# Multiple file processing
awk '{
    if(NR%10==0) getline < "extra.txt";
    print
}'

# Error handling
awk '{
    rc = getline;
    if(rc == 0) print "EOF";
    else if(rc < 0) print "Error";
    else print $0
}'
```

4. close() - Close file or pipe

```bash
# Close output file
awk '{print > "temp.txt"; if(NR%1000==0) close("temp.txt")}' bigfile.txt

# Close input file
awk 'FNR==1 {close("temp.txt")} {print > "temp.txt"}'

# Close pipe
awk '{print | "sort"; close("sort")}' file.txt

# System resource management
awk '{
    for(i=1;i<=NF;i++) {
        cmd = "md5sum " $i;
        cmd | getline hash;
        close(cmd);
        print $i, hash
    }
}'
```

5. fflush() - Flush buffer

```bash
# Force output
awk '{print; fflush()}' file.txt

# Flush specific file
awk '{print > "out.txt"; fflush("out.txt")}'

# Flush all
awk '{print; fflush()}' largefile.txt

# Real-time monitoring
awk '{print strftime(), $0; fflush()}' logfile.txt
```

6. system() - Execute system command

```bash
# Run command
awk 'BEGIN{system("date")}'

# Use system output (better to use getline)
awk '{system("echo Processed: " $0)}'

# Check command status
awk '{
    rc = system("test -f " $1);
    if(rc == 0) print $1, "exists";
    else print $1, "missing"
}'

# Create directories
awk '{
    system("mkdir -p " $1 "/backup");
    print "Created directory for", $1
}'

# Copy files
awk '{
    cmd = "cp " $1 " " $2;
    if(system(cmd) == 0) print "Copied", $1, "to", $2
}'

# Multiple commands
awk '{
    cmd = "convert " $1 " -resize 50% resized_" $1;
    system(cmd);
    print "Processed", $1
}' images.txt
```

---

Time Functions (GNU AWK)

1. systime() - Current Unix timestamp

```bash
# Get timestamp
awk 'BEGIN{print systime()}'

# Measure execution time
awk 'BEGIN{start=systime()} {count++} END{print "Time:", systime()-start, "seconds"}'

# Add timestamps to lines
awk '{print systime(), $0}' log.txt
```

2. strftime([format[, timestamp]]) - Format time

```bash
# Current date/time
awk 'BEGIN
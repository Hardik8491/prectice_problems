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


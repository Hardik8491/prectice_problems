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
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚      User Interface (Shell)          â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚      System Calls                    â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚   Kernel (Resource Management)       â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚   Hardware (CPU, Memory, I/O)        â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
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


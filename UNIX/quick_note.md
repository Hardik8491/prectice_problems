# 📘 UNIX & Shell Scripting Notes

---

# 🧩 1. Introduction to UNIX

## 🔹 What is UNIX?

* Multi-user, multi-tasking OS
* Stable, secure, used in servers

## 🔹 Key Features

* Multi-user support
* File system hierarchy
* Powerful command-line tools
* Shell scripting

---

# 🖥️ 2. Basic UNIX Commands

## 🔸 File & Directory Commands

```bash
pwd        # present working directory
ls         # list files
ls -l      # long listing
ls -a      # hidden files
cd dir     # change directory
mkdir dir  # create directory
rmdir dir  # remove empty directory
```

---

## 🔸 File Operations

```bash
touch file.txt     # create file
cp a.txt b.txt     # copy file
mv a.txt b.txt     # rename/move
rm file.txt        # delete file
cat file.txt       # display content
less file.txt      # paginated view
head file.txt      # first 10 lines
tail file.txt      # last 10 lines
```

---

## 🔸 Permissions

```bash
chmod 755 file.sh
```

| Number | Permission |
| ------ | ---------- |
| 7      | rwx        |
| 6      | rw-        |
| 5      | r-x        |

---

# 🔍 3. Filters in UNIX

## 🔹 grep

```bash
grep "error" file.txt
grep -i "error" file.txt   # case-insensitive
grep -n "error" file.txt   # line number
```

---

## 🔹 sort

```bash
sort file.txt
sort -r file.txt   # reverse
sort -n file.txt   # numeric
```

---

## 🔹 uniq

```bash
uniq file.txt
sort file.txt | uniq
uniq -c file.txt   # count
```

---

## 🔹 wc

```bash
wc file.txt
wc -l file.txt   # lines
wc -w file.txt   # words
wc -c file.txt   # characters
```

---

## 🔹 cut

```bash
cut -d "," -f1 file.csv
```

---

## 🔹 paste

```bash
paste file1 file2
```

---

## 🔹 tr

```bash
tr 'a-z' 'A-Z' < file.txt
```

---

# 🔥 4. AWK (Important)

## 🔹 Basics

```bash
awk '{print $1}' file.txt
```

| Symbol | Meaning     |
| ------ | ----------- |
| $0     | full line   |
| $1,$2  | columns     |
| $NF    | last column |

---

## 🔹 Special Variables

```bash
NR  # line number
NF  # number of fields
FS  # field separator
RS  # record separator
```

---

## 🔹 Example

```bash
awk -F "," '{print $1, $NF}' file.csv
```

---

## 🔹 Remove duplicates

```bash
awk '!seen[$0]++' file.txt
```

---

# 🔧 5. sed (Stream Editor)

## 🔹 Replace text

```bash
sed 's/old/new/' file.txt
sed 's/old/new/g' file.txt
```

---

## 🔹 Delete line

```bash
sed '2d' file.txt
```

---

## 🔹 Print specific line

```bash
sed -n '2p' file.txt
```

---

# 🐚 6. Shell Scripting Basics

## 🔹 What is Shell Script?

* File containing commands executed sequentially

---

## 🔹 First Script

```bash
#!/bin/bash
echo "Hello World"
```

Run:

```bash
chmod +x script.sh
./script.sh
```

---

# 🔤 7. Variables

```bash
name="Hardik"
echo $name
```

---

# 🔢 8. Input from User

```bash
read name
echo "Hello $name"
```

---

# 🔀 9. Conditional Statements

## 🔹 if

```bash
if [ $a -gt 10 ]
then
  echo "Greater"
fi
```

---

## 🔹 if-else

```bash
if [ $a -gt 10 ]
then
  echo "Greater"
else
  echo "Smaller"
fi
```

---

## 🔹 Operators

| Operator | Meaning   |
| -------- | --------- |
| -eq      | equal     |
| -ne      | not equal |
| -gt      | greater   |
| -lt      | less      |

---

# 🔁 10. Loops

## 🔹 for loop

```bash
for i in 1 2 3
do
  echo $i
done
```

---

## 🔹 while loop

```bash
i=1
while [ $i -le 5 ]
do
  echo $i
  ((i++))
done
```

---

# 🧮 11. Functions

```bash
function greet() {
  echo "Hello"
}
greet
```

---

# 📂 12. File Testing

```bash
-f file.txt   # file exists
-d dir        # directory exists
```

---

# 🔗 13. Pipes & Redirection

## 🔹 Pipe

```bash
cat file.txt | grep "error"
```

---

## 🔹 Redirection

```bash
>   # overwrite
>>  # append
<   # input
```

---

# ⚡ 14. Process Commands

```bash
ps        # show processes
top       # live processes
kill PID  # kill process
```

---

# 🔥 15. Important One-Liners

```bash
awk '{print $NF}' file.txt          # last column
awk 'NR % 2 == 1' file.txt          # odd lines
sort file.txt | uniq                # remove duplicates
grep -i "error" file.txt            # search
```

---

# 🚀 16. Interview Tips

* `awk` → data processing
* `sed` → text editing
* `grep` → searching
* `sort + uniq` → duplicates
* `$NF` → last column

---

# 🧠 Final Summary

| Tool | Use              |
| ---- | ---------------- |
| grep | search           |
| awk  | processing       |
| sed  | edit             |
| sort | arrange          |
| uniq | remove duplicate |

---

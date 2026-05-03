# UNIX Problems (with Solutions)

Here are practical UNIX problems commonly asked in technical interviews and assessments:

---

## ❓ 1. Print lines containing "error"

```bash
grep "error" file.txt
```

👉 Case-insensitive:

```bash
grep -i "error" file.txt
```

---

## ❓ 2. Count number of lines, words, characters

```bash
wc file.txt
```

👉 Only lines:

```bash
wc -l file.txt
```

---

## ❓ 3. Print first column

```bash
awk '{print $1}' file.txt
```

---

## ❓ 4. Print last column

```bash
awk '{print $NF}' file.txt
```

---

## ❓ 5. Print lines where salary > 5000

```bash
awk '$3 > 5000' file.txt
```

---

## ❓ 6. Remove duplicate lines

```bash
sort file.txt | uniq
```

👉 OR (better):

```bash
awk '!seen[$0]++' file.txt
```

---

## ❓ 7. Count duplicate occurrences

```bash
sort file.txt | uniq -c
```

---

## ❓ 8. Replace word in file

```bash
sed 's/old/new/g' file.txt
```

---

## ❓ 9. Print specific line (e.g., line 3)

```bash
sed -n '3p' file.txt
```

---

## ❓ 10. Print odd lines

```bash
awk 'NR % 2 == 1' file.txt
```

---

## ❓ 11. Sort file numerically

```bash
sort -n file.txt
```

---

## ❓ 12. Extract column from CSV

```bash
awk -F "," '{print $2}' file.csv
```

---

## ❓ 13. Print top 5 lines

```bash
head -5 file.txt
```

---

## ❓ 14. Print last 5 lines

```bash
tail -5 file.txt
```

---

## ❓ 15. Find pattern with line number

```bash
grep -n "error" file.txt
```

---

## ❓ 16. Count number of files in directory

```bash
ls | wc -l
```

---

## ❓ 17. Print only unique values from column

```bash
awk '{print $1}' file.txt | sort | uniq
```

---

## ❓ 18. Sum of column

```bash
awk '{sum += $3} END {print sum}' file.txt
```

---

## ❓ 19. Find largest number in column

```bash
awk 'max < $3 {max = $3} END {print max}' file.txt
```

---

## ❓ 20. Delete blank lines

```bash
sed '/^$/d' file.txt
```

---

# Most Important Topics

These 5 are frequently asked:

1. `awk '{print $NF}'`
2. `awk '!seen[$0]++'`
3. `sort | uniq`
4. `grep -i`
5. `wc -l`

---

# Pattern Understanding (Very Important)

Interview questions mostly test:

* Filtering → `grep`
* Processing → `awk`
* Editing → `sed`
* Counting → `wc`
* Sorting → `sort + uniq`

---

# 🧠 Pro Tip

If you don’t know solution:

👉 Think:

* **Search? → grep**
* **Columns? → awk**
* **Replace? → sed**
* **Duplicates? → sort + uniq / awk**

---

# Integrated Challenges

## Challenge 1: Build a Complete School Management System

### Phase 1: Design (SQL)
- Create database schema for students, teachers, classes, subjects, grades
- Define relationships between entities

### Phase 2: Backend (Python + SQL)
- Create Python classes to manage database operations
- Implement CRUD operations
- Calculate GPA, class rankings

### Phase 3: Shell Script (Bash)
- Create backup script for database
- Monitor database performance
- Generate reports

---

## Challenge 2: Log Analysis System

### Phase 1: Generate Log Files (Bash)
```bash
#!/bin/bash
# Generate sample logs
for i in {1..100}; do
    echo "$(date '+%Y-%m-%d %H:%M:%S') ERROR: Process failed" >> system.log
done
```

### Phase 2: Parse and Analyze (Python)
```python
import re
from collections import Counter

with open('system.log', 'r') as f:
    errors = [line for line in f if 'ERROR' in line]
    print(f"Total errors: {len(errors)}")
```

### Phase 3: Store in Database (SQL)
```sql
CREATE TABLE logs (
    log_id INT PRIMARY KEY AUTO_INCREMENT,
    timestamp DATETIME,
    level VARCHAR(20),
    message TEXT
);
```

---

## Challenge 3: File Processing Pipeline

### Scenario:
1. **UNIX:** Gather all CSV files from a directory
2. **Python:** Parse and clean data
3. **SQL:** Load into database and generate reports

### UNIX commands:
```bash
find . -name "*.csv" -type f
```

### Python script:
```python
import csv
import mysql.connector

for file in ['file1.csv', 'file2.csv']:
    with open(file, 'r') as f:
        reader = csv.DictReader(f)
        for row in reader:
            # Insert into database
            pass
```

---

**Created:** May 3, 2026
**Subject Matter:** UNIX, Python, and SQL
**Purpose:** Comprehensive learning and interview preparation

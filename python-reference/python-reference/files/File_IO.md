---
title: 📁 File I/O
parent: File Operations
nav_order: 1
---

# 📁 File I/O

Reading and writing files in Python.

---

## 📖 Reading Files

```python
# Read entire file as string
with open("/etc/hostname", "r") as f:
    content = f.read()

# Read all lines as list
with open("/etc/hosts", "r") as f:
    lines = f.readlines()

# Read line by line (memory-efficient for large files)
with open("/var/log/syslog", "r") as f:
    for line in f:
        print(line.strip())

# Read with encoding
with open("file.txt", "r", encoding="utf-8") as f:
    content = f.read()
```

---

## ✏️ Writing Files

```python
# Write (overwrites existing)
with open("output.txt", "w") as f:
    f.write("Hello, World!\n")

# Append
with open("logfile.txt", "a") as f:
    f.write("New log entry\n")

# Write multiple lines
lines = ["line one\n", "line two\n", "line three\n"]
with open("output.txt", "w") as f:
    f.writelines(lines)
```

---

## 📂 File Modes

| Mode  | Meaning                          |
|-------|----------------------------------|
| `r`   | Read (default)                   |
| `w`   | Write (create or overwrite)      |
| `a`   | Append                           |
| `x`   | Create (fails if exists)         |
| `rb`  | Read binary                      |
| `wb`  | Write binary                     |
| `r+`  | Read and write                   |

---

## 🔒 The `with` Statement

Always use `with open(...)` — it closes the file automatically, even if an error occurs:

```python
# Good — file always closed
with open("file.txt") as f:
    data = f.read()

# Bad — file may stay open on error
f = open("file.txt")
data = f.read()
f.close()
```

---

## 🔍 Checking Files

```python
import os

os.path.exists("/etc/passwd")      # True
os.path.isfile("/etc/passwd")      # True
os.path.isdir("/etc")              # True
os.path.getsize("/etc/passwd")     # Size in bytes
os.path.getmtime("/etc/passwd")    # Modified timestamp (float)

# Better: use pathlib (Python 3.4+)
from pathlib import Path

p = Path("/etc/passwd")
p.exists()         # True
p.is_file()        # True
p.stat().st_size   # Size in bytes
```

---

## 🔁 Working with Lines

```python
# Read, process, write
with open("input.txt") as fin, open("output.txt", "w") as fout:
    for line in fin:
        processed = line.strip().upper()
        fout.write(processed + "\n")

# Filter lines
with open("/var/log/syslog") as f:
    errors = [line for line in f if "error" in line.lower()]

# Search for pattern
import re
pattern = re.compile(r"Failed password for (\w+)")
with open("/var/log/auth.log") as f:
    for line in f:
        m = pattern.search(line)
        if m:
            print(f"Failed login: {m.group(1)}")
```

---

## 📌 Summary

| Task                     | Syntax                              |
|--------------------------|-------------------------------------|
| Read entire file         | `f.read()`                          |
| Read all lines           | `f.readlines()`                     |
| Iterate lines            | `for line in f:`                    |
| Write to file            | `f.write("text\n")`                 |
| Append to file           | `open("f", "a")`                    |
| Check file exists        | `Path("f").exists()`                |
| Always use               | `with open("file") as f:`           |

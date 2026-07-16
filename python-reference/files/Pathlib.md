---
title: 📂 Working with Paths (pathlib)
parent: File Operations
nav_order: 2
---

# 📂 Working with Paths (pathlib)

The modern way to work with filesystem paths in Python 3.

---

## 📦 Import

```python
from pathlib import Path
```

---

## 🗺️ Creating Paths

```python
# Create Path objects
p = Path("/etc/nginx/nginx.conf")
home = Path.home()                  # /home/username
cwd = Path.cwd()                    # Current working directory

# Build paths with /
config_dir = Path("/etc") / "nginx"
config_file = config_dir / "nginx.conf"
```

---

## 🔍 Inspecting Paths

```python
p = Path("/etc/nginx/nginx.conf")

p.name          # 'nginx.conf'
p.stem          # 'nginx'  (name without suffix)
p.suffix        # '.conf'
p.parent        # Path('/etc/nginx')
p.parents[0]    # Path('/etc/nginx')
p.parents[1]    # Path('/etc')
p.parts         # ('/', 'etc', 'nginx', 'nginx.conf')
str(p)          # '/etc/nginx/nginx.conf'
```

---

## ✅ Checking Paths

```python
p.exists()         # True if path exists
p.is_file()        # True if it's a file
p.is_dir()         # True if it's a directory
p.is_symlink()     # True if it's a symlink

stat = p.stat()
stat.st_size       # Size in bytes
stat.st_mtime      # Last modified (Unix timestamp)
```

---

## 📁 Directory Operations

```python
d = Path("/tmp/mydir")

# Create directory
d.mkdir()                           # Create directory
d.mkdir(parents=True)               # Create parent dirs too
d.mkdir(parents=True, exist_ok=True) # Don't error if exists

# List contents
for item in d.iterdir():
    print(item)

# Glob (find files by pattern)
for conf in Path("/etc").glob("*.conf"):
    print(conf)

# Recursive glob
for py in Path("/opt/myapp").rglob("*.py"):
    print(py)

# Remove directory (must be empty)
d.rmdir()
```

---

## 📄 File Operations

```python
p = Path("/tmp/test.txt")

# Read
content = p.read_text()
data = p.read_bytes()         # Binary

# Write (overwrites)
p.write_text("Hello, World!\n")
p.write_bytes(b"binary data")

# Delete
p.unlink()                    # Delete file
p.unlink(missing_ok=True)     # Don't error if missing

# Rename / move
p.rename(Path("/tmp/newname.txt"))
p.replace(Path("/tmp/newname.txt"))   # Overwrites target

# Copy (no built-in — use shutil)
import shutil
shutil.copy2(p, Path("/backup/test.txt"))
shutil.copytree(src_dir, dst_dir)
```

---

## 🔄 Common Patterns

```python
# Find all log files older than 7 days
import time
cutoff = time.time() - (7 * 86400)
old_logs = [
    f for f in Path("/var/log").rglob("*.log")
    if f.stat().st_mtime < cutoff
]

# Create a dated output file
from datetime import date
outfile = Path("/tmp") / f"report_{date.today()}.txt"
outfile.write_text("Report content here")

# Ensure output directory exists
output_dir = Path("/opt/myapp/output")
output_dir.mkdir(parents=True, exist_ok=True)
```

---

## 📌 Summary

| Task                     | Syntax                              |
|--------------------------|-------------------------------------|
| Create path              | `p = Path("/some/path")`            |
| Join paths               | `p / "subdir" / "file.txt"`         |
| File name                | `p.name`                            |
| Parent directory         | `p.parent`                          |
| Extension                | `p.suffix`                          |
| Check exists             | `p.exists()`                        |
| List directory           | `p.iterdir()`                       |
| Find by pattern          | `p.glob("*.conf")`                  |
| Recursive find           | `p.rglob("*.py")`                   |
| Read text                | `p.read_text()`                     |
| Write text               | `p.write_text("content")`           |
| Delete file              | `p.unlink()`                        |
| Create dir (safe)        | `p.mkdir(parents=True, exist_ok=True)` |

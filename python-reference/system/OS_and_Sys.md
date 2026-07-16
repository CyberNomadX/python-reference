---
title: 🖥️ os and sys Modules
parent: System Tools
nav_order: 1
---

# 🖥️ os and sys Modules

Interacting with the operating system and Python runtime.

---

## 📦 Import

```python
import os
import sys
```

---

## 🗂️ os Module — Filesystem

```python
# Current directory
os.getcwd()                        # Get current working directory
os.chdir("/tmp")                   # Change directory

# Directory operations
os.listdir("/etc")                 # List directory contents
os.makedirs("/tmp/a/b/c", exist_ok=True)  # Create nested dirs
os.remove("file.txt")              # Delete file
os.rmdir("emptydir")               # Delete empty directory

import shutil
shutil.rmtree("/tmp/mydir")        # Delete directory tree
shutil.copy2("src.txt", "dst.txt") # Copy file
shutil.move("src", "dst")          # Move file or directory

# File info
os.path.exists("/etc/passwd")      # True/False
os.path.isfile("/etc/passwd")
os.path.isdir("/etc")
os.path.getsize("/etc/passwd")
os.stat("/etc/passwd")             # Full stat info

# Path manipulation
os.path.join("/etc", "nginx", "nginx.conf")  # Build path
os.path.basename("/etc/nginx/nginx.conf")    # 'nginx.conf'
os.path.dirname("/etc/nginx/nginx.conf")     # '/etc/nginx'
os.path.splitext("file.tar.gz")             # ('file.tar', '.gz')
os.path.abspath("relative/path")            # Absolute path
```

---

## 🌍 os Module — Process and Environment

```python
# Process info
os.getpid()         # Current PID
os.getppid()        # Parent PID
os.getuid()         # User ID (Unix)
os.getgid()         # Group ID (Unix)

# Run command (simple, use subprocess for capture)
os.system("ls -la")

# Walk directory tree
for dirpath, dirnames, filenames in os.walk("/var/log"):
    for filename in filenames:
        full_path = os.path.join(dirpath, filename)
        print(full_path)
```

---

## ⚙️ sys Module — Python Runtime

```python
sys.argv           # Command-line arguments: ['script.py', 'arg1', 'arg2']
sys.argv[0]        # Script name
sys.argv[1:]       # All arguments after script name

sys.exit(0)        # Exit with code 0 (success)
sys.exit(1)        # Exit with error code

sys.version        # Python version string
sys.platform       # 'linux', 'darwin', 'win32'

sys.path           # List of module search paths
sys.path.insert(0, "/my/module/dir")  # Add to path

sys.stdin          # Standard input stream
sys.stdout         # Standard output stream
sys.stderr         # Standard error stream

# Write to stderr
print("Error: something went wrong", file=sys.stderr)
```

---

## 🖥️ Platform Detection

```python
import sys
import platform

# Quick check
if sys.platform == "linux":
    pass
elif sys.platform == "darwin":
    pass
elif sys.platform == "win32":
    pass

# Detailed info
platform.system()       # 'Linux', 'Darwin', 'Windows'
platform.release()      # Kernel/OS version
platform.machine()      # 'x86_64', 'arm64'
platform.node()         # Hostname
```

---

## 📌 Summary

| Task                     | Syntax                              |
|--------------------------|-------------------------------------|
| Current directory        | `os.getcwd()`                       |
| Change directory         | `os.chdir("/path")`                 |
| List directory           | `os.listdir("/path")`               |
| Create nested dirs       | `os.makedirs("/a/b", exist_ok=True)`|
| Delete file              | `os.remove("file")`                 |
| Walk directory tree      | `os.walk("/path")`                  |
| File exists              | `os.path.exists("/path")`           |
| Join paths               | `os.path.join("/etc", "file")`      |
| Script arguments         | `sys.argv`                          |
| Exit with code           | `sys.exit(0)`                       |
| Detect OS                | `sys.platform`                      |

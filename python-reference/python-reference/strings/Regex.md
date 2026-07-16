---
title: 🔍 Regular Expressions
parent: Strings
nav_order: 2
---

# 🔍 Regular Expressions

Pattern matching with Python's `re` module.

---

## 📦 Import

```python
import re
```

---

## 🎯 Core Functions

```python
text = "Server IP: 192.168.1.100 connected at 14:32:01"

# Search — find first match anywhere in string
match = re.search(r"\d+\.\d+\.\d+\.\d+", text)
if match:
    print(match.group())    # 192.168.1.100

# Match — only matches at start of string
m = re.match(r"Server", text)   # Match object or None

# Findall — return list of all matches
ips = re.findall(r"\d+\.\d+\.\d+\.\d+", text)
# ['192.168.1.100']

# Sub — replace matches
result = re.sub(r"\d+\.\d+\.\d+\.\d+", "[REDACTED]", text)
# 'Server IP: [REDACTED] connected at 14:32:01'

# Split on pattern
parts = re.split(r"\s+", "one  two   three")
# ['one', 'two', 'three']
```

---

## 🔣 Common Patterns

```python
# IP address (simple)
r"\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}"

# Email address
r"[\w.+-]+@[\w-]+\.[a-zA-Z]{2,}"

# URL
r"https?://[^\s]+"

# Date (YYYY-MM-DD)
r"\d{4}-\d{2}-\d{2}"

# Time (HH:MM:SS)
r"\d{2}:\d{2}:\d{2}"

# Windows path
r"[A-Za-z]:\\(?:[^\\/:*?\"<>|\r\n]+\\)*[^\\/:*?\"<>|\r\n]*"

# Word boundary
r"\bword\b"     # matches 'word' but not 'wording'
```

---

## 📋 Regex Syntax Reference

| Pattern   | Meaning                          |
|-----------|----------------------------------|
| `.`       | Any character except newline     |
| `\d`      | Digit [0-9]                      |
| `\D`      | Non-digit                        |
| `\w`      | Word char [a-zA-Z0-9_]           |
| `\W`      | Non-word char                    |
| `\s`      | Whitespace (space, tab, newline) |
| `\S`      | Non-whitespace                   |
| `^`       | Start of string                  |
| `$`       | End of string                    |
| `*`       | 0 or more                        |
| `+`       | 1 or more                        |
| `?`       | 0 or 1 (optional)                |
| `{n}`     | Exactly n times                  |
| `{n,m}`   | Between n and m times            |
| `[abc]`   | Character class (a, b, or c)     |
| `[^abc]`  | Not a, b, or c                   |
| `(group)` | Capture group                    |
| `a\|b`    | a or b                           |

---

## 🎯 Groups and Captures

```python
log = "2024-01-15 08:32:01 ERROR nginx: connection timeout"

pattern = r"(\d{4}-\d{2}-\d{2}) (\d{2}:\d{2}:\d{2}) (\w+)"
m = re.search(pattern, log)

if m:
    print(m.group(0))   # entire match
    print(m.group(1))   # 2024-01-15
    print(m.group(2))   # 08:32:01
    print(m.group(3))   # ERROR

# Named groups
pattern = r"(?P<date>\d{4}-\d{2}-\d{2}) (?P<level>\w+)"
m = re.search(pattern, log)
print(m.group("date"))    # 2024-01-15
print(m.group("level"))   # ERROR
```

---

## ⚙️ Flags

```python
# Case-insensitive
re.search(r"error", text, re.IGNORECASE)

# Multiline (^ and $ match each line)
re.findall(r"^\d+", text, re.MULTILINE)

# Dot matches newline too
re.search(r"start.*end", text, re.DOTALL)

# Compile for reuse (faster in loops)
ip_pattern = re.compile(r"\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}")
matches = ip_pattern.findall(log_file_content)
```

---

## 📌 Summary

| Task                    | Function                                |
|-------------------------|-----------------------------------------|
| Find first match        | `re.search(pattern, text)`              |
| Match at start          | `re.match(pattern, text)`               |
| All matches             | `re.findall(pattern, text)`             |
| Replace matches         | `re.sub(pattern, replacement, text)`    |
| Split on pattern        | `re.split(pattern, text)`               |
| Case-insensitive        | `re.search(p, t, re.IGNORECASE)`        |
| Compile for reuse       | `p = re.compile(pattern)`               |

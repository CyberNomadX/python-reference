---
title: 🔤 String Operations
parent: Strings
nav_order: 1
---

# 🔤 String Operations

Working with strings — the most common data type in sysadmin scripts.

---

## 📝 Creating Strings

```python
single = 'hello'
double = "world"
multi  = """
This spans
multiple lines
"""

# Raw string (backslashes are literal — useful for paths/regex)
path = r"C:\Users\Alice\Documents"
pattern = r"\d+\.\d+"
```

---

## 🔍 Accessing and Slicing

```python
s = "Hello, World!"

s[0]       # 'H'  (first char)
s[-1]      # '!'  (last char)
s[7:12]    # 'World'
s[:5]      # 'Hello'
s[::2]     # 'Hlo ol!'  (every other char)
s[::-1]    # '!dlroW ,olleH'  (reversed)
len(s)     # 13
```

---

## 🔧 Common String Methods

```python
s = "  Hello, World!  "

s.strip()           # 'Hello, World!'  (remove whitespace)
s.lstrip()          # 'Hello, World!  '
s.rstrip()          # '  Hello, World!'
s.lower()           # '  hello, world!  '
s.upper()           # '  HELLO, WORLD!  '
s.title()           # '  Hello, World!  '

s.replace("World", "Python")   # '  Hello, Python!  '
s.count("l")        # 3
s.startswith("  H") # True
s.endswith("!  ")   # True

# Split and join
words = "one two three".split()       # ['one', 'two', 'three']
csv = "a,b,c".split(",")             # ['a', 'b', 'c']
joined = " ".join(["one", "two"])    # 'one two'
path = "/".join(["etc", "nginx", "conf"])  # 'etc/nginx/conf'

# Find and check
"world" in "hello world"    # True
"hello world".find("world") # 6  (index)
"hello world".index("world")# 6  (raises ValueError if not found)
```

---

## 🎨 String Formatting

```python
name = "Alice"
count = 42

# f-strings (Python 3.6+ — preferred)
print(f"Hello, {name}! Count: {count}")
print(f"Pi is approximately {3.14159:.2f}")   # 2 decimal places
print(f"{'left':<10}")     # left-aligned, 10 wide
print(f"{'right':>10}")    # right-aligned
print(f"{count:05d}")      # zero-padded: 00042

# .format()
print("Hello, {}!".format(name))
print("Hello, {name}!".format(name=name))

# % formatting (old style — still seen in logs/C code)
print("Hello, %s! Count: %d" % (name, count))
```

---

## 🔍 Useful Checks

```python
"123".isdigit()          # True
"abc".isalpha()          # True
"abc123".isalnum()       # True
"   ".isspace()          # True
"Hello".istitle()        # True
```

---

## 📌 Summary

| Task                  | Syntax                                |
|-----------------------|---------------------------------------|
| Strip whitespace      | `s.strip()`                           |
| Lower / upper         | `s.lower()` / `s.upper()`             |
| Replace               | `s.replace("old", "new")`             |
| Split on delimiter    | `s.split(",")`                        |
| Join list to string   | `",".join(lst)`                       |
| Check contains        | `"sub" in s`                          |
| Find index            | `s.find("sub")` (returns -1 if miss)  |
| f-string              | `f"Hello {name}"`                     |
| Format float          | `f"{val:.2f}"`                        |
| Zero pad              | `f"{n:05d}"`                          |

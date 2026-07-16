---
title: 🎨 String Formatting
parent: Strings
nav_order: 3
---

# 🎨 String Formatting

f-strings, format(), template strings, and format specifiers.

---

## ⭐ f-strings (Python 3.6+ — Use These)

```python
name = "Alice"
count = 42
pi = 3.14159

# Basic
print(f"Hello, {name}!")

# Expression inside
print(f"Count doubled: {count * 2}")
print(f"Type: {type(name).__name__}")

# Method calls
print(f"Upper: {name.upper()}")

# Conditional
status = "active" if count > 0 else "inactive"
print(f"Status: {'active' if count > 0 else 'inactive'}")

# Multi-line
msg = (
    f"Name: {name}\n"
    f"Count: {count}\n"
    f"Pi: {pi:.2f}"
)
```

---

## 🔢 Format Specifiers

```python
n = 1234567.891

# Numbers
f"{n:.2f}"          # '1234567.89'  — 2 decimal places
f"{n:,.2f}"         # '1,234,567.89' — thousands separator
f"{n:e}"            # '1.234568e+06' — scientific notation
f"{42:05d}"         # '00042'  — zero-padded integer
f"{42:+d}"          # '+42'    — always show sign
f"{255:x}"          # 'ff'     — hex (lowercase)
f"{255:X}"          # 'FF'     — hex (uppercase)
f"{255:08b}"        # '11111111' — binary, 8 wide
f"{0.756:.1%}"      # '75.6%'  — percentage

# Alignment
f"{'left':<10}"     # 'left      '  — left-align in 10 chars
f"{'right':>10}"    # '     right'  — right-align
f"{'center':^10}"   # '  center  '  — center
f"{'fill':*^10}"    # '**fill****'  — center with fill char

# Width from variable
width = 10
f"{'text':{width}}"
```

---

## 🔧 str.format()

```python
# Positional
"{} {}".format("hello", "world")         # 'hello world'
"{0} {1} {0}".format("hello", "world")   # 'hello world hello'

# Keyword
"{name} is {age}".format(name="Alice", age=30)

# Dict unpacking
data = {"name": "Alice", "role": "admin"}
"{name} — {role}".format(**data)

# Format specs work the same
"{:.2f}".format(3.14159)    # '3.14'
```

---

## 📋 Template Strings (Safe for User Input)

```python
from string import Template

t = Template("Hello, $name! You have $count messages.")
result = t.substitute(name="Alice", count=5)
# 'Hello, Alice! You have 5 messages.'

# safe_substitute — doesn't error on missing vars
result = t.safe_substitute(name="Alice")
# 'Hello, Alice! You have $count messages.'
```

Good for user-provided templates where you don't want arbitrary expression evaluation.

---

## 📌 Format Specifier Cheat Sheet

| Specifier  | Example          | Result           |
|------------|------------------|------------------|
| `:.2f`     | `f"{3.14159:.2f}"` | `3.14`         |
| `:,.0f`    | `f"{1234567:,.0f}"` | `1,234,567`   |
| `:05d`     | `f"{42:05d}"`    | `00042`          |
| `:x`       | `f"{255:x}"`     | `ff`             |
| `:b`       | `f"{10:b}"`      | `1010`           |
| `:.1%`     | `f"{0.756:.1%}"` | `75.6%`          |
| `:<10`     | `f"{'a':<10}"`   | `a         `     |
| `:>10`     | `f"{'a':>10}"`   | `         a`     |
| `:^10`     | `f"{'a':^10}"`   | `    a     `     |

---
title: 📋 Lists and Tuples
parent: Data Structures
nav_order: 1
---

# 📋 Lists and Tuples

Python's ordered sequence types.

---

## 📋 Lists

Lists are ordered, mutable (changeable) collections.

```python
# Create
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", True, None]
empty = []

# Access
print(fruits[0])     # apple (first)
print(fruits[-1])    # cherry (last)

# Slicing
print(fruits[1:3])   # ['banana', 'cherry']
print(fruits[:2])    # ['apple', 'banana']
print(fruits[::2])   # every other: ['apple', 'cherry']
```

---

## ✏️ Modifying Lists

```python
fruits.append("date")            # Add to end
fruits.insert(1, "avocado")      # Insert at index
fruits.extend(["mango", "kiwi"]) # Add multiple

fruits.remove("banana")          # Remove by value
popped = fruits.pop()            # Remove and return last
popped = fruits.pop(0)           # Remove and return by index

fruits.sort()                    # Sort in place
fruits.sort(reverse=True)        # Sort descending
sorted_copy = sorted(fruits)     # Return sorted copy

fruits.reverse()                 # Reverse in place
fruits.clear()                   # Remove all items
```

---

## 🔍 List Operations

```python
# Length
len(fruits)

# Check membership
"apple" in fruits      # True or False

# Count occurrences
fruits.count("apple")

# Find index
fruits.index("banana")

# Copy
copy = fruits.copy()
copy = fruits[:]       # Same thing

# Concatenate
combined = fruits + ["mango", "kiwi"]
```

---

## 🔄 Iterating

```python
for fruit in fruits:
    print(fruit)

# With index
for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")

# Multiple lists together
for name, score in zip(names, scores):
    print(f"{name}: {score}")
```

---

## 📌 Tuples

Tuples are ordered and **immutable** (can't be changed after creation).

```python
# Create
coords = (10, 20)
rgb = (255, 128, 0)
single = (42,)          # Note: trailing comma for single-item tuple

# Access (same as list)
print(coords[0])        # 10

# Unpack
x, y = coords
r, g, b = rgb

# Swap values
a, b = b, a

# Named tuple
from collections import namedtuple
Point = namedtuple("Point", ["x", "y"])
p = Point(3, 4)
print(p.x, p.y)         # 3 4
```

---

## 📌 Summary

| Task                  | Syntax                            |
|-----------------------|-----------------------------------|
| Create list           | `lst = [1, 2, 3]`                 |
| Append                | `lst.append(val)`                 |
| Insert at index       | `lst.insert(i, val)`              |
| Remove by value       | `lst.remove(val)`                 |
| Pop last              | `lst.pop()`                       |
| Sort in place         | `lst.sort()`                      |
| Length                | `len(lst)`                        |
| Check membership      | `val in lst`                      |
| Enumerate             | `for i, v in enumerate(lst):`     |
| Zip two lists         | `for a, b in zip(lst1, lst2):`    |
| Create tuple          | `t = (1, 2, 3)`                   |
| Unpack tuple          | `x, y, z = t`                     |

---
title: 🗂️ Dictionaries and Sets
parent: Data Structures
nav_order: 2
---

# 🗂️ Dictionaries and Sets

Key-value stores and unique-value collections.

---

## 📖 Dictionaries

Dictionaries store key-value pairs. Keys must be unique and immutable.

```python
# Create
user = {
    "name": "Alice",
    "role": "admin",
    "age": 30
}
empty = {}

# Access
print(user["name"])           # Alice
print(user.get("email"))      # None (no KeyError)
print(user.get("email", "N/A"))  # N/A (default value)
```

---

## ✏️ Modifying Dicts

```python
user["email"] = "alice@example.com"    # Add or update
user.update({"age": 31, "city": "Springfield"})  # Update multiple

del user["age"]                        # Delete key
removed = user.pop("city")             # Remove and return
user.pop("missing", None)              # Safe pop with default
user.clear()                           # Remove all
```

---

## 🔍 Iterating

```python
# Keys (default)
for key in user:
    print(key)

# Values
for value in user.values():
    print(value)

# Both
for key, value in user.items():
    print(f"{key}: {value}")

# Check if key exists
if "name" in user:
    print(user["name"])
```

---

## 🛠️ Dict Patterns

```python
# Dict comprehension
squares = {x: x**2 for x in range(6)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Merge dicts (Python 3.9+)
merged = dict1 | dict2
dict1 |= dict2    # Update in place

# defaultdict — auto-creates missing keys
from collections import defaultdict
counts = defaultdict(int)
for word in words:
    counts[word] += 1

# Counter — count occurrences
from collections import Counter
word_counts = Counter(words)
top_5 = word_counts.most_common(5)

# Nested dict
config = {
    "database": {"host": "localhost", "port": 5432},
    "cache": {"host": "redis", "port": 6379}
}
print(config["database"]["host"])    # localhost
```

---

## 🔵 Sets

Sets store unique values with no guaranteed order.

```python
# Create
colors = {"red", "green", "blue"}
unique_ips = set()
from_list = set([1, 2, 2, 3, 3, 3])   # {1, 2, 3}

# Add / remove
colors.add("yellow")
colors.discard("red")     # Safe remove (no error if missing)
colors.remove("green")    # Raises KeyError if missing

# Check membership
"blue" in colors    # True (fast O(1) lookup)

# Set operations
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

a | b    # Union: {1, 2, 3, 4, 5, 6}
a & b    # Intersection: {3, 4}
a - b    # Difference: {1, 2}
a ^ b    # Symmetric difference: {1, 2, 5, 6}
```

---

## 📌 Summary

| Task                     | Syntax                              |
|--------------------------|-------------------------------------|
| Create dict              | `d = {"key": "value"}`              |
| Safe get                 | `d.get("key", default)`             |
| Add/update               | `d["key"] = value`                  |
| Delete key               | `del d["key"]`                      |
| Iterate key/value        | `for k, v in d.items():`            |
| Count occurrences        | `Counter(iterable)`                 |
| Create set               | `s = {1, 2, 3}` or `set()`         |
| Union                    | `a \| b`                            |
| Intersection             | `a & b`                             |
| Difference               | `a - b`                             |
| Unique values from list  | `set(my_list)`                      |

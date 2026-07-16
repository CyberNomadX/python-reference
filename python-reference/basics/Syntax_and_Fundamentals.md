---
title: ⚙️ Syntax and Fundamentals
parent: Basics
nav_order: 2
---

# ⚙️ Syntax and Fundamentals

Python control flow, functions, error handling, and key syntax patterns.

---

## 🔀 if / elif / else

```python
score = 85

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("Below C")
```

Comparison operators: `==`, `!=`, `<`, `>`, `<=`, `>=`

Logical operators: `and`, `or`, `not`

```python
if age >= 18 and has_id:
    print("Access granted")

if not active:
    print("Account disabled")
```

---

## 🔁 Loops

```python
# for loop — iterate over sequence
for i in range(5):          # 0, 1, 2, 3, 4
    print(i)

for name in ["Alice", "Bob", "Charlie"]:
    print(f"Hello, {name}")

# while loop
count = 0
while count < 5:
    print(count)
    count += 1

# break and continue
for i in range(10):
    if i == 3:
        continue    # skip 3
    if i == 7:
        break       # stop at 7
    print(i)
```

---

## 🧩 Functions

```python
# Define
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

# Call
print(greet("Alice"))               # Hello, Alice!
print(greet("Alice", "Hey"))        # Hey, Alice!

# *args (variable positional args)
def add(*numbers):
    return sum(numbers)

print(add(1, 2, 3, 4))    # 10

# **kwargs (variable keyword args)
def profile(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

profile(name="Alice", role="admin")
```

---

## 🛡️ Error Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Can't divide by zero")

try:
    value = int("abc")
except ValueError as e:
    print(f"Error: {e}")
finally:
    print("This always runs")

# Catch multiple exceptions
try:
    x = some_function()
except (TypeError, ValueError) as e:
    print(f"Bad input: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
    raise   # re-raise
```

---

## 🎯 Comprehensions

```python
# List comprehension
squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# With filter
evens = [x for x in range(20) if x % 2 == 0]

# Dict comprehension
lengths = {word: len(word) for word in ["hello", "world"]}
# {'hello': 5, 'world': 5}
```

---

## 📌 Summary

| Concept           | Syntax                             |
|-------------------|------------------------------------|
| if/elif/else      | `if cond:` / `elif cond:` / `else:`|
| for loop          | `for x in iterable:`               |
| while loop        | `while condition:`                 |
| break / continue  | `break` / `continue`               |
| Function          | `def name(args): return val`       |
| Default arg       | `def f(x, y=10):`                  |
| try/except        | `try:` / `except ExcType as e:`    |
| List comprehension| `[expr for x in seq if cond]`      |

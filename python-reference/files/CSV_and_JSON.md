---
title: 📊 CSV and JSON
parent: File Operations
nav_order: 3
---

# 📊 CSV and JSON

Two of the most common data formats in sysadmin and API work.

---

## 📄 CSV

### Reading

```python
import csv

# Read as rows (list of lists)
with open("users.csv") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# Skip header
with open("users.csv") as f:
    reader = csv.reader(f)
    header = next(reader)
    for row in reader:
        print(row)

# Read as dicts (column names from header)
with open("users.csv") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["username"], row["email"])
```

### Writing

```python
# Write rows
with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["name", "age", "city"])      # Header
    writer.writerow(["Alice", 30, "Springfield"])
    writer.writerows([["Alice", 25, "Madison"], ["Bob", 35, "Milwaukee"]])

# Write dicts
fields = ["name", "age", "city"]
rows = [{"name": "Alice", "age": 30, "city": "Springfield"}]

with open("output.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=fields)
    writer.writeheader()
    writer.writerows(rows)
```

---

## 🔧 JSON

### Reading

```python
import json

# From file
with open("config.json") as f:
    data = json.load(f)

# From string
json_string = '{"host": "localhost", "port": 5432}'
data = json.loads(json_string)
print(data["host"])    # localhost
```

### Writing

```python
config = {
    "host": "localhost",
    "port": 5432,
    "debug": False,
    "tags": ["production", "primary"]
}

# To file
with open("config.json", "w") as f:
    json.dump(config, f, indent=2)

# To string
json_string = json.dumps(config, indent=2)
print(json_string)
```

### Working with JSON

```python
# Pretty print
print(json.dumps(data, indent=2))

# Handle dates (not JSON-serializable by default)
from datetime import datetime
import json

class DateEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, datetime):
            return obj.isoformat()
        return super().default(obj)

json.dumps({"ts": datetime.now()}, cls=DateEncoder)

# Safer: convert to string first
data["timestamp"] = datetime.now().isoformat()
```

---

## 📌 Summary

| Task                     | Syntax                                    |
|--------------------------|-------------------------------------------|
| Read CSV (dicts)         | `csv.DictReader(f)`                       |
| Write CSV (dicts)        | `csv.DictWriter(f, fieldnames=[...])`     |
| Read JSON file           | `json.load(f)`                            |
| Read JSON string         | `json.loads(string)`                      |
| Write JSON file          | `json.dump(data, f, indent=2)`            |
| JSON to string           | `json.dumps(data, indent=2)`              |
| Always open CSV with     | `open("f", newline="")`                   |

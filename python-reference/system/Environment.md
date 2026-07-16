---
title: 🌍 Environment Variables
parent: System Tools
nav_order: 2
---

# 🌍 Environment Variables

Reading and using environment variables in Python — essential for config and secrets.

---

## 📖 Reading Env Vars

```python
import os

# Get value (returns None if not set)
home = os.environ.get("HOME")
api_key = os.environ.get("API_KEY")

# Get with default
debug = os.environ.get("DEBUG", "false")
port = int(os.environ.get("PORT", "8080"))

# Raise error if required var is missing
db_url = os.environ["DATABASE_URL"]   # KeyError if not set

# View all
for key, value in os.environ.items():
    print(f"{key}={value}")
```

---

## ✏️ Setting Env Vars (in Process)

```python
# Set for current process (affects subprocess too)
os.environ["MY_VAR"] = "value"

# Unset
del os.environ["MY_VAR"]
os.environ.pop("MY_VAR", None)    # Safe pop
```

---

## 🔒 .env Files with python-dotenv

The `python-dotenv` library loads variables from a `.env` file:

```bash
pip install python-dotenv
```

`.env` file:
```
DATABASE_URL=postgresql://localhost/mydb
API_KEY=secret123
DEBUG=true
PORT=8080
```

```python
from dotenv import load_dotenv
import os

load_dotenv()   # Loads from .env in current directory

db_url = os.environ.get("DATABASE_URL")
api_key = os.environ.get("API_KEY")
```

> ⚠️ Never commit `.env` files to version control. Add `.env` to `.gitignore`.

---

## 🏗️ Config Pattern for Scripts

```python
import os
from dataclasses import dataclass


@dataclass
class Config:
    api_url: str
    api_key: str
    timeout: int
    debug: bool

    @classmethod
    def from_env(cls):
        api_url = os.environ.get("API_URL", "https://api.example.com")
        api_key = os.environ.get("API_KEY")
        if not api_key:
            raise ValueError("API_KEY environment variable is required")
        timeout = int(os.environ.get("TIMEOUT", "30"))
        debug = os.environ.get("DEBUG", "").lower() in ("1", "true", "yes")
        return cls(api_url=api_url, api_key=api_key, timeout=timeout, debug=debug)


config = Config.from_env()
```

---

## 📌 Summary

| Task                     | Syntax                                    |
|--------------------------|-------------------------------------------|
| Get var (safe)           | `os.environ.get("VAR")`                   |
| Get with default         | `os.environ.get("VAR", "default")`        |
| Get (raise if missing)   | `os.environ["VAR"]`                       |
| Set var                  | `os.environ["VAR"] = "value"`             |
| Unset var (safe)         | `os.environ.pop("VAR", None)`             |
| Load .env file           | `from dotenv import load_dotenv; load_dotenv()` |

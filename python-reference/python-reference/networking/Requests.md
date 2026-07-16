---
title: 🌐 requests Library
parent: Networking
nav_order: 1
---

# 🌐 requests Library

Making HTTP requests in Python — the standard for API work.

---

## 📦 Install

```bash
pip install requests
```

```python
import requests
```

---

## 🔵 GET Requests

```python
# Basic GET
r = requests.get("https://api.example.com/users")

# Check status
print(r.status_code)    # 200
r.raise_for_status()    # Raises exception on 4xx/5xx

# Response body
print(r.text)           # As string
data = r.json()         # Parse JSON automatically
print(r.content)        # As bytes

# Query parameters
r = requests.get(
    "https://api.example.com/users",
    params={"status": "active", "limit": 50}
)
# → GET /users?status=active&limit=50
```

---

## 🟢 POST / PUT / DELETE

```python
# POST with JSON body
r = requests.post(
    "https://api.example.com/users",
    json={"name": "Alice", "role": "admin"}
)
print(r.status_code)    # 201

# POST form data
r = requests.post(
    "https://api.example.com/login",
    data={"username": "alice", "password": "secret"}
)

# PUT (update)
r = requests.put(
    "https://api.example.com/users/42",
    json={"role": "superadmin"}
)

# DELETE
r = requests.delete("https://api.example.com/users/42")
```

---

## 🔑 Auth and Headers

```python
# Bearer token
headers = {"Authorization": "Bearer mytoken123"}
r = requests.get("https://api.example.com/data", headers=headers)

# Basic auth
r = requests.get(
    "https://api.example.com/secure",
    auth=("username", "password")
)

# API key as header
r = requests.get(
    "https://api.example.com/data",
    headers={"X-API-Key": "abc123"}
)
```

---

## ⏱️ Timeouts and Retries

```python
# Always set a timeout
r = requests.get("https://api.example.com", timeout=10)
r = requests.get("https://api.example.com", timeout=(3.05, 27))
# (connect timeout, read timeout)

# Session for connection reuse + shared headers
session = requests.Session()
session.headers.update({"Authorization": "Bearer mytoken"})

r1 = session.get("https://api.example.com/users")
r2 = session.get("https://api.example.com/groups")
```

---

## 🛡️ Error Handling

```python
try:
    r = requests.get("https://api.example.com/data", timeout=10)
    r.raise_for_status()
    data = r.json()
except requests.exceptions.Timeout:
    print("Request timed out")
except requests.exceptions.HTTPError as e:
    print(f"HTTP error: {e.response.status_code}")
except requests.exceptions.ConnectionError:
    print("Connection failed")
except requests.exceptions.RequestException as e:
    print(f"Request failed: {e}")
```

---

## 📌 Summary

| Task                    | Syntax                                          |
|-------------------------|-------------------------------------------------|
| GET request             | `requests.get(url)`                             |
| POST JSON               | `requests.post(url, json={...})`                |
| With headers            | `requests.get(url, headers={"X-Key": "val"})`   |
| Auth header             | `headers={"Authorization": "Bearer token"}`     |
| Query params            | `requests.get(url, params={"k": "v"})`          |
| Timeout                 | `requests.get(url, timeout=10)`                 |
| Parse JSON response     | `r.json()`                                      |
| Check for errors        | `r.raise_for_status()`                          |
| Reuse connection        | `session = requests.Session()`                  |

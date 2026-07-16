---
title: 🖥️ subprocess — Running Commands
parent: Scripting
nav_order: 3
---

# 🖥️ subprocess — Running Commands

Running shell commands from Python scripts.

---

## 📦 Import

```python
import subprocess
```

---

## ✅ subprocess.run (Modern Standard)

```python
# Run command, wait for it to finish
result = subprocess.run(["ls", "-la", "/etc"])

# Capture output
result = subprocess.run(
    ["ls", "-la", "/etc"],
    capture_output=True,
    text=True
)
print(result.stdout)
print(result.stderr)
print(result.returncode)   # 0 = success

# Raise exception on failure
result = subprocess.run(
    ["systemctl", "status", "nginx"],
    capture_output=True,
    text=True,
    check=True    # Raises CalledProcessError if returncode != 0
)
```

---

## 📋 Common Patterns

```python
# Run shell command (string instead of list)
result = subprocess.run(
    "ps aux | grep nginx",
    shell=True,
    capture_output=True,
    text=True
)

# Get just the output as a string
def run(cmd):
    return subprocess.run(cmd, capture_output=True, text=True, check=True).stdout.strip()

hostname = run(["hostname", "-f"])
df_output = run(["df", "-h"])

# Check if command succeeded
result = subprocess.run(["ping", "-c", "1", "8.8.8.8"], capture_output=True)
if result.returncode == 0:
    print("Network reachable")

# Set timeout
try:
    result = subprocess.run(["curl", "https://example.com"], timeout=30, capture_output=True, text=True)
except subprocess.TimeoutExpired:
    print("Command timed out")
```

---

## 🔄 Streaming Output (Real-time)

```python
# Print output as it comes (no buffering)
process = subprocess.Popen(
    ["tail", "-f", "/var/log/syslog"],
    stdout=subprocess.PIPE,
    text=True
)

for line in process.stdout:
    print(line, end="")
    if "ERROR" in line:
        process.terminate()
        break
```

---

## 🌍 Environment Variables

```python
import os

# Pass custom env to subprocess
env = os.environ.copy()
env["MY_VAR"] = "custom_value"

result = subprocess.run(["printenv", "MY_VAR"], env=env, capture_output=True, text=True)
print(result.stdout)
```

---

## ⚠️ Security: Avoid shell=True with User Input

```python
# DANGEROUS — user input in shell=True can inject commands
user_input = "file.txt; rm -rf /"
subprocess.run(f"cat {user_input}", shell=True)  # Never do this

# SAFE — use list form, shell=False (default)
subprocess.run(["cat", user_input], capture_output=True)
```

---

## 📌 Summary

| Task                    | Syntax                                              |
|-------------------------|-----------------------------------------------------|
| Run command             | `subprocess.run(["cmd", "arg"])`                    |
| Capture output          | `run(..., capture_output=True, text=True)`          |
| Raise on failure        | `run(..., check=True)`                              |
| Get stdout as string    | `result.stdout.strip()`                             |
| Check return code       | `result.returncode`                                 |
| Set timeout             | `run(..., timeout=30)`                              |
| Shell pipeline          | `run("cmd1 \| cmd2", shell=True)`                   |
| Stream output           | `Popen(..., stdout=PIPE)`                           |

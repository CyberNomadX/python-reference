---
title: ⏰ Scheduling
parent: System Tools
nav_order: 3
---

# ⏰ Scheduling

Running tasks on a schedule from Python.

---

## ⏱️ Basic: time.sleep

```python
import time

while True:
    do_something()
    time.sleep(60)    # Wait 60 seconds
```

Simple but blocks the entire script and can drift over time.

---

## 📅 schedule Library

A simple, human-readable task scheduler:

```bash
pip install schedule
```

```python
import schedule
import time

def check_disk():
    import shutil
    usage = shutil.disk_usage("/")
    pct = usage.used / usage.total * 100
    if pct > 90:
        print(f"WARNING: Disk at {pct:.1f}%")

def send_report():
    print("Sending daily report...")

# Schedule jobs
schedule.every(5).minutes.do(check_disk)
schedule.every().hour.do(check_disk)
schedule.every().day.at("08:00").do(send_report)
schedule.every().monday.at("09:00").do(send_report)

# Run loop
while True:
    schedule.run_pending()
    time.sleep(1)
```

---

## 🏃 Run in Background Thread

```python
import schedule
import threading
import time

def job():
    print("Running job...")

schedule.every(10).minutes.do(job)

def run_schedule():
    while True:
        schedule.run_pending()
        time.sleep(1)

# Start scheduler in background thread
thread = threading.Thread(target=run_schedule, daemon=True)
thread.start()

# Your main program continues here
print("Main program running...")
```

---

## 🔁 threading.Timer (One-shot Delayed Execution)

```python
import threading

def delayed_task():
    print("Running after 30 seconds")

timer = threading.Timer(30.0, delayed_task)
timer.start()

# Cancel if needed
timer.cancel()
```

---

## 📋 datetime Utilities

```python
from datetime import datetime, timedelta, date
import time

# Current time
now = datetime.now()
today = date.today()
timestamp = time.time()    # Unix timestamp (float)

# Format
print(now.strftime("%Y-%m-%d %H:%M:%S"))   # 2024-01-15 08:32:01
print(today.isoformat())                    # 2024-01-15

# Arithmetic
tomorrow = today + timedelta(days=1)
one_hour_ago = now - timedelta(hours=1)
in_two_weeks = today + timedelta(weeks=2)

# Parse from string
dt = datetime.strptime("2024-01-15 08:32:01", "%Y-%m-%d %H:%M:%S")
```

---

## 📌 Summary

| Task                          | Syntax                                  |
|-------------------------------|-----------------------------------------|
| Sleep N seconds               | `time.sleep(60)`                        |
| Schedule every N minutes      | `schedule.every(5).minutes.do(fn)`      |
| Schedule daily at time        | `schedule.every().day.at("08:00").do(fn)` |
| Run pending jobs              | `schedule.run_pending()`                |
| Current datetime              | `datetime.now()`                        |
| Format datetime               | `dt.strftime("%Y-%m-%d %H:%M:%S")`      |
| Parse datetime string         | `datetime.strptime(s, fmt)`             |
| Add time                      | `dt + timedelta(hours=1)`               |
| Run scheduler in background   | `threading.Thread(target=run_schedule, daemon=True)` |

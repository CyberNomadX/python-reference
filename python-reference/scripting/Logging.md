---
title: 📋 logging Module
parent: Scripting
nav_order: 2
---

# 📋 logging Module

Proper logging for Python scripts — better than `print()`.

---

## 🔹 Basic Setup

```python
import logging

# Basic config (console output)
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S"
)

logging.debug("Debug detail")       # Not shown at INFO level
logging.info("Script started")
logging.warning("Low disk space")
logging.error("Failed to connect")
logging.critical("System going down")
```

---

## 📊 Log Levels

| Level      | Value | When to use                         |
|------------|-------|--------------------------------------|
| `DEBUG`    | 10    | Detailed diagnostic info             |
| `INFO`     | 20    | Confirmation things are working      |
| `WARNING`  | 30    | Something unexpected, but continuing |
| `ERROR`    | 40    | Serious problem, function failed     |
| `CRITICAL` | 50    | Program may not be able to continue  |

---

## 📁 Log to File

```python
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(name)s: %(message)s",
    handlers=[
        logging.FileHandler("/var/log/myscript.log"),
        logging.StreamHandler()    # Also print to console
    ]
)
```

---

## 🏗️ Logger Per Module (Best Practice)

```python
# In each module/script
logger = logging.getLogger(__name__)

def do_something():
    logger.info("Starting operation")
    try:
        result = risky_operation()
        logger.info(f"Success: {result}")
    except Exception as e:
        logger.error(f"Operation failed: {e}", exc_info=True)
```

---

## 🔄 Rotating Log Files

```python
import logging
from logging.handlers import RotatingFileHandler, TimedRotatingFileHandler

# Rotate by size (10MB, keep 5 backups)
handler = RotatingFileHandler(
    "/var/log/myscript.log",
    maxBytes=10 * 1024 * 1024,
    backupCount=5
)

# Rotate by time (daily, keep 30 days)
handler = TimedRotatingFileHandler(
    "/var/log/myscript.log",
    when="midnight",
    interval=1,
    backupCount=30
)

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(message)s",
    handlers=[handler, logging.StreamHandler()]
)
```

---

## ⚡ Quick Script Template

```python
import logging
import sys

def setup_logging(verbose=False):
    level = logging.DEBUG if verbose else logging.INFO
    logging.basicConfig(
        level=level,
        format="%(asctime)s [%(levelname)s] %(message)s",
        datefmt="%Y-%m-%d %H:%M:%S",
        handlers=[
            logging.StreamHandler(sys.stdout),
            logging.FileHandler("/var/log/myscript.log")
        ]
    )

logger = logging.getLogger(__name__)
```

---

## 📌 Summary

| Task                     | Syntax                                         |
|--------------------------|------------------------------------------------|
| Basic config             | `logging.basicConfig(level=logging.INFO, ...)`|
| Log a message            | `logging.info("message")`                      |
| Log with exception       | `logger.error("msg", exc_info=True)`           |
| Named logger             | `logger = logging.getLogger(__name__)`         |
| Log to file              | `handlers=[FileHandler("file.log")]`           |
| Log to file + console    | `handlers=[FileHandler(...), StreamHandler()]` |
| Rotating by size         | `RotatingFileHandler(maxBytes=10MB)`           |
| Rotating by time         | `TimedRotatingFileHandler(when="midnight")`    |

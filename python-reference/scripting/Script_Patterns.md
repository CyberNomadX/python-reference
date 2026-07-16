---
title: 🏗️ Script Patterns
parent: Scripting
nav_order: 4
---

# 🏗️ Script Patterns

Real-world patterns for writing reliable Python scripts.

---

## 📜 Script Template

```python
#!/usr/bin/env python3
"""
Brief description of what this script does.

Usage: script.py [options] <argument>
"""

import argparse
import logging
import sys
from pathlib import Path

# ── Logging ────────────────────────────────────────────
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S"
)
logger = logging.getLogger(__name__)


# ── Functions ──────────────────────────────────────────
def process(args):
    logger.info(f"Processing: {args.target}")
    # ... your logic here
    return 0


# ── CLI ────────────────────────────────────────────────
def parse_args():
    parser = argparse.ArgumentParser(description=__doc__)
    parser.add_argument("target", help="Target to process")
    parser.add_argument("--verbose", "-v", action="store_true")
    return parser.parse_args()


# ── Entry Point ────────────────────────────────────────
if __name__ == "__main__":
    args = parse_args()
    if args.verbose:
        logging.getLogger().setLevel(logging.DEBUG)
    sys.exit(process(args))
```

---

## 🛡️ Input Validation

```python
def validate_ip(ip: str) -> bool:
    import re
    pattern = r"^(\d{1,3}\.){3}\d{1,3}$"
    if not re.match(pattern, ip):
        return False
    return all(0 <= int(octet) <= 255 for octet in ip.split("."))

def validate_file(path: str) -> Path:
    p = Path(path)
    if not p.exists():
        raise argparse.ArgumentTypeError(f"File not found: {path}")
    if not p.is_file():
        raise argparse.ArgumentTypeError(f"Not a file: {path}")
    return p

# Use as argparse type
parser.add_argument("--config", type=validate_file)
```

---

## 🔄 Retry with Backoff

```python
import time
import functools

def retry(tries=3, delay=1, backoff=2):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            wait = delay
            for attempt in range(tries):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == tries - 1:
                        raise
                    logger.warning(f"Attempt {attempt+1} failed: {e}. Retrying in {wait}s...")
                    time.sleep(wait)
                    wait *= backoff
        return wrapper
    return decorator

@retry(tries=3, delay=2, backoff=2)
def fetch_data(url):
    import requests
    return requests.get(url, timeout=10).json()
```

---

## 🧹 Context Manager / Cleanup

```python
import tempfile
import contextlib

@contextlib.contextmanager
def temp_dir():
    """Create a temp directory and clean it up when done."""
    import shutil
    path = Path(tempfile.mkdtemp())
    try:
        yield path
    finally:
        shutil.rmtree(path, ignore_errors=True)

# Usage
with temp_dir() as tmp:
    (tmp / "work.txt").write_text("temporary data")
    # ... do work
# tmp is deleted automatically
```

---

## 📊 Progress for Long Operations

```python
# Simple progress without dependencies
def progress(current, total, prefix="Progress"):
    pct = current / total * 100
    bar = "█" * int(pct / 2) + "░" * (50 - int(pct / 2))
    print(f"\r{prefix}: [{bar}] {pct:.1f}%", end="", flush=True)
    if current == total:
        print()

for i, item in enumerate(items, 1):
    process(item)
    progress(i, len(items))
```

---

## 📌 Summary

| Pattern               | Purpose                               |
|-----------------------|---------------------------------------|
| `if __name__ == "__main__":` | Only run when executed directly |
| `sys.exit(code)`      | Proper exit with return code          |
| `@functools.wraps`    | Preserve function metadata in decorators |
| `contextlib.contextmanager` | Clean setup/teardown pattern  |
| `argparse.ArgumentTypeError` | Validation in argparse types  |
| `logger.exception()`  | Log error with full traceback         |

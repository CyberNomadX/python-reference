---
title: 🎛️ argparse — CLI Arguments
parent: Scripting
nav_order: 1
---

# 🎛️ argparse — CLI Arguments

Building proper command-line interfaces for Python scripts.

---

## 📦 Import

```python
import argparse
```

---

## 🔹 Basic Usage

```python
parser = argparse.ArgumentParser(
    description="My useful script"
)

# Positional argument (required)
parser.add_argument("host", help="Target hostname or IP")

# Optional argument
parser.add_argument("--port", type=int, default=80, help="Port number")

# Flag (boolean)
parser.add_argument("--verbose", "-v", action="store_true", help="Verbose output")

args = parser.parse_args()

print(f"Host: {args.host}")
print(f"Port: {args.port}")
if args.verbose:
    print("Verbose mode on")
```

Running:
```bash
python3 script.py myserver.com --port 443 -v
```

---

## 🛠️ Argument Types

```python
# String (default)
parser.add_argument("--name", type=str)

# Integer
parser.add_argument("--count", type=int, default=10)

# Float
parser.add_argument("--threshold", type=float, default=0.9)

# File (opens automatically)
parser.add_argument("--input", type=argparse.FileType("r"))
parser.add_argument("--output", type=argparse.FileType("w"))

# Choices (restrict to specific values)
parser.add_argument("--env", choices=["dev", "staging", "prod"])

# Multiple values
parser.add_argument("--hosts", nargs="+", help="One or more hosts")
parser.add_argument("--count", nargs="?", const=5, default=1)

# Required optional
parser.add_argument("--token", required=True)
```

---

## 📂 Subcommands

```python
parser = argparse.ArgumentParser()
subparsers = parser.add_subparsers(dest="command")

# 'start' subcommand
start = subparsers.add_parser("start", help="Start service")
start.add_argument("service")

# 'stop' subcommand
stop = subparsers.add_parser("stop", help="Stop service")
stop.add_argument("service")

args = parser.parse_args()

if args.command == "start":
    print(f"Starting {args.service}")
elif args.command == "stop":
    print(f"Stopping {args.service}")
```

Running:
```bash
python3 script.py start nginx
python3 script.py stop nginx
```

---

## 🔄 Complete Script Template

```python
#!/usr/bin/env python3
"""
Description of what this script does.
"""

import argparse
import sys


def main(args):
    print(f"Running against: {args.host}:{args.port}")
    if args.verbose:
        print(f"Verbose mode enabled")


def parse_args():
    parser = argparse.ArgumentParser(
        description=__doc__,
        formatter_class=argparse.RawDescriptionHelpFormatter
    )
    parser.add_argument("host", help="Target host")
    parser.add_argument("--port", "-p", type=int, default=22, help="Port (default: 22)")
    parser.add_argument("--verbose", "-v", action="store_true")
    return parser.parse_args()


if __name__ == "__main__":
    main(parse_args())
```

---

## 📌 Summary

| Task                     | Syntax                                           |
|--------------------------|--------------------------------------------------|
| Positional arg           | `parser.add_argument("name")`                    |
| Optional flag            | `parser.add_argument("--flag")`                  |
| Short + long             | `parser.add_argument("--verbose", "-v")`         |
| With default             | `parser.add_argument("--port", default=80)`      |
| Typed argument           | `parser.add_argument("--count", type=int)`       |
| Boolean flag             | `parser.add_argument("--dry-run", action="store_true")` |
| Required optional        | `parser.add_argument("--token", required=True)`  |
| Multiple values          | `parser.add_argument("--hosts", nargs="+")`      |
| Restricted choices       | `parser.add_argument("--env", choices=[...])`    |
| Parse args               | `args = parser.parse_args()`                     |

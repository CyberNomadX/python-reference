---
title: 🔌 Socket Basics
parent: Networking
nav_order: 2
---

# 🔌 Socket Basics

Low-level TCP/UDP networking with Python's built-in `socket` module.

---

## 📦 Import

```python
import socket
```

---

## 🔍 DNS and Host Info

```python
# Hostname to IP
ip = socket.gethostbyname("google.com")
print(ip)    # 142.250.80.46

# Reverse lookup (IP to hostname)
hostname, _, _ = socket.gethostbyaddr("8.8.8.8")
print(hostname)

# Local hostname
socket.gethostname()

# Local IP
socket.gethostbyname(socket.gethostname())
```

---

## 🔌 TCP Client

```python
import socket

host = "example.com"
port = 80

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.settimeout(5)
    s.connect((host, port))
    s.sendall(b"GET / HTTP/1.0\r\nHost: example.com\r\n\r\n")
    data = s.recv(1024)
    print(data.decode())
```

---

## 🖥️ TCP Server

```python
import socket
import threading

HOST = "0.0.0.0"
PORT = 9000

def handle_client(conn, addr):
    with conn:
        print(f"Connected: {addr}")
        while True:
            data = conn.recv(1024)
            if not data:
                break
            conn.sendall(data)   # Echo back

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    s.bind((HOST, PORT))
    s.listen()
    print(f"Listening on {HOST}:{PORT}")
    while True:
        conn, addr = s.accept()
        thread = threading.Thread(target=handle_client, args=(conn, addr))
        thread.start()
```

---

## ✅ Port Check (Common Pattern)

```python
import socket

def is_port_open(host: str, port: int, timeout: float = 3.0) -> bool:
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(timeout)
        try:
            s.connect((host, port))
            return True
        except (socket.timeout, ConnectionRefusedError, OSError):
            return False

# Usage
if is_port_open("192.168.1.10", 443):
    print("HTTPS port is open")
else:
    print("Port closed or unreachable")
```

---

## 📡 UDP

```python
# UDP client (connectionless — send and optionally receive)
with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as s:
    s.sendto(b"hello", ("192.168.1.10", 9000))
    data, addr = s.recvfrom(1024)
    print(f"Received from {addr}: {data}")
```

---

## 📌 Summary

| Task                     | Syntax                                         |
|--------------------------|------------------------------------------------|
| DNS lookup               | `socket.gethostbyname("host")`                 |
| Reverse DNS              | `socket.gethostbyaddr("ip")`                   |
| TCP socket               | `socket.socket(AF_INET, SOCK_STREAM)`          |
| UDP socket               | `socket.socket(AF_INET, SOCK_DGRAM)`           |
| Connect                  | `s.connect((host, port))`                      |
| Set timeout              | `s.settimeout(5)`                              |
| Send data                | `s.sendall(data)`                              |
| Receive data             | `s.recv(1024)`                                 |
| Check port open          | `try: s.connect((host, port))` + catch errors  |

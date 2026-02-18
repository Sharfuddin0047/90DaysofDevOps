# 📅 Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## 🎯 Objective

Understand DNS resolution, IP addressing, CIDR/subnetting, and ports in practical DevOps context.

---

# 🌍 Task 1 – DNS: How Names Become IPs

## 🧠 What Happens When I Type `google.com`?

1. Browser checks local DNS cache.
2. If not found, it asks the configured DNS resolver.
3. DNS resolver queries root → TLD (.com) → authoritative name server.
4. DNS returns an IP address (A/AAAA record).
5. Browser connects to that IP over TCP (usually port 443).

---

## 📌 DNS Record Types

* **A** → Maps domain to IPv4 address
* **AAAA** → Maps domain to IPv6 address
* **CNAME** → Alias of another domain
* **MX** → Mail server record
* **NS** → Name server responsible for domain

---

## 🔎 Command Run

```bash
dig google.com
```

### Observation

* A Record: `142.250.xx.xx`
* TTL: e.g., `300` seconds

---

# 🧮 Task 2 – IP Addressing

## 🔹 What is IPv4?

An IPv4 address is a 32-bit number written in dotted decimal format:

Example:

```
192.168.1.10
```

Structure:

* 4 octets (8 bits each)
* Range: 0–255 per octet

---

## 🔹 Public vs Private IP

* **Public IP** → Accessible on the internet
  Example: `8.8.8.8`

* **Private IP** → Used inside local networks
  Example: `192.168.1.5`

---

## 🔹 Private IP Ranges

* `10.0.0.0 – 10.255.255.255`
* `172.16.0.0 – 172.31.255.255`
* `192.168.0.0 – 192.168.255.255`

---

## 🔎 Command Run

```bash
ip addr show
```

### Observation

My IP:
`192.168.x.x` → Private IP


---

# 🧩 Task 3 – CIDR & Subnetting

## 🔹 What Does `/24` Mean?

`192.168.1.0/24`

* 24 bits are network portion
* 8 bits for hosts
* Subnet mask: `255.255.255.0`

---

## 🔹 Usable Hosts

Formula:

```
2^n - 2
```

| CIDR | Host Bits | Usable Hosts |
| ---- | --------- | ------------ |
| /24  | 8         | 254          |
| /16  | 16        | 65,534       |
| /28  | 4         | 14           |

---

## 🔹 Why Do We Subnet?

* Better IP management
* Security isolation
* Reduce broadcast traffic
* Efficient IP usage

---

## 📊 CIDR Table

| CIDR | Subnet Mask     | Total IPs | Usable Hosts |
| ---- | --------------- | --------- | ------------ |
| /24  | 255.255.255.0   | 256       | 254          |
| /16  | 255.255.0.0     | 65,536    | 65,534       |
| /28  | 255.255.255.240 | 16        | 14           |

---

# 🚪 Task 4 – Ports

## 🔹 What is a Port?

A port is a logical communication endpoint.

IP = Building
Port = Door

Multiple services can run on one IP using different ports.

---

## 📌 Common Ports

| Port  | Service |
| ----- | ------- |
| 22    | SSH     |
| 80    | HTTP    |
| 443   | HTTPS   |
| 53    | DNS     |
| 3306  | MySQL   |
| 6379  | Redis   |
| 27017 | MongoDB |

---

## 🔎 Command Run

```bash
ss -tulpn
```

### Example Observation

* Port 22 → sshd
* Port 631 → cups

---

# 🔗 Task 5 – Putting It Together

## 🔹 `curl http://myapp.com:8080`

Concepts involved:

* DNS resolves `myapp.com`
* TCP connection established
* Port 8080 used
* HTTP protocol request sent

Layers involved:
Application → Transport → Internet → Link

---

## 🔹 App Can't Reach DB at `10.0.1.50:3306`

First checks:

1. Is port 3306 open? (`ss -tulpn` on DB server)
2. Network connectivity? (`ping 10.0.1.50`)
3. Firewall rules?
4. DB service running?

---

# 🧠 What I Learned (3 Key Points)

1. DNS resolution is a multi-step hierarchical process.
2. CIDR helps control IP allocation and segmentation.
3. Ports allow multiple services on one machine.

---

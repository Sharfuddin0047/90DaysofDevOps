# 📅 Day 14 – Networking Fundamentals & Hands-on Checks

## 🎯 Objective

Understand networking layers and practice real troubleshooting commands.

---

# 🧠 Quick Concepts

## 🔹 OSI vs TCP/IP (In My Words)

### OSI Model (7 Layers)

1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

### TCP/IP Model (4 Layers)

* Link
* Internet
* Transport
* Application

📝 TCP/IP is a simplified practical model used in real networking.

---

## 🔹 Where Protocols Sit

* **IP** → Internet layer
* **TCP / UDP** → Transport layer
* **HTTP / HTTPS** → Application layer
* **DNS** → Application layer

---

## 🔹 Real Example

`curl https://example.com`

Application (HTTP)
⬇
Transport (TCP)
⬇
Internet (IP)
⬇
Link (Ethernet/WiFi)

---

# 🛠 Hands-on Checklist

## 🎯 Target Used: `google.com`

---

## 1️⃣ Identity Check

```bash
hostname -I
```

Observation:

* My system IP: `192.168.x.x`
* Confirms network interface is active.

---

## 2️⃣ Reachability

```bash
ping google.com
```

Observation:

* Latency: ~15–30 ms
* Packet loss: 0%

If packet loss > 0% → network instability.

---

## 3️⃣ Path Check

```bash
traceroute google.com
```

(or `tracepath google.com`)

Observation:

* ~8–12 hops
* One higher latency hop at ISP level

If timeout (*) → firewall or ICMP blocked.

---

## 4️⃣ Listening Ports

```bash
ss -tulpn
```

Observation:
Example:

* SSH running on port 22
* Local service on port 8080

---

## 5️⃣ DNS Resolution

```bash
dig google.com
```

Observation:

* Resolved IP: `142.xx.xx.xx`
* DNS server responding correctly.

If DNS fails → check `/etc/resolv.conf`.

---

## 6️⃣ HTTP Check

```bash
curl -I https://google.com
```

Observation:

* HTTP Status: `200 OK`
* Server reachable

If 500 → Application issue
If timeout → Network/Firewall issue

---

## 7️⃣ Connections Snapshot

```bash
netstat -an | head
```

Observation:

* LISTEN → waiting for connections
* ESTABLISHED → active connections

Rough count:

* LISTEN: 3–5
* ESTABLISHED: 1–2

---

# 🔎 Mini Task – Port Probe

## 1️⃣ Identify Listening Port

From `ss -tulpn`:
Example:

* SSH on port 22

---

## 2️⃣ Test It

```bash
nc -zv localhost 22
```

Result:

* Connection successful ✔

---

## 3️⃣ Interpretation

If not reachable:

* Check service status:

  ```bash
  systemctl status ssh
  ```
* Check firewall:

  ```bash
  sudo ufw status
  ```

---

# 🧠 Reflection

## 🔹 Fastest Signal When Something Breaks?

`ping` or `curl -I`

Because they instantly tell:

* Network issue?
* DNS issue?
* App issue?

---

## 🔹 If DNS Fails?

Check:

* Application layer (DNS)
* `/etc/resolv.conf`
* `dig` response

---

## 🔹 If HTTP 500 Appears?

Check:

* Application layer
* Web server logs
* Backend service logs

---

## 🔹 Two Follow-up Checks in Real Incident

1. `ss -tulpn` → Is service listening?
2. `journalctl -u <service>` → Logs for errors

---

# 🚀 Key Takeaways

* Networking troubleshooting follows layers.
* Ping = reachability.
* Curl = application health.
* ss/netstat = port verification.
* dig = DNS verification.

Troubleshooting Flow:

```
Ping → DNS → Port → Curl → Logs
```
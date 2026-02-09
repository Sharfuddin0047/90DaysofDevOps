# 🐧 Linux Practice – Processes and Services

This practice focuses on running real Linux commands to inspect processes, services, and logs while building troubleshooting confidence.

---

## ✅ Process Checks

### 1️⃣ View Running Processes
**Command:**
```bash
ps aux | head
```

**Output Observed:**
- Displayed running processes with USER, PID, CPU, and MEMORY usage.
- Confirmed multiple background services are active.

**Learning:**  
`ps aux` is useful for quickly identifying resource-heavy or unusual processes.

---

### 2️⃣ Real-Time Monitoring
**Command:**
```bash
top
```

**Output Observed:**
- Observed live CPU and memory usage.
- Identified processes consuming the most resources.

**Learning:**  
`top` helps detect performance bottlenecks instantly.

---

## ✅ Service Checks

**Service Chosen:** `cron` (Linux job scheduler)

---

### 3️⃣ Check Service Status
**Command:**
```bash
systemctl status cron
```

**Output Observed:**
- Service showed **active (running)**.
- Displayed uptime and recent logs.

**Learning:**  
Always check service status first during troubleshooting.

---

### 4️⃣ List Running Services
**Command:**
```bash
systemctl list-units --type=service --state=running
```

**Output Observed:**
- Listed all active services.
- Helped confirm that essential services are operational.

**Learning:**  
Provides a quick health overview of the system.

---

## ✅ Log Checks

### 5️⃣ Inspect Service Logs
**Command:**
```bash
journalctl -u cron --since "1 hour ago"
```

**Output Observed:**
- Displayed recent cron activity.
- No errors were detected.

**Learning:**  
`journalctl` is critical for investigating service behavior.

---

### 6️⃣ View Recent System Logs
**Command:**
```bash
tail -n 50 /var/log/syslog
```

**Output Observed:**
- Showed the latest system events.
- Confirmed normal system operations.

**Learning:**  
`tail` is excellent for quickly reviewing recent log entries.

---

## 🔧 Mini Troubleshooting Flow

**Scenario:** A scheduled job is not running.

### Steps:

✅ **1. Check if the service is running**
```bash
systemctl status cron
```

✅ **2. Verify recent logs**
```bash
journalctl -u cron
```

✅ **3. Search for errors**
```bash
grep cron /var/log/syslog
```

**Result:**  
The service was healthy with no failures detected.

---

## ⭐ Key Takeaways

- Follow a structured troubleshooting approach:  
  👉 Check processes → Verify service → Inspect logs  

- Logs often provide the fastest clues during incidents.

- Regular practice builds confidence and speed — essential skills for DevOps engineers.

---

✅ **Tip:** Run these commands multiple times on your system until they become muscle memory.

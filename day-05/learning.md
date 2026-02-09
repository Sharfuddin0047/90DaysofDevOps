# 🛠️ Linux Troubleshooting Runbook – CPU, Memory, and Logs

This runbook documents a focused troubleshooting drill performed on a running Linux service.  
It captures system health, reviews logs, and outlines next steps if the issue escalates.

---

## 🎯 Target Service / Process

**Service chosen:** `cron`  
Reason: Core system service, always running, easy to inspect logs and behavior.

---

## 🖥️ Environment Basics

### 1️⃣ System Information
**Command:**
```bash
uname -a
```

**Observation:**  
Shows kernel version, architecture, and OS type.

---

### 2️⃣ OS Details
**Command:**
```bash
cat /etc/os-release
```

**Observation:**  
Confirmed Linux distribution and version for context during troubleshooting.

---

## 📁 Filesystem Sanity Check

### 3️⃣ Create Temporary Directory
**Command:**
```bash
mkdir /tmp/runbook-demo
```

**Observation:**  
Directory created successfully, filesystem is writable.

---

### 4️⃣ Copy and Verify File
**Command:**
```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo
```

**Observation:**  
File copied correctly, permissions and ownership look normal.

---

## ⚙️ CPU & Memory Snapshot

### 5️⃣ Real-Time Resource Usage
**Command:**
```bash
top
```

**Observation:**  
CPU usage low, no abnormal spikes. `cron` process consuming negligible resources.

---

### 6️⃣ Memory Usage
**Command:**
```bash
free -h
```

**Observation:**  
Sufficient free and available memory, no swap pressure observed.

---

## 💽 Disk & IO Snapshot

### 7️⃣ Disk Space Usage
**Command:**
```bash
df -h
```

**Observation:**  
Root filesystem has sufficient free space; no partitions near full.

---

### 8️⃣ Log Directory Size
**Command:**
```bash
du -sh /var/log
```

**Observation:**  
Log directory size within reasonable limits, no runaway log growth.

---

## 🌐 Network Snapshot

### 9️⃣ Listening Ports and Services
**Command:**
```bash
ss -tulpn
```

**Observation:**  
No unexpected ports open; system services listening as expected.

---

### 🔟 Connectivity Test
**Command:**
```bash
ping -c 3 google.com
```

**Observation:**  
Network connectivity healthy with normal latency.

---

## 📜 Logs Reviewed

### 1️⃣1️⃣ Service Logs
**Command:**
```bash
journalctl -u cron -n 50
```

**Observation:**  
Recent cron activity visible, no errors or warnings.

---

### 1️⃣2️⃣ System Logs
**Command:**
```bash
tail -n 50 /var/log/syslog
```

**Observation:**  
No critical errors related to `cron` or system stability.

---

## ✅ Quick Findings

- System is stable with low CPU and memory usage.
- Disk space and logs are under control.
- Target service (`cron`) is active and behaving normally.
- No immediate action required.

---

## 🚨 If This Worsens (Next Steps)

1. Restart the service safely:
```bash
systemctl restart cron
```

2. Increase log inspection window:
```bash
journalctl -u cron --since "24 hours ago"
```

3. Capture deeper diagnostics:
- Enable debug logs (if supported)
- Collect `strace` on the process
- Check related scheduled jobs and permissions

---

## 🧠 Key Takeaway

A structured checklist helps avoid panic during incidents.  
Always **capture evidence first**, then act.

---

✅ This runbook can be reused and adapted for any Linux service in production.

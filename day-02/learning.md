Here is your **properly formatted `.md` file** with fixed headings, spacing, code blocks, and consistency:

````md
# 🐧 Linux Architecture Notes  
**File:** linux-architecture-notes.md  

---

## 1️⃣ Core Components of Linux

### 🔹 Kernel
- The **core of the OS**
- Directly interacts with hardware
- Responsible for:
  - Process management  
  - Memory management  
  - Device drivers  
  - File systems  
- Runs in **kernel space** (high privilege)

👉 Users never interact with the kernel directly.

---

### 🔹 User Space
- Where **users and applications** run
- Includes:
  - Shell (bash, zsh)  
  - System utilities (`ls`, `cp`, `ps`)  
  - Applications  
- Limited privileges → safer  

👉 User space programs request services from the kernel using **system calls**.

---

### 🔹 Init / systemd
- The **first process** started by the kernel (**PID = 1**)
- Manages:
  - System startup  
  - Services  
  - Background processes (daemons)  

👉 Modern Linux distributions use **systemd** as the init system.

---

## 2️⃣ Process Creation & Management

### 🔹 How a Process is Created
1. User runs a command (e.g., `ls`)  
2. Shell calls **fork()** → creates a new process  
3. New process calls **exec()** → loads the program  
4. Kernel assigns a **PID (Process ID)**  

---

### 🔹 Process States
- **Running (R):** Currently executing on CPU  
- **Sleeping (S):** Waiting for an event or I/O  
- **Uninterruptible Sleep (D):** Waiting for disk/network I/O  
- **Stopped (T):** Paused manually (e.g., `Ctrl + Z`)  
- **Zombie (Z):** Finished execution but parent hasn’t collected its status  

👉 Too many zombie processes may indicate poorly managed parent processes.

---

## 3️⃣ What systemd Does (And Why It Matters)

### 🔹 systemd Responsibilities
- Starts services in parallel → faster boot time  
- Restarts failed services automatically  
- Manages logs using `journalctl`  
- Handles service dependencies  

Example:

```bash
systemctl status nginx
````

---

### 🔹 Why systemd is Important for DevOps

* Used by most modern Linux servers
* Critical for:

  * Service troubleshooting
  * Deployment automation
  * High availability & reliability

👉 If a production service crashes, **systemd can restart it automatically.**

---

## 4️⃣ Daily Linux Commands (Must-Know)

```bash
ps aux        # View running processes
top / htop    # Live system monitoring
systemctl     # Manage services
journalctl    # View system logs
kill / kill -9 <PID>   # Stop processes
```

---

## ✅ Key Takeaways

* Kernel controls the system
* User space runs applications
* systemd keeps services running
* Understanding processes = faster debugging

👉 **Linux knowledge is the backbone of DevOps troubleshooting.**
```

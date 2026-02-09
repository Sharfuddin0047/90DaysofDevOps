# 🐧 Linux Commands Cheat Sheet

A quick reference for essential Linux commands used in real-world troubleshooting and DevOps environments.

---

## 📁 File System Commands

| Command | Usage |
|--------|--------|
| `ls -la` | List all files including hidden files with permissions |
| `pwd` | Display current directory path |
| `cd <dir>` | Change directory |
| `mkdir <name>` | Create a new directory |
| `rm -rf <dir>` | Remove directory recursively |
| `cp -r src dest` | Copy files or directories |
| `mv old new` | Move or rename files |
| `touch file.txt` | Create an empty file |
| `find / -name file` | Search for a file in the system |
| `du -sh *` | Show directory sizes |
| `df -h` | Display disk space usage in human-readable format |

---

## ⚙️ Process Management

| Command | Usage |
|--------|--------|
| `ps aux` | View all running processes |
| `top` | Real-time system resource usage |
| `htop` | Interactive process viewer (better than top) |
| `kill <PID>` | Terminate a process by PID |
| `kill -9 <PID>` | Force kill a process |
| `pkill <name>` | Kill processes by name |
| `free -h` | Show memory usage |
| `uptime` | Display system uptime and load average |
| `nice` | Start a process with a specific priority |
| `renice` | Change priority of a running process |

---

## 🌐 Networking Commands

| Command | Usage |
|--------|--------|
| `ping google.com` | Test network connectivity |
| `ip addr` | Show IP addresses and network interfaces |
| `curl <url>` | Transfer data from or to a server (test APIs/websites) |
| `dig google.com` | Perform DNS lookup |
| `netstat -tulnp` | Show listening ports and associated processes |
| `ss -tuln` | Modern replacement for netstat |
| `traceroute google.com` | Trace the path packets take to a host |

---

## 📜 Logs & Troubleshooting

| Command | Usage |
|--------|--------|
| `tail -f /var/log/syslog` | Monitor logs in real time |
| `less file.log` | View large log files efficiently |
| `head file.log` | Show the first few lines of a file |
| `grep "error" file.log` | Search for specific patterns in logs |
| `journalctl -xe` | View detailed systemd logs |

---

## ⭐ Most Used in Production

These commands solve a large percentage of real-world production issues:

- `top` → Detect CPU or memory spikes  
- `df -h` → Identify disk space problems  
- `tail -f` → Monitor logs live  
- `ss -tuln` → Debug port and service issues  
- `ps aux` → Inspect running processes  

---

✅ **Tip:** Mastering these commands will help you troubleshoot faster, reduce downtime, and build strong operational confidence — a critical skill for every DevOps engineer.

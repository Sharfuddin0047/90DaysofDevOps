# 📅 Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## 🎯 Objective

Apply:

* Functions
* Strict mode
* Arguments
* Loops
* Error handling
* Cron scheduling

---

# 🟢 Task 1 – Log Rotation Script

## 📄 `log_rotate.sh`

```bash
#!/bin/bash
set -euo pipefail

LOG_DIR="${1:-}"

if [ -z "$LOG_DIR" ]; then
    echo "Usage: $0 <log_directory>"
    exit 1
fi

if [ ! -d "$LOG_DIR" ]; then
    echo "Error: Directory does not exist."
    exit 1
fi

echo "Rotating logs in $LOG_DIR"

# Compress .log files older than 7 days
COMPRESSED=$(find "$LOG_DIR" -type f -name "*.log" -mtime +7 -print -exec gzip {} \; | wc -l)

# Delete .gz files older than 30 days
DELETED=$(find "$LOG_DIR" -type f -name "*.gz" -mtime +30 -print -delete | wc -l)

echo "Compressed files: $COMPRESSED"
echo "Deleted old archives: $DELETED"
```

---

# 🟡 Task 2 – Backup Script

## 📄 `backup.sh`

```bash
#!/bin/bash
set -euo pipefail

SOURCE="${1:-}"
DEST="${2:-}"

if [ -z "$SOURCE" ] || [ -z "$DEST" ]; then
    echo "Usage: $0 <source_directory> <backup_destination>"
    exit 1
fi

if [ ! -d "$SOURCE" ]; then
    echo "Error: Source directory does not exist."
    exit 1
fi

mkdir -p "$DEST"

TIMESTAMP=$(date +%Y-%m-%d)
ARCHIVE="$DEST/backup-$TIMESTAMP.tar.gz"

tar -czf "$ARCHIVE" "$SOURCE"

if [ -f "$ARCHIVE" ]; then
    echo "Backup created: $ARCHIVE"
    du -h "$ARCHIVE"
else
    echo "Backup failed!"
    exit 1
fi

# Delete backups older than 14 days
find "$DEST" -type f -name "backup-*.tar.gz" -mtime +14 -delete
```

---

# 🔵 Task 3 – Crontab

## 🔎 Current Schedule

```bash
crontab -l
```

(Write what you saw here)

---

## 📌 Cron Syntax

```
* * * * *  command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

---

## 🗓 Required Cron Entries

### 🔹 Log Rotation – Daily at 2 AM

```bash
0 2 * * * /path/to/log_rotate.sh /var/log/myapp
```

---

### 🔹 Backup – Every Sunday at 3 AM

```bash
0 3 * * 0 /path/to/backup.sh /source /backup
```

---

### 🔹 Health Check – Every 5 Minutes

```bash
*/5 * * * * /path/to/health_check.sh
```

---

# 🔴 Task 4 – Maintenance Script

## 📄 `maintenance.sh`

```bash
#!/bin/bash
set -euo pipefail

LOGFILE="/var/log/maintenance.log"

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> "$LOGFILE"
}

run_log_rotation() {
    log "Starting log rotation..."
    ./log_rotate.sh /var/log/myapp >> "$LOGFILE" 2>&1
    log "Log rotation completed."
}

run_backup() {
    log "Starting backup..."
    ./backup.sh /home/user/data /backup >> "$LOGFILE" 2>&1
    log "Backup completed."
}

main() {
    log "Maintenance job started"
    run_log_rotation
    run_backup
    log "Maintenance job finished"
}

main
```

---

## 📅 Cron Entry for Maintenance (Daily 1 AM)

```bash
0 1 * * * /path/to/maintenance.sh
```

---

# 🧪 Sample Output (Example)

```
2026-02-08 01:00:00 - Maintenance job started
Compressed files: 3
Deleted old archives: 1
Backup created: /backup/backup-2026-02-08.tar.gz
2026-02-08 01:01:15 - Maintenance job finished
```

---

# 🧠 What I Learned (3 Key Points)

1. Automation becomes powerful when combined with cron.
2. Log rotation and backups are real production tasks.
3. Strict mode prevents silent automation failures.

---

# 🚀 Real DevOps Relevance

These patterns are used in:

* Production log management
* Server maintenance automation
* CI/CD artifact backups
* Scheduled health checks
* Disaster recovery preparation

This is real infrastructure-level scripting.

---

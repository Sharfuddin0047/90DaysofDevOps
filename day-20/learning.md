# ✅ `log_analyzer.sh`

```bash
#!/bin/bash

set -euo pipefail

# -----------------------------
# Task 1: Input & Validation
# -----------------------------

if [[ $# -ne 1 ]]; then
    echo "Usage: $0 <log_file>"
    exit 1
fi

LOG_FILE="$1"

if [[ ! -f "$LOG_FILE" ]]; then
    echo "Error: File '$LOG_FILE' does not exist."
    exit 1
fi

DATE=$(date +%Y-%m-%d)
REPORT_FILE="log_report_${DATE}.txt"

echo "Analyzing log file: $LOG_FILE"
echo

# -----------------------------
# Task 2: Error Count
# -----------------------------

ERROR_COUNT=$(grep -Eci "ERROR|Failed" "$LOG_FILE" || true)
TOTAL_LINES=$(wc -l < "$LOG_FILE")

echo "Total Errors (ERROR/Failed): $ERROR_COUNT"

# -----------------------------
# Task 3: Critical Events
# -----------------------------

CRITICAL_EVENTS=$(grep -n "CRITICAL" "$LOG_FILE" || true)

echo
echo "--- Critical Events ---"
if [[ -z "$CRITICAL_EVENTS" ]]; then
    echo "No critical events found."
else
    echo "$CRITICAL_EVENTS"
fi

# -----------------------------
# Task 4: Top 5 Error Messages
# -----------------------------

TOP_ERRORS=$(grep "ERROR" "$LOG_FILE" \
    | sed -E 's/^[^ ]+ [^ ]+ [^ ]+ //' \
    | sort \
    | uniq -c \
    | sort -rn \
    | head -5)

echo
echo "--- Top 5 Error Messages ---"
if [[ -z "$TOP_ERRORS" ]]; then
    echo "No ERROR messages found."
else
    echo "$TOP_ERRORS"
fi

# -----------------------------
# Task 5: Generate Report
# -----------------------------

{
    echo "Log Analysis Report"
    echo "===================="
    echo "Date: $(date)"
    echo "Log File: $LOG_FILE"
    echo "Total Lines: $TOTAL_LINES"
    echo "Total Errors (ERROR/Failed): $ERROR_COUNT"
    echo
    echo "--- Top 5 Error Messages ---"
    echo "$TOP_ERRORS"
    echo
    echo "--- Critical Events ---"
    if [[ -z "$CRITICAL_EVENTS" ]]; then
        echo "No critical events found."
    else
        echo "$CRITICAL_EVENTS"
    fi
} > "$REPORT_FILE"

echo
echo "Report generated: $REPORT_FILE"

# -----------------------------
# Task 6 (Optional): Archive
# -----------------------------

ARCHIVE_DIR="archive"

mkdir -p "$ARCHIVE_DIR"
mv "$LOG_FILE" "$ARCHIVE_DIR/"

echo "Log file moved to $ARCHIVE_DIR/"
```

---

# ✅ Sample Console Output

```
$ ./log_analyzer.sh sample_log.log

Analyzing log file: sample_log.log

Total Errors (ERROR/Failed): 63

--- Critical Events ---
84:2025-07-29 10:15:23 CRITICAL Disk space below threshold
217:2025-07-29 14:32:01 CRITICAL Database connection lost

--- Top 5 Error Messages ---
45 Connection timed out
32 File not found
28 Permission denied
15 Disk I/O error
9 Out of memory

Report generated: log_report_2026-02-18.txt
Log file moved to archive/
```

---

# ✅ `day-20-solution.md`

You can use this content for your markdown submission:

---

# Day 20 – Log Analyzer & Report Generator

## 📌 Objective

Build a Bash script that analyzes system logs and generates a summary report.

---

## 🛠 Tools Used

* `grep` → Search patterns
* `grep -c` → Count matches
* `grep -n` → Show line numbers
* `wc -l` → Count total lines
* `sort`
* `uniq -c`
* `head`
* `sed`
* `date`
* `mv`
* `mkdir -p`

---

## 🔍 Features Implemented

### 1️⃣ Input Validation

* Script exits if no argument is passed.
* Script exits if file doesn't exist.
* Uses `set -euo pipefail` for safer execution.

---

### 2️⃣ Error Count

```bash
grep -Eci "ERROR|Failed"
```

Counts case-insensitive matches of ERROR and Failed.

---

### 3️⃣ Critical Events

```bash
grep -n "CRITICAL"
```

Prints critical log entries with line numbers.

---

### 4️⃣ Top 5 Error Messages

```bash
grep "ERROR" logfile \
| sed -E 's/^[^ ]+ [^ ]+ [^ ]+ //' \
| sort \
| uniq -c \
| sort -rn \
| head -5
```

Steps:

* Extract ERROR lines
* Remove timestamp
* Count duplicates
* Sort descending
* Show top 5

---

### 5️⃣ Report Generation

Creates:

```
log_report_<date>.txt
```

Includes:

* Date
* Log file name
* Total lines
* Total errors
* Top 5 errors
* Critical events

---

### 6️⃣ Archive Feature

* Creates `archive/` directory if missing
* Moves processed log file
* Prints confirmation message

---

## 📚 What I Learned (3 Key Points)

1. How to chain multiple Linux text-processing tools effectively.
2. How `set -euo pipefail` makes scripts production-safe.
3. How to generate automated reports from raw logs.

---


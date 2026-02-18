# 📅 Day 18 – Shell Scripting: Functions & Slightly Advanced Concepts

## 🎯 Objective

Learn:

* Functions
* Return values
* Local variables
* `set -euo pipefail`
* Structured, reusable scripting

---

# 🟢 Task 1 – Basic Functions

## 📄 `functions.sh`

```bash
#!/bin/bash

greet() {
    local NAME="$1"
    echo "Hello, $NAME!"
}

add() {
    local NUM1="$1"
    local NUM2="$2"
    local SUM=$((NUM1 + NUM2))
    echo "Sum: $SUM"
}

# Calling functions
greet "Shubham"
add 5 7
```

### ✅ Output

```
Hello, Shubham!
Sum: 12
```

---

# 🟡 Task 2 – Functions with Return Values

## 📄 `disk_check.sh`

```bash
#!/bin/bash

check_disk() {
    echo "Disk Usage:"
    df -h /
}

check_memory() {
    echo "Memory Usage:"
    free -h
}

main() {
    check_disk
    echo "-----------------------"
    check_memory
}

main
```

### ✅ Output (Example)

```
Disk Usage:
Filesystem  Size  Used Avail Use% Mounted on
/dev/sda1    50G   20G   28G  42% /

Memory Usage:
              total   used   free
Mem:            8G     3G     4G
```

---

# 🔵 Task 3 – Strict Mode (`set -euo pipefail`)

## 📄 `strict_demo.sh`

```bash
#!/bin/bash
set -euo pipefail

echo "Testing strict mode"

# Undefined variable test
echo "$UNDEFINED_VAR"

# Command failure test
false

# Pipe failure test
grep "text" nonexistent_file | sort
```

---

## 🔎 What Happens?

### 🔹 `set -e`

Script exits immediately if any command fails.

### 🔹 `set -u`

Script exits if an undefined variable is used.

### 🔹 `set -o pipefail`

If any command in a pipeline fails, the whole pipeline fails.

---

## 📌 Explanation

* `set -e` → Exit on command error
* `set -u` → Exit on undefined variable
* `set -o pipefail` → Catch failures inside pipelines

💡 Together, they make scripts production-safe.

---

# 🟣 Task 4 – Local Variables

## 📄 `local_demo.sh`

```bash
#!/bin/bash

global_var="I am global"

demo_local() {
    local local_var="I am local"
    echo "$local_var"
}

demo_global() {
    global_var="Modified global"
}

demo_local
echo "$local_var"   # Will be empty

demo_global
echo "$global_var"  # Modified
```

### ✅ Observation

* `local_var` is not accessible outside function.
* `global_var` changes globally.

---

# 🔴 Task 5 – System Info Reporter

## 📄 `system_info.sh`

```bash
#!/bin/bash
set -euo pipefail

print_header() {
    echo "================================="
    echo "$1"
    echo "================================="
}

system_info() {
    print_header "System Information"
    echo "Hostname: $(hostname)"
    echo "OS: $(uname -a)"
}

uptime_info() {
    print_header "Uptime"
    uptime
}

disk_usage() {
    print_header "Top 5 Disk Usage"
    df -h | head -n 6
}

memory_usage() {
    print_header "Memory Usage"
    free -h
}

top_cpu() {
    print_header "Top 5 CPU Processes"
    ps aux --sort=-%cpu | head -n 6
}

main() {
    system_info
    uptime_info
    disk_usage
    memory_usage
    top_cpu
}

main
```

---

## ✅ Sample Output Structure

```
=================================
System Information
=================================
Hostname: dev-server
OS: Linux ...

=================================
Uptime
=================================
 10:45 up 2 days,  3:21,  1 user

=================================
Memory Usage
=================================
...
```

Clean. Structured. Reusable. Production-style.

---

# 🧠 What I Learned (3 Key Points)

1. Functions make scripts modular and reusable.
2. `set -euo pipefail` prevents silent failures.
3. `local` variables protect script scope.

---

# 🚀 Real DevOps Impact

These skills are used in:

* Deployment automation
* Health check scripts
* CI/CD helpers
* Server bootstrap scripts
* Monitoring scripts

You are now writing **structured automation**, not just commands.

---

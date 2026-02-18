# 🐚 Shell Scripting Cheat Sheet

**Day 21 – Personal Reference Guide**

---

# 📌 Quick Reference Table

| Topic    | Key Syntax               | Example                            |
| -------- | ------------------------ | ---------------------------------- |
| Variable | `VAR="value"`            | `NAME="DevOps"`                    |
| Argument | `$1`, `$2`               | `./script.sh arg1`                 |
| If       | `if [ condition ]; then` | `if [ -f file ]; then`             |
| For loop | `for i in list; do`      | `for i in 1 2 3; do`               |
| Function | `name() { ... }`         | `greet() { echo "Hi"; }`           |
| Grep     | `grep pattern file`      | `grep -i "error" log.txt`          |
| Awk      | `awk '{print $1}' file`  | `awk -F: '{print $1}' /etc/passwd` |
| Sed      | `sed 's/old/new/g' file` | `sed -i 's/foo/bar/g' config.txt`  |

---

# 1️⃣ Basics

## Shebang

```bash
#!/bin/bash
```

Tells the OS to use Bash interpreter.

---

## Run a Script

```bash
chmod +x script.sh
./script.sh
bash script.sh
```

---

## Comments

```bash
# Single line comment
echo "Hello" # Inline comment
```

---

## Variables

```bash
NAME="DevOps"
echo $NAME
echo "$NAME"
echo '$NAME'
```

* `$VAR` → value
* `"$VAR"` → safe quoting
* `'$VAR'` → literal

---

## Read User Input

```bash
read -p "Enter name: " NAME
echo "Hello $NAME"
```

---

## Command-Line Arguments

```bash
echo $0   # Script name
echo $1   # First argument
echo $#   # Number of arguments
echo $@   # All arguments
echo $?   # Last command exit code
```

---

# 2️⃣ Operators & Conditionals

## String Comparison

```bash
[ "$a" = "$b" ]
[ "$a" != "$b" ]
[ -z "$a" ]   # empty
[ -n "$a" ]   # not empty
```

---

## Integer Comparison

```bash
[ "$a" -eq "$b" ]
[ "$a" -ne "$b" ]
[ "$a" -lt "$b" ]
[ "$a" -gt "$b" ]
[ "$a" -le "$b" ]
[ "$a" -ge "$b" ]
```

---

## File Test Operators

```bash
-f file   # regular file
-d dir    # directory
-e file   # exists
-r file   # readable
-w file   # writable
-x file   # executable
-s file   # not empty
```

---

## If / Elif / Else

```bash
if [ -f file.txt ]; then
    echo "File exists"
elif [ -d dir ]; then
    echo "Directory exists"
else
    echo "Not found"
fi
```

---

## Logical Operators

```bash
[ -f file ] && echo "Exists"
[ -f file ] || echo "Missing"
! [ -f file ]
```

---

## Case Statement

```bash
case $1 in
    start) echo "Starting";;
    stop)  echo "Stopping";;
    *)     echo "Invalid option";;
esac
```

---

# 3️⃣ Loops

## For Loop (List)

```bash
for i in 1 2 3; do
    echo $i
done
```

---

## For Loop (C-style)

```bash
for ((i=1; i<=5; i++)); do
    echo $i
done
```

---

## While Loop

```bash
i=1
while [ $i -le 5 ]; do
    echo $i
    ((i++))
done
```

---

## Until Loop

```bash
i=1
until [ $i -gt 5 ]; do
    echo $i
    ((i++))
done
```

---

## Break & Continue

```bash
break
continue
```

---

## Loop Over Files

```bash
for file in *.log; do
    echo $file
done
```

---

## Loop Over Command Output

```bash
ps aux | while read line; do
    echo "$line"
done
```

---

# 4️⃣ Functions

## Define Function

```bash
greet() {
    echo "Hello"
}
```

---

## Call Function

```bash
greet
```

---

## Function Arguments

```bash
add() {
    echo $(($1 + $2))
}
add 5 3
```

---

## Return vs Echo

```bash
return 1   # exit code
echo "value"  # output
```

---

## Local Variables

```bash
myfunc() {
    local VAR="local"
}
```

---

# 5️⃣ Text Processing Commands

## Grep

```bash
grep "error" file
grep -i "error" file
grep -r "error" .
grep -c "error" file
grep -n "error" file
grep -v "info" file
grep -E "ERROR|FAIL" file
```

---

## Awk

```bash
awk '{print $1}' file
awk -F: '{print $1}' /etc/passwd
awk '/ERROR/ {print $2}' file
awk 'BEGIN {print "Start"} {print $1} END {print "End"}' file
```

---

## Sed

```bash
sed 's/old/new/g' file
sed -i 's/foo/bar/g' file
sed '/pattern/d' file
```

---

## Cut

```bash
cut -d: -f1 /etc/passwd
cut -c1-5 file
```

---

## Sort

```bash
sort file
sort -n file
sort -r file
sort -u file
```

---

## Uniq

```bash
uniq file
uniq -c file
```

---

## Tr

```bash
tr 'a-z' 'A-Z'
tr -d '\n'
```

---

## Wc

```bash
wc -l file
wc -w file
wc -c file
```

---

## Head / Tail

```bash
head -n 10 file
tail -n 10 file
tail -f logfile
```

---

# 6️⃣ Useful One-Liners

### Delete files older than 7 days

```bash
find /var/log -name "*.log" -mtime +7 -delete
```

### Count lines in all log files

```bash
wc -l *.log
```

### Replace text in multiple files

```bash
sed -i 's/localhost/127.0.0.1/g' *.conf
```

### Check if service is running

```bash
systemctl is-active nginx
```

### Disk usage alert

```bash
df -h | awk '$5+0 > 80 {print $0}'
```

### Real-time error monitoring

```bash
tail -f app.log | grep --line-buffered ERROR
```

---

# 7️⃣ Error Handling & Debugging

## Exit Codes

```bash
exit 0
exit 1
echo $?
```

---

## Strict Mode

```bash
set -e          # exit on error
set -u          # unset variable error
set -o pipefail # catch pipe errors
set -x          # debug mode
```

Best Practice:

```bash
set -euo pipefail
```

---

## Trap

```bash
cleanup() {
    echo "Cleaning up..."
}
trap cleanup EXIT
```

---

# 🧠 What I Learned

1. Shell scripting is powerful when combining small Linux tools.
2. Error handling (`set -euo pipefail`) is critical for production scripts.
3. Text processing commands (`grep`, `awk`, `sed`) are core DevOps skills.

---
# 📅 Day 16 – Shell Scripting Basics

## 🎯 Objective

Learn:

* Shebang (`#!/bin/bash`)
* Variables
* User input with `read`
* If-else conditions
* Basic automation logic

---

# 🟢 Task 1 – Your First Script

## 📄 `hello.sh`

```bash
#!/bin/bash

echo "Hello, DevOps!"
```

## Make it Executable & Run

```bash
chmod +x hello.sh
./hello.sh
```

### ✅ Output

```
Hello, DevOps!
```

---

## ❓ What Happens If You Remove the Shebang?

If you run:

```bash
./hello.sh
```

Without:

```bash
#!/bin/bash
```

You may get:

* Error (if default shell differs)
* It may run with `/bin/sh` instead of `/bin/bash`

💡 Shebang tells the system which interpreter to use.

---

# 🟡 Task 2 – Variables

## 📄 `variables.sh`

```bash
#!/bin/bash

NAME="Shubham"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"
```

### Run

```bash
chmod +x variables.sh
./variables.sh
```

### ✅ Output

```
Hello, I am Shubham and I am a DevOps Engineer
```

---

## 🔎 Single vs Double Quotes

```bash
echo 'Hello $NAME'
```

Output:

```
Hello $NAME
```

```bash
echo "Hello $NAME"
```

Output:

```
Hello Shubham
```

💡 Double quotes expand variables.
💡 Single quotes treat content literally.

---

# 🔵 Task 3 – User Input with read

## 📄 `greet.sh`

```bash
#!/bin/bash

read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL"
```

### Run

```bash
chmod +x greet.sh
./greet.sh
```

### Example Output

```
Enter your name: Shubham
Enter your favourite tool: Docker
Hello Shubham, your favourite tool is Docker
```

---

# 🟣 Task 4 – If-Else Conditions

---

## 📄 `check_number.sh`

```bash
#!/bin/bash

read -p "Enter a number: " NUM

if [ $NUM -gt 0 ]; then
    echo "Positive number"
elif [ $NUM -lt 0 ]; then
    echo "Negative number"
else
    echo "Zero"
fi
```

---

## 📄 `file_check.sh`

```bash
#!/bin/bash

read -p "Enter filename: " FILE

if [ -f "$FILE" ]; then
    echo "File exists."
else
    echo "File does not exist."
fi
```

---

# 🔴 Task 5 – Combine Everything

## 📄 `server_check.sh`

```bash
#!/bin/bash

SERVICE="sshd"

read -p "Do you want to check the status of $SERVICE? (y/n): " CHOICE

if [ "$CHOICE" = "y" ]; then
    STATUS=$(systemctl is-active $SERVICE)

    if [ "$STATUS" = "active" ]; then
        echo "$SERVICE is running."
    else
        echo "$SERVICE is not running."
    fi
else
    echo "Skipped."
fi
```

---

# 🧠 What I Learned (3 Key Points)

1. Shebang defines which shell executes the script.
2. Variables must not have spaces around `=`.
3. If-else logic allows real automation decisions.

---

# 🚀 Real DevOps Connection

Shell scripting helps you:

* Automate server checks
* Create monitoring scripts
* Write deployment helpers
* Build CI/CD automation steps

This is the foundation before advanced scripting.

---

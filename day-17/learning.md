# 📅 Day 17 – Shell Scripting: Loops, Arguments & Error Handling

## 🎯 Objective

Learn:

* `for` and `while` loops
* Command-line arguments
* Installing packages via script
* Basic error handling

---

# 🟢 Task 1 – For Loop

## 📄 `for_loop.sh`

```bash
#!/bin/bash

for FRUIT in apple banana mango orange grapes
do
    echo "Fruit: $FRUIT"
done
```

### ✅ Output

```
Fruit: apple
Fruit: banana
Fruit: mango
Fruit: orange
Fruit: grapes
```

---

## 📄 `count.sh`

```bash
#!/bin/bash

for i in {1..10}
do
    echo $i
done
```

### ✅ Output

```
1
2
3
...
10
```

---

# 🟡 Task 2 – While Loop

## 📄 `countdown.sh`

```bash
#!/bin/bash

read -p "Enter a number: " NUM

while [ $NUM -ge 0 ]
do
    echo $NUM
    NUM=$((NUM-1))
done

echo "Done!"
```

### ✅ Example Output

```
5
4
3
2
1
0
Done!
```

---

# 🔵 Task 3 – Command-Line Arguments

---

## 📄 `greet.sh`

```bash
#!/bin/bash

if [ -z "$1" ]; then
    echo "Usage: ./greet.sh <name>"
    exit 1
fi

echo "Hello, $1!"
```

### Example Runs

```bash
./greet.sh Shubham
```

Output:

```
Hello, Shubham!
```

```bash
./greet.sh
```

Output:

```
Usage: ./greet.sh <name>
```

---

## 📄 `args_demo.sh`

```bash
#!/bin/bash

echo "Script name: $0"
echo "Total arguments: $#"
echo "All arguments: $@"
```

### Example Run

```bash
./args_demo.sh one two three
```

Output:

```
Script name: ./args_demo.sh
Total arguments: 3
All arguments: one two three
```

---

# 🟣 Task 4 – Install Packages via Script

## 📄 `install_packages.sh`

```bash
#!/bin/bash

# Check if running as root
if [ "$EUID" -ne 0 ]; then
    echo "Please run as root"
    exit 1
fi

PACKAGES="nginx curl wget"

for PKG in $PACKAGES
do
    if dpkg -s $PKG &> /dev/null; then
        echo "$PKG is already installed."
    else
        echo "Installing $PKG..."
        apt update -y
        apt install -y $PKG
        echo "$PKG installed successfully."
    fi
done
```

### Run

```bash
sudo ./install_packages.sh
```

---

# 🔴 Task 5 – Error Handling

## 📄 `safe_script.sh`

```bash
#!/bin/bash

set -e  # Exit immediately if any command fails

mkdir /tmp/devops-test || echo "Directory already exists"

cd /tmp/devops-test || { echo "Failed to enter directory"; exit 1; }

touch test-file.txt || echo "Failed to create file"

echo "Script completed successfully."
```

---

# 🧠 What I Learned (3 Key Points)

1. Loops help automate repetitive tasks.
2. `$1`, `$@`, `$#` allow flexible script inputs.
3. Error handling (`set -e`, `||`) prevents silent failures.

---

# 🚀 Real DevOps Connection

These concepts help in:

* Writing deployment scripts
* Automating server setup
* Handling CI/CD pipeline scripts
* Creating safe production automation

You’re now moving from beginner to intermediate scripting level.

---

# 🔐 Day 10 – File Permissions & File Operations Challenge

This challenge focused on creating, reading, and securing files using Linux file operations and permission management.

---

## 📁 Files Created

- `devops.txt`
- `notes.txt`
- `script.sh`
- `project/` (directory)

---

## 🧩 Task 1: Create Files

### Commands Used
```bash
touch devops.txt
echo "Linux file permissions are important." > notes.txt
vim script.sh
```

**Content inside `script.sh`:**
```bash
echo "Hello DevOps"
```

### Verification
```bash
ls -l
```

**Observation:**  
All files were created with default permissions (`rw-r--r--` for files).

---

## 🧩 Task 2: Read Files

### Commands Used
```bash
cat notes.txt
vim -R script.sh
head -n 5 /etc/passwd
tail -n 5 /etc/passwd
```

**Observation:**  
- `cat` displayed full file content  
- `vim -R` opened file in read-only mode  
- `head` and `tail` helped inspect system files safely  

---

## 🧩 Task 3: Understand Permissions

### Check Permissions
```bash
ls -l devops.txt notes.txt script.sh
```

### Observed Permissions (Before)
- `devops.txt` → `-rw-r--r--`
- `notes.txt` → `-rw-r--r--`
- `script.sh` → `-rw-r--r--`

### Interpretation
- **Owner:** read & write
- **Group:** read-only
- **Others:** read-only
- No file was executable initially

---

## 🧩 Task 4: Modify Permissions

### 1️⃣ Make Script Executable
```bash
chmod +x script.sh
./script.sh
```

**Result:**  
Output displayed: `Hello DevOps`

---

### 2️⃣ Make `devops.txt` Read-Only
```bash
chmod a-w devops.txt
```

---

### 3️⃣ Set `notes.txt` to 640
```bash
chmod 640 notes.txt
```

---

### 4️⃣ Create Directory with 755
```bash
mkdir project
chmod 755 project
```

---

### Verification
```bash
ls -l
ls -ld project
```

**Observed Permissions (After):**
- `script.sh` → `-rwxr-xr-x`
- `devops.txt` → `-r--r--r--`
- `notes.txt` → `-rw-r-----`
- `project/` → `drwxr-xr-x`

---

## 🧩 Task 5: Test Permissions

### 1️⃣ Write to Read-Only File
```bash
echo "test" >> devops.txt
```
**Error:**  
`Permission denied`

---

### 2️⃣ Execute File Without Execute Permission
```bash
chmod -x script.sh
./script.sh
```
**Error:**  
`Permission denied`

---

## 🛠️ Commands Used (Summary)

- `touch`
- `echo`
- `cat`
- `vim`, `vim -R`
- `head`, `tail`
- `chmod`
- `ls -l`, `ls -ld`
- `mkdir`

---

## 📚 What I Learned

- File permissions control security and execution in Linux.
- Execute (`x`) permission is mandatory to run scripts.
- Numeric (`640`, `755`) and symbolic (`+x`, `-w`) modes are both powerful.
- Always verify permissions after making changes.

---

## ⭐ Key Takeaway

Understanding file permissions prevents security issues and execution failures.  
This is a **core DevOps skill** used daily in production systems.

---

✅ **Day 10 completed successfully!**

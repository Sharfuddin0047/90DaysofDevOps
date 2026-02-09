# 📄 File I/O Practice – Linux Fundamentals

This practice focuses on basic file read/write operations using fundamental Linux commands.

---

## 🎯 Objective
Create a text file and practice writing, appending, and reading its contents using simple and repeatable commands.

---

## 🧾 File Created
**File name:** `notes.txt`

---

## ✅ Commands Executed

### 1️⃣ Create an Empty File
```bash
touch notes.txt
```
**What it did:** Created a blank file.

---

### 2️⃣ Write First Line (Overwrite Mode)
```bash
echo "Linux is the backbone of modern infrastructure." > notes.txt
```
**What it did:** Added the first line and overwrote any existing content.

---

### 3️⃣ Append a Second Line
```bash
echo "File operations are essential for DevOps workflows." >> notes.txt
```
**What it did:** Appended text without deleting previous content.

---

### 4️⃣ Write and Display Using tee
```bash
echo "Practicing daily builds strong command-line skills." | tee -a notes.txt
```
**What it did:** Displayed the text in the terminal and appended it to the file.

---

### 5️⃣ Append More Lines
```bash
echo "Logs and configs are plain text files." >> notes.txt
echo "Quick file access speeds up troubleshooting." >> notes.txt
echo "Automation often relies on editing files." >> notes.txt
echo "Understanding redirection prevents mistakes." >> notes.txt
echo "Small commands save big time." >> notes.txt
```
**What it did:** Expanded the file to multiple lines for reading practice.

---

## 📖 Reading the File

### View Entire File
```bash
cat notes.txt
```
**Observation:** Displayed all lines in the file.

---

### View First 2 Lines
```bash
head -n 2 notes.txt
```
**Observation:** Quickly checked the beginning of the file.

---

### View Last 2 Lines
```bash
tail -n 2 notes.txt
```
**Observation:** Verified recently appended content.

---

## 📌 Quick Learnings

- `>` overwrites a file, while `>>` safely appends.
- `tee` is useful when you want to write and verify output instantly.
- `cat`, `head`, and `tail` help inspect files efficiently.
- Strong file handling skills improve debugging and automation speed.

---

✅ **Key Takeaway:**  
Almost everything in Linux is a text file — mastering file operations is a foundational DevOps skill.

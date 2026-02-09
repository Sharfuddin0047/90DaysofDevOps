# 👤 Day 09 – Linux User & Group Management Challenge

This challenge focused on hands-on practice with Linux users, groups, and permissions — a critical skill for secure system administration and DevOps workflows.

---

## ✅ Users & Groups Created

### 👥 Users
- `tokyo`
- `berlin`
- `professor`
- `nairobi`

### 👥 Groups
- `developers`
- `admins`
- `project-team`

---

## 🧩 Task 1: Create Users

### Commands Used
```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor
```

### Verification
```bash
cat /etc/passwd | grep -E "tokyo|berlin|professor"
ls -l /home
```

**Observation:**  
Home directories were created successfully under `/home`.

---

## 🧩 Task 2: Create Groups

### Commands Used
```bash
sudo groupadd developers
sudo groupadd admins
```

### Verification
```bash
cat /etc/group | grep -E "developers|admins"
```

---

## 🧩 Task 3: Assign Users to Groups

### Group Assignments
- `tokyo` → developers  
- `berlin` → developers, admins  
- `professor` → admins  

### Commands Used
```bash
sudo usermod -aG developers tokyo
sudo usermod -aG developers,admins berlin
sudo usermod -aG admins professor
```

### Verification
```bash
groups tokyo
groups berlin
groups professor
```

---

## 🧩 Task 4: Shared Directory for Developers

### Create Directory & Set Permissions
```bash
sudo mkdir /opt/dev-project
sudo chgrp developers /opt/dev-project
sudo chmod 775 /opt/dev-project
```

### Verification
```bash
ls -ld /opt/dev-project
```

### Test File Creation
```bash
sudo -u tokyo touch /opt/dev-project/tokyo-file.txt
sudo -u berlin touch /opt/dev-project/berlin-file.txt
ls -l /opt/dev-project
```

**Observation:**  
Both users successfully created files, confirming correct group permissions.

---

## 🧩 Task 5: Team Workspace Setup

### Create User & Group
```bash
sudo useradd -m nairobi
sudo passwd nairobi

sudo groupadd project-team
```

### Add Users to Group
```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

### Create Shared Directory
```bash
sudo mkdir /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace
```

### Verification & Test
```bash
groups nairobi
ls -ld /opt/team-workspace
sudo -u nairobi touch /opt/team-workspace/nairobi-test.txt
ls -l /opt/team-workspace
```

**Observation:**  
User `nairobi` successfully created files in the shared workspace.

---

## 🛠️ Commands Used (Summary)

- `useradd`, `passwd`
- `groupadd`
- `usermod -aG`
- `groups`
- `mkdir`, `chgrp`, `chmod`
- `ls -l`, `ls -ld`
- `sudo -u`

---

## 📚 What I Learned

- Linux users and groups control access and collaboration.
- Group permissions (`775`) are essential for shared team directories.
- Always verify users, groups, and permissions after changes.
- `sudo -u` is very useful for testing access without switching users.

---

## ⭐ Key Takeaway

User and group management is foundational for security, teamwork, and real-world DevOps environments.  
Correct permissions prevent access issues and reduce operational risk.

---
✅ **Day 09 completed successfully!**

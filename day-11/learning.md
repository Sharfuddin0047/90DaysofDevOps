# Day 11 – File Ownership Challenge (chown & chgrp)

## Task
Master file and directory ownership in Linux.

- Understand file ownership (user and group)
- Change file owner using `chown`
- Change file group using `chgrp`
- Apply ownership changes recursively

---

## Expected Output
- A markdown file: `day-11-file-ownership.md`
- Screenshots showing ownership changes

---

## Challenge Tasks

### Task 1: Understanding Ownership (10 minutes)

Run:

```bash
ls -l
```

Identify the **owner** and **group** columns.

**Format:**
```
-rw-r--r-- 1 owner group size date filename
```

👉 **Document:** What is the difference between owner and group?

---

### Task 2: Basic chown Operations (20 minutes)

Create a file:

```bash
touch devops-file.txt
```

Check current owner:

```bash
ls -l devops-file.txt
```

Change owner:

```bash
sudo chown tokyo devops-file.txt
sudo chown berlin devops-file.txt
```

Verify:

```bash
ls -l devops-file.txt
```

---

### Task 3: Basic chgrp Operations (15 minutes)

Create file:

```bash
touch team-notes.txt
```

Check group:

```bash
ls -l team-notes.txt
```

Create group:

```bash
sudo groupadd heist-team
```

Change file group:

```bash
sudo chgrp heist-team team-notes.txt
```

Verify:

```bash
ls -l team-notes.txt
```

---

### Task 4: Combined Owner & Group Change (15 minutes)

Create file:

```bash
touch project-config.yaml
```

Change owner AND group:

```bash
sudo chown professor:heist-team project-config.yaml
```

Create directory:

```bash
mkdir app-logs
sudo chown berlin:heist-team app-logs
```

---

### Task 5: Recursive Ownership (20 minutes)

Create directory structure:

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

Create group:

```bash
sudo groupadd planners
```

Change ownership recursively:

```bash
sudo chown -R professor:planners heist-project/
```

Verify:

```bash
ls -lR heist-project/
```

---

### Task 6: Practice Challenge (20 minutes)

Create users (if not already created):

```bash
sudo useradd tokyo
sudo useradd berlin
sudo useradd nairobi
```

Create groups:

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

Create directory and files:

```bash
mkdir bank-heist
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

Set ownership:

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

Verify:

```bash
ls -l bank-heist/
```

---

## Key Commands Reference

```bash
# View ownership
ls -l filename

# Change owner only
sudo chown newowner filename

# Change group only
sudo chgrp newgroup filename

# Change both owner and group
sudo chown owner:group filename

# Recursive change
sudo chown -R owner:group directory/

# Change only group with chown
sudo chown :groupname filename
```

---

## Documentation Template

```markdown
# Day 11 Challenge

## Files & Directories Created
- [List all files and directories]

## Ownership Changes
- devops-file.txt: user:user → tokyo:heist-team

## Commands Used
- [List your commands]

## What I Learned
- Ownership controls access to files
- `chown` changes file owner
- Recursive ownership is critical for project directories
```

---

## Troubleshooting

**Permission denied?**  
Use `sudo` for chown/chgrp operations.

**Group doesn't exist?**
```bash
sudo groupadd groupname
```

**User doesn't exist?**
```bash
sudo useradd username
```

---

## Why This Matters for DevOps

Proper file ownership is essential for:

- Application deployments  
- Shared team directories  
- Container file permissions  
- CI/CD pipeline artifacts  
- Log file management  

---

✅ **Day 11 completed successfully!**

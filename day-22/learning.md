Perfect 🔥
This is where real DevOps starts.

Below is your **complete Day 22 reference solution** — structured so you can directly create:

* `git-commands.md`
* `day-22-notes.md`
* Clean commit history

---

# ✅ Step-By-Step Execution Guide

---

# 🔹 Task 1 – Install & Configure Git

### 1️⃣ Verify Installation

```bash
git --version
```

If installed, you’ll see something like:

```
git version 2.43.0
```

---

### 2️⃣ Set Your Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

### 3️⃣ Verify Configuration

```bash
git config --list
```

Or:

```bash
git config user.name
git config user.email
```

---

# 🔹 Task 2 – Create Your First Repository

```bash
mkdir devops-git-practice
cd devops-git-practice
git init
```

You’ll see:

```
Initialized empty Git repository in .../.git/
```

---

### Check Status

```bash
git status
```

Git tells you:

* You’re on branch `main`
* No commits yet
* Nothing to commit

---

### Explore `.git/`

```bash
ls -la .git
```

You’ll see:

* `HEAD`
* `config`
* `objects/`
* `refs/`
* `hooks/`

👉 This folder is the **entire Git database**.

If you delete `.git/` → the folder is no longer a Git repo.

---

# 📄 Create `git-commands.md`

Here is your starter file:

---

# 📘 git-commands.md

# Git Commands Reference

---

## 🔧 Setup & Config

### `git --version`

Shows installed Git version.

```bash
git --version
```

### `git config --global user.name`

Sets your Git username.

```bash
git config --global user.name "DevOps Learner"
```

### `git config --global user.email`

Sets your Git email.

```bash
git config --global user.email "devops@email.com"
```

---

## 🔁 Basic Workflow

### `git init`

Initializes a new Git repository.

```bash
git init
```

### `git status`

Shows working directory and staging area state.

```bash
git status
```

### `git add`

Stages changes.

```bash
git add file.txt
git add .
```

### `git commit`

Creates a snapshot of staged changes.

```bash
git commit -m "Initial commit"
```

---

## 👀 Viewing Changes

### `git log`

Shows commit history.

```bash
git log
```

### `git log --oneline`

Compact commit history.

```bash
git log --oneline
```

### `git diff`

Shows unstaged changes.

```bash
git diff
```

### `git diff --staged`

Shows staged changes.

```bash
git diff --staged
```

---

# 🔹 Task 4 – Stage & Commit

```bash
git add git-commands.md
git status
git commit -m "Add initial git commands reference"
```

---

# 🔹 Task 5 – Build Commit History

Now repeat:

### ✏ Edit File

Add new commands:

```markdown
### git branch
Lists branches.
```

Then:

```bash
git diff
git add git-commands.md
git commit -m "Add branch command documentation"
```

Repeat again:

```bash
git commit -m "Add git diff examples"
git commit -m "Add viewing history section"
```

You should now have **at least 3–4 commits**.

---

### View Compact History

```bash
git log --oneline
```

Example output:

```
a1c9d2e Add viewing history section
f8b3a11 Add git diff examples
d3f8c7a Add branch command documentation
c2a9e55 Add initial git commands reference
```

---

# 📄 Create `day-22-notes.md`

Here is your clean answer file:

---

# 📝 Day 22 – Git Notes

## 1️⃣ Difference between `git add` and `git commit`

* `git add` moves changes to the staging area.
* `git commit` saves staged changes permanently in the repository.

---

## 2️⃣ What is the Staging Area?

The staging area is a temporary area where you prepare changes before committing.
It allows selective commits instead of committing everything at once.

---

## 3️⃣ What does `git log` show?

* Commit hash
* Author
* Date
* Commit message

It shows the project history.

---

## 4️⃣ What is the `.git/` folder?

It contains:

* Commit history
* Branch references
* Configuration
* Object database

If you delete it, the project is no longer a Git repository.

---

## 5️⃣ Working Directory vs Staging Area vs Repository

| Area              | Meaning                    |
| ----------------- | -------------------------- |
| Working Directory | Where you edit files       |
| Staging Area      | Where changes are prepared |
| Repository        | Permanent commit history   |

Workflow:

```
Working Directory → Staging Area → Repository
```

---

# 🎯 What You Should Have Now

✅ Local Git repo
✅ Multiple commits
✅ Clean commit messages
✅ git-commands.md
✅ day-22-notes.md
✅ Screenshot of `git log --oneline`

---

# 🔥 Pro DevOps Advice

From today onward:

* Make **small commits**
* Write **clear messages**
* Never commit junk
* Treat Git history like production history

Good commit message format:

```
Add: branch command documentation
Fix: typo in git diff section
Update: improve workflow explanation
```
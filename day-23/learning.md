# 📄 day-23-notes.md

# 🌿 Day 23 – Git Branching & Working with GitHub

---

# 🧠 Task 1 – Understanding Branches

## 1️⃣ What is a branch in Git?

A branch is a movable pointer to a commit.
It allows you to work on changes independently without affecting other branches.

---

## 2️⃣ Why use branches instead of committing everything to `main`?

* Keeps `main` stable
* Allows parallel development
* Enables safe experimentation
* Supports team collaboration

---

## 3️⃣ What is `HEAD` in Git?

`HEAD` is a pointer to the current branch you are on.
It tells Git which commit you’re currently working from.

Example:

```
HEAD → main → latest commit
```

---

## 4️⃣ What happens to files when switching branches?

* Git updates your working directory
* Files change to match the branch’s latest commit
* Commits from other branches disappear (but are not deleted)

---

# 🌿 Task 2 – Branching Commands

## 1️⃣ List branches

```bash
git branch
```

---

## 2️⃣ Create branch

```bash
git branch feature-1
```

---

## 3️⃣ Switch to branch

```bash
git switch feature-1
```

OR older method:

```bash
git checkout feature-1
```

---

## 4️⃣ Create & switch in one command

```bash
git switch -c feature-2
```

Old way:

```bash
git checkout -b feature-2
```

---

## 5️⃣ Difference: `switch` vs `checkout`

| Command        | Purpose                             |
| -------------- | ----------------------------------- |
| `git switch`   | Only switches branches              |
| `git checkout` | Switches branches OR restores files |

👉 `switch` is safer and clearer.

---

## 6️⃣ Make commit on feature-1

```bash
git switch feature-1
echo "Feature 1 update" >> git-commands.md
git add .
git commit -m "Add feature-1 update"
```

---

## 7️⃣ Switch back to main

```bash
git switch main
git log --oneline
```

You’ll see that `feature-1` commit is NOT present.

---

## 8️⃣ Delete branch

```bash
git branch -d feature-2
```

Force delete:

```bash
git branch -D feature-2
```

---

# 🌍 Task 3 – Push to GitHub

## 1️⃣ Add remote

```bash
git remote add origin https://github.com/yourusername/devops-git-practice.git
```

Check:

```bash
git remote -v
```

---

## 2️⃣ Push main branch

```bash
git push -u origin main
```

`-u` sets upstream tracking.

---

## 3️⃣ Push feature branch

```bash
git push -u origin feature-1
```

Both branches should now be visible on GitHub.

---

## 4️⃣ Difference between `origin` and `upstream`

| Term       | Meaning                             |
| ---------- | ----------------------------------- |
| `origin`   | Default name of YOUR remote repo    |
| `upstream` | Original repository you forked from |

Example:

```
origin → your fork
upstream → original project
```

---

# 🔄 Task 4 – Fetch vs Pull

After editing a file directly on GitHub:

```bash
git pull origin main
```

---

## Difference Between Fetch and Pull

| Command     | What it does                         |
| ----------- | ------------------------------------ |
| `git fetch` | Downloads changes but does NOT merge |
| `git pull`  | Fetch + merge automatically          |

Safe workflow:

```bash
git fetch
git log origin/main
git merge origin/main
```

---

# 🍴 Task 5 – Clone vs Fork

## Clone

```bash
git clone https://github.com/user/repo.git
```

Creates a local copy.

---

## Fork

* Fork is a GitHub feature.
* Creates a copy under your GitHub account.
* Then you clone your fork.

---

## Difference Between Clone & Fork

| Clone                | Fork                  |
| -------------------- | --------------------- |
| Local copy           | GitHub copy           |
| No ownership change  | You own the fork      |
| Used for downloading | Used for contributing |

---

## When to Use?

* Clone → Personal learning / quick use
* Fork → Contributing to open-source

---

## Keep Fork in Sync

Add upstream:

```bash
git remote add upstream https://github.com/original/repo.git
git fetch upstream
git merge upstream/main
```

---

# 📘 Update `git-commands.md`

Add this new section:

---

## 🌿 Branching

### `git branch`

List branches.

```bash
git branch
```

### `git branch <name>`

Create branch.

```bash
git branch feature-1
```

### `git switch <branch>`

Switch branch.

```bash
git switch main
```

### `git switch -c <branch>`

Create and switch.

```bash
git switch -c feature-2
```

### `git branch -d <branch>`

Delete branch.

```bash
git branch -d feature-2
```

---

## 🌍 Remote Commands

### `git remote -v`

List remotes.

### `git remote add origin <url>`

Connect to GitHub.

### `git push -u origin main`

Push branch and set upstream.

### `git fetch`

Download remote changes.

### `git pull`

Fetch + merge.

---

# 🎯 What Your `git log --oneline` Should Look Like

Example:

```
f21ac9e Add remote commands documentation
b91de12 Add branching section
c11ab32 Add feature-1 update
a8de112 Add initial git commands
```

Take screenshot for submission.

---

# 🔥 What You Just Learned (Important)

* Branches are just pointers
* Switching branches changes your working directory
* GitHub remotes connect local to cloud
* Fetch is safe, pull is automatic
* Forking is for contribution

---

# 🚀 DevOps Reality

In real DevOps:

* No one commits directly to `main`
* Every change goes through feature branch
* Then Pull Request
* Then Review
* Then Merge

Tomorrow you’re ready for:

* 🔀 Merging
* ⚔ Merge conflicts
* 🔁 Rebase
* 🧠 Git internals

---

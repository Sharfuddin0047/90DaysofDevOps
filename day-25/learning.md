# 📄 day-25-notes.md

# 🚨 Day 25 – Git Reset vs Revert & Branching Strategies

---

# 🔁 Task 1 – Git Reset

## 🔹 After 3 commits (A → B → C)

```
A --- B --- C (HEAD)
```

---

## 1️⃣ `git reset --soft HEAD~1`

```
git reset --soft HEAD~1
```

Result:

```
A --- B (HEAD)
```

* Commit C is removed from history
* Changes from C are still in **staging area**

---

## 2️⃣ `git reset --mixed HEAD~1` (default)

```
git reset --mixed HEAD~1
```

Result:

```
A --- B (HEAD)
```

* Commit C removed
* Changes moved to **working directory**
* Not staged

---

## 3️⃣ `git reset --hard HEAD~1`

```
git reset --hard HEAD~1
```

Result:

```
A --- B (HEAD)
```

* Commit C removed
* Changes permanently deleted
* Working directory cleaned

---

## 🧠 Differences

| Option    | Commit Removed | Changes Kept | Where?            |
| --------- | -------------- | ------------ | ----------------- |
| `--soft`  | ✅              | ✅            | Staging           |
| `--mixed` | ✅              | ✅            | Working directory |
| `--hard`  | ✅              | ❌            | Deleted           |

---

## ❗ Which is destructive?

`--hard` is destructive because it deletes commits and working directory changes permanently.

---

## 🛠 When to use?

* `--soft` → Fix last commit message or combine commits
* `--mixed` → Unstage files
* `--hard` → Completely discard local changes

---

## 🚫 Should you reset pushed commits?

No ❌
It rewrites history and breaks collaborators' repositories.

---

# 🔄 Task 2 – Git Revert

After 3 commits:

```
X --- Y --- Z
```

Run:

```
git revert Y
```

Result:

```
X --- Y --- Z --- Y'
```

* Git creates a NEW commit that undoes Y
* Y still exists in history

---

## 🧠 Answers

### Difference between reset and revert?

| Reset                | Revert             |
| -------------------- | ------------------ |
| Moves branch pointer | Creates new commit |
| Rewrites history     | Preserves history  |

---

### Why is revert safer?

Because it does not delete commits — it adds a reversal commit.

---

### When to use?

* Reset → Local undo before push
* Revert → Undo changes in shared/public branch

---

# 📊 Task 3 – Reset vs Revert Comparison

|                              | `git reset`          | `git revert`                     |
| ---------------------------- | -------------------- | -------------------------------- |
| What it does                 | Moves branch pointer | Creates new commit to undo       |
| Removes commit from history? | Yes                  | No                               |
| Safe for shared branches?    | No                   | Yes                              |
| When to use                  | Local cleanup        | Undo in production/shared branch |

---

# 🌿 Task 4 – Branching Strategies

---

# 1️⃣ GitFlow

### Structure

```
main (production)
develop (integration)
feature/*
release/*
hotfix/*
```

### Flow

* Feature → develop
* Release → main
* Hotfix → main + develop

### Used For:

Large teams, scheduled releases.

### Pros

* Structured
* Clear release process

### Cons

* Complex
* Heavy process overhead

---

# 2️⃣ GitHub Flow

### Structure

```
main
 ├── feature-1
 ├── feature-2
```

### Flow

* Create branch
* Open Pull Request
* Merge to main

### Used For:

Startups, SaaS, continuous deployment.

### Pros

* Simple
* Fast
* CI/CD friendly

### Cons

* Not ideal for complex release cycles

---

# 3️⃣ Trunk-Based Development

### Structure

```
main (trunk)
short-lived branches
```

Everyone merges to `main` frequently.

### Used For:

High-velocity teams (Google-style).

### Pros

* Very fast integration
* Avoids long-lived branches

### Cons

* Requires strong CI and discipline

---

# 🧠 Answers

### Startup shipping fast?

✅ GitHub Flow

---

### Large team with scheduled releases?

✅ GitFlow

---

### Example Open Source Strategy

For example:

* Many modern projects (like React) use a GitHub Flow style.
* Large systems like Kubernetes use structured release branches.

---

# 📘 Update `git-commands.md`

Add:

---

# 🔁 Reset & Revert

### `git reset --soft HEAD~1`

Undo last commit, keep changes staged.

### `git reset --mixed HEAD~1`

Undo commit, keep changes unstaged.

### `git reset --hard HEAD~1`

Undo commit and delete changes.

### `git revert <hash>`

Create commit that undoes another commit.

---

# 🔎 Safety Tools

### `git reflog`

Shows complete reference log, even after reset.

---

# 🧠 Most Important Concept Today

* Reset rewrites history.
* Revert preserves history.
* Never rewrite shared history.
* Always protect `main`.

---

# 🚀 What You Now Understand

* How to undo safely
* History rewriting risks
* Professional branching models
* Real-world Git workflows

---

# 🔥 DevOps Golden Rule

If code is pushed and shared:

👉 Use **revert**
👉 Avoid **reset --hard**
👉 Never force push to main

---
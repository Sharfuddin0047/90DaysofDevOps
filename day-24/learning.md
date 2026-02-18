# 📄 day-24-notes.md

# 🚀 Day 24 – Advanced Git: Merge, Rebase, Stash & Cherry Pick

---

# 🔀 Task 1 – Git Merge

## 🌿 Fast-Forward Merge

If `main` has not moved ahead since branch creation:

```
main: A---B
feature:     C---D
```

After merge:

```
A---B---C---D
```

No merge commit created.

### Definition:

A fast-forward merge happens when Git simply moves the branch pointer forward.

---

## 🔁 Merge Commit

If both branches have new commits:

```
main:    A---B---E
feature:      C---D
```

After merge:

```
A---B---E
      \     \
       C---D---M
```

Git creates a merge commit (`M`).

---

## ❗ What is a Merge Conflict?

Occurs when:

* Same file
* Same line
* Modified differently in two branches

Git shows:

```
<<<<<<< HEAD
Your changes
=======
Other branch changes
>>>>>>> feature
```

You must manually resolve it.

---

## 📝 Answers

### What is a fast-forward merge?

When Git moves the branch pointer forward without creating a new commit.

### When does Git create a merge commit?

When both branches have diverged (both have new commits).

### What is a merge conflict?

When Git cannot automatically combine changes from two branches.

---

# 🔄 Task 2 – Git Rebase

## What Rebase Does

Instead of merging:

Rebase takes your branch commits and replays them on top of another branch.

Before rebase:

```
main:    A---B---E
feature:      C---D
```

After rebase:

```
A---B---E---C'---D'
```

Commits are rewritten (new hashes).

---

## Compare History

### Merge History

Has branch structure (non-linear).

### Rebase History

Looks linear and clean.

Use:

```bash
git log --oneline --graph --all
```

---

## 📝 Answers

### What does rebase do?

It rewrites commits and applies them on top of another base branch.

### How is history different?

* Merge → branch graph preserved
* Rebase → linear history

### Why never rebase pushed commits?

Because it rewrites commit history and breaks other collaborators’ repositories.

### When to use?

* Rebase → Clean up local branch before merging
* Merge → Preserve history in shared branches

---

# 🧹 Task 3 – Squash Merge

## Squash Merge

```bash
git merge --squash feature-profile
```

Result:

* All feature commits combined into ONE commit.
* History stays clean.

---

## Compare

| Merge Type    | Result            |
| ------------- | ----------------- |
| Regular Merge | Keeps all commits |
| Squash Merge  | Combines commits  |

---

## 📝 Answers

### What does squash do?

Combines multiple commits into one.

### When to use?

When feature branch has many small commits (fix, typo, etc.).

### Trade-off?

You lose detailed commit history from that branch.

---

# 📦 Task 4 – Git Stash

## Basic Stash

```bash
git stash
```

Saves uncommitted changes.

---

## Stash with Message

```bash
git stash push -m "WIP login feature"
```

---

## List Stashes

```bash
git stash list
```

---

## Apply Stash

```bash
git stash apply
```

Apply specific stash:

```bash
git stash apply stash@{1}
```

---

## Pop Stash

```bash
git stash pop
```

---

## 📝 Answers

### Difference: pop vs apply

| Command | Behavior                  |
| ------- | ------------------------- |
| apply   | Keeps stash               |
| pop     | Applies and deletes stash |

---

### Real-world usage?

When:

* Mid-feature
* Urgent bug fix needed
* Need to switch branches safely

---

# 🍒 Task 5 – Cherry Pick

## Cherry Pick Example

```bash
git log --oneline
git cherry-pick <commit-hash>
```

Applies ONE specific commit from another branch.

---

## 📝 Answers

### What does cherry-pick do?

Applies a specific commit from another branch onto current branch.

### When to use?

* Hotfix needed on production
* Apply one bug fix without merging full branch

### What can go wrong?

* Duplicate commits
* Conflicts
* Messy history

---

# 📘 Update `git-commands.md`

Add this section:

---

# 🔀 Merge & Rebase

### `git merge <branch>`

Merge branch into current branch.

### `git merge --squash <branch>`

Combine all commits into one.

### `git rebase <branch>`

Replay commits on top of another branch.

### `git log --oneline --graph --all`

Visualize branch history.

---

# 📦 Stash

### `git stash`

Save uncommitted changes.

### `git stash push -m "msg"`

Stash with message.

### `git stash list`

List stashes.

### `git stash apply`

Apply stash without removing.

### `git stash pop`

Apply and remove stash.

---

# 🍒 Cherry Pick

### `git cherry-pick <hash>`

Apply specific commit.

---

# 🧠 Big Concept Summary

| Feature     | Use Case                 |
| ----------- | ------------------------ |
| Merge       | Combine branches         |
| Rebase      | Clean up history         |
| Squash      | Simplify feature commits |
| Stash       | Temporary save work      |
| Cherry-pick | Apply specific commit    |

---

# 🔥 Most Important DevOps Rule

Never:

* Rebase shared branches
* Force push to main
* Rewrite public history

---

# 🚀 You Now Understand:

* Linear vs non-linear history
* Commit rewriting
* Context switching safely
* Selective commit application

This is intermediate-to-advanced Git.

---
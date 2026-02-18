# 📘 day-26-notes.md

# Day 26 – GitHub CLI (gh)

---

## ✅ Task 1: Install & Authenticate

### Install (Linux example)

```bash
sudo apt install gh
```

### Authenticate

```bash
gh auth login
```

Follow prompts:

* GitHub.com
* HTTPS
* Login with browser (recommended)

### Verify Login

```bash
gh auth status
```

### 🔎 Authentication Methods Supported

* Browser-based OAuth (recommended)
* Personal Access Token (PAT)
* SSH authentication
* GitHub Enterprise authentication

---

## ✅ Task 2: Working with Repositories

### Create New Repo

```bash
gh repo create devops-gh-test --public --source=. --remote=origin --push
```

Or create empty repo with README:

```bash
gh repo create devops-gh-test --public --add-readme
```

### Clone Repo

```bash
gh repo clone owner/repo-name
```

### View Repo Details

```bash
gh repo view
```

### List All Your Repos

```bash
gh repo list
```

### Open Repo in Browser

```bash
gh repo view --web
```

### Delete Repo (Careful!)

```bash
gh repo delete devops-gh-test
```

---

## ✅ Task 3: Issues

### Create Issue

```bash
gh issue create --title "Test Issue" --body "This is created from CLI" --label bug
```

### List Open Issues

```bash
gh issue list
```

### View Specific Issue

```bash
gh issue view 1
```

### Close Issue

```bash
gh issue close 1
```

### 💡 How `gh issue` Helps in Automation?

* Auto-create issues on deployment failure
* Open incident tickets from CI/CD
* Generate issues from monitoring alerts
* Bulk manage issues using scripts

Example:

```bash
gh issue create --title "Build Failed" --body "Pipeline failed on prod"
```

---

## ✅ Task 4: Pull Requests

### Create Branch & Push

```bash
git checkout -b feature-branch
echo "change" >> test.txt
git add .
git commit -m "Added test file"
git push origin feature-branch
```

### Create PR from Terminal

```bash
gh pr create --fill
```

### List PRs

```bash
gh pr list
```

### View PR Details

```bash
gh pr view 1
```

### Merge PR

```bash
gh pr merge 1 --merge
```

### 🔎 Merge Methods Supported

* `--merge` (Create merge commit)
* `--squash` (Squash commits)
* `--rebase` (Rebase and merge)

### 👀 Review Someone Else’s PR

```bash
gh pr checkout 12
gh pr review 12 --approve
gh pr review 12 --comment -b "Looks good!"
```

---

## ✅ Task 5: GitHub Actions (Preview)

### List Workflow Runs

```bash
gh run list
```

### View Specific Run

```bash
gh run view 123456
```

### Useful in CI/CD?

* Monitor pipeline status from terminal
* Cancel failed runs
* Download logs
* Trigger workflows manually
* Integrate into deployment scripts

Example:

```bash
gh workflow run deploy.yml
```

---

## ✅ Task 6: Useful `gh` Tricks

### `gh api` – Raw API Calls

```bash
gh api repos/:owner/:repo
```

### `gh gist`

```bash
gh gist create file.txt
```

### `gh release`

```bash
gh release create v1.0.0
```

### `gh alias`

```bash
gh alias set prc "pr create --fill"
```

### `gh search repos`

```bash
gh search repos devops
```

---

# 📊 Real DevOps Use Cases

* Automating PR creation after CI success
* Creating releases automatically after tagging
* Triggering workflows via scripts
* Managing issues from monitoring alerts
* Bulk repository management

---

# 🎯 Final Thoughts

The GitHub CLI removes browser dependency and improves:

* Speed ⚡
* Automation 🤖
* Productivity 📈
* DevOps efficiency 🔥

For DevOps engineers, mastering `gh` is a big step toward automation-first thinking.

---
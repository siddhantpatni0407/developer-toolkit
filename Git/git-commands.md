# 🧰 Git Commands — Complete Guide

This document serves as a comprehensive reference for Git, covering everything from basic setup and everyday use to advanced workflows and optimization tips.

---

## 🔧 Setup & Configuration

| Command | Description |
|--------|-------------|
| `git config --global user.name "Your Name"` | Set your Git username globally. |
| `git config --global user.email "you@example.com"` | Set your Git email globally. |
| `git config --list` | List all active Git configurations. |
| `git config --global core.editor code` | Set default editor (e.g., VS Code). |
| `git config --global alias.st status` | Create a shortcut alias (`git st`). |
| `git config --show-origin` | Show where each config value is set. |

---

## 📁 Repository Initialization

| Command | Description |
|--------|-------------|
| `git init` | Initialize a new Git repository in the current directory. |
| `git clone <repo-url>` | Clone a repository from GitHub or any remote. |

---

## 📄 Basic File Operations

| Command | Description |
|--------|-------------|
| `git status` | Show current changes and untracked files. |
| `git add <file>` | Stage a file for commit. |
| `git add .` | Stage all changes. |
| `git commit -m "message"` | Commit staged changes with a message. |
| `git rm <file>` | Remove file from working directory and stage the deletion. |
| `git mv <old> <new>` | Rename or move a file. |

---

## 🔁 Branching & Merging

| Command | Description |
|--------|-------------|
| `git branch` | List all local branches. |
| `git branch <name>` | Create a new branch. |
| `git checkout <branch>` | Switch to an existing branch. |
| `git checkout -b <name>` | Create and switch to a new branch. |
| `git merge <branch>` | Merge a branch into current branch. |
| `git branch -d <name>` | Delete a local branch. |
| `git switch <branch>` | Alternative to `checkout` (simpler syntax). |
| `git switch -c <name>` | Create and switch in one step (like `checkout -b`). |

---

## ⬆️ Remote Repositories

| Command | Description |
|--------|-------------|
| `git remote -v` | View remote repository URLs. |
| `git remote add origin <url>` | Add a new remote repository. |
| `git push -u origin main` | Push local `main` branch and set upstream. |
| `git fetch` | Get updates from the remote (without merging). |
| `git pull` | Fetch + merge remote changes. |
| `git push` | Push changes to remote. |

---

## 🔍 History & Logs

| Command | Description |
|--------|-------------|
| `git log` | View commit history. |
| `git log --oneline` | Condensed log (one line per commit). |
| `git show <commit>` | Show details of a specific commit. |
| `git diff` | View unstaged changes. |
| `git diff --staged` | View staged changes. |
| `git blame <file>` | Show line-by-line commit history for a file. |

---

## ⏮ Undoing Changes

| Command | Description |
|--------|-------------|
| `git checkout -- <file>` | Discard changes in a file. |
| `git restore <file>` | Restore file to last committed state (modern alternative). |
| `git reset <file>` | Unstage a file. |
| `git reset --hard` | Reset working directory and index to last commit. **⚠️ Irreversible** |
| `git revert <commit>` | Create a new commit that reverses a previous commit. |

---

## 🗂️ Stashing

| Command | Description |
|--------|-------------|
| `git stash` | Temporarily save all local changes. |
| `git stash list` | Show list of stashed changes. |
| `git stash pop` | Reapply the last stash and remove it. |
| `git stash apply` | Reapply the last stash (but keep it). |
| `git stash drop` | Delete the last stash. |

---

## 🧪 Tags

| Command | Description |
|--------|-------------|
| `git tag` | List all tags. |
| `git tag <v1.0>` | Create a lightweight tag. |
| `git tag -a <v1.0> -m "Version 1"` | Create an annotated tag. |
| `git push origin <tag>` | Push a single tag to remote. |
| `git push origin --tags` | Push all local tags. |

---

## ⚒️ Advanced Commands

| Command | Description |
|--------|-------------|
| `git cherry-pick <commit>` | Apply a specific commit to the current branch. |
| `git rebase <branch>` | Reapply commits on top of another base branch. |
| `git reflog` | Show a log of all reference updates (including reset commits). |
| `git clean -fd` | Remove untracked files and directories. **⚠️ Irreversible** |
| `git bisect` | Binary search through commit history to find a bug. |

---

## 🧠 Helpful Aliases

These aliases allow you to run git co, git br, git ci, etc.

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --decorate"
```

## 🛠 Useful Tips

- Use `.gitignore` to exclude files and directories from being tracked by Git.
- Use `git stash` before switching branches if you have uncommitted changes you want to save temporarily.
- Use `git log --graph` to visualize commit history and branch merges.
- Use `git reflog` to recover lost commits or find previous states of your repository.

---

## 🌐 External References

- [Git Official Documentation](https://git-scm.com/doc)
- [Git Cheatsheet (PDF)](https://education.github.com/git-cheat-sheet-education.pdf)
- [Oh My Git! — Interactive Git Learning Game](https://ohmygit.org/)

---

## 📌 Recommended Workflow (Basic)

### 🔽 Clone the repository:

```bash
git clone <url>
cd <repo>
````

### 🌿 Create and switch to a feature branch:

```bash
git checkout -b feature/new-feature
```

### ✏️ Make changes and commit them:

```bash
git add .
git commit -m "Add new feature"
```

### 🚀 Push to remote and create a pull request:

```bash
git push -u origin feature/new-feature
```
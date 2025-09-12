# 🪝 Git Hooks

**Git Hooks** are custom scripts that run automatically at specific points in the Git lifecycle.  
They are useful to **automate workflows, enforce coding standards, and catch issues early**.

---

## ⚖️ Client-Side vs Server-Side Hooks

| Type            | Location      | Examples of Usage                                                       |
| --------------- | ------------- | ----------------------------------------------------------------------- |
| **Client-side** | `.git/hooks/` | Run tests before commit, enforce commit message style, auto-format code |
| **Server-side** | On Git server | Enforce branch naming, reject non-signed commits, enforce CI checks     |

---

## 📂 Hook Types

| 🔑 Hook Name              | ⏱️ Trigger Time                      | 🛠️ Common Use Cases                                     |
| ------------------------- | ------------------------------------ | ------------------------------------------------------- |
| **applypatch-msg**        | On `git am` before applying a patch  | Verify commit message from patch files                  |
| **pre-applypatch**        | Before applying patch                | Run linters or tests                                    |
| **post-applypatch**       | After patch applied                  | Send notifications or run builds                        |
| **pre-commit**            | Before `git commit`                  | Lint, format, run security scans, block secrets         |
| **prepare-commit-msg**    | Before commit message editor opens   | Pre-fill commit template or add JIRA/issue ID           |
| **commit-msg**            | After commit message entered         | Enforce Conventional Commits or validate message format |
| **post-commit**           | After commit is created              | Notify Slack/Discord, update local docs                 |
| **pre-rebase**            | Before rebasing starts               | Prevent rebasing protected branches                     |
| **post-rewrite**          | After commands like `git rebase`     | Re-apply custom formatting or hooks                     |
| **pre-push**              | Before pushing to remote             | Run tests, block push if failing, scan for secrets      |
| **pre-receive** (server)  | Before remote accepts push           | Enforce branch protection (no direct push to main)      |
| **update** (server)       | On push for each branch              | Enforce tag naming, branch naming policies              |
| **post-receive** (server) | After push                           | Trigger CI/CD pipelines, send notifications             |
| **post-checkout**         | After `git checkout`                 | Sync `.env` files, reset configs                        |
| **post-merge**            | After a successful merge             | Run migrations, install dependencies                    |
| **post-rewrite**          | After `git commit --amend` or rebase | Update reflogs, notify tracking systems                 |

---

## ⚡ Example Hooks

### ✅ Pre-commit hook (lint, format, and secrets check)

`.git/hooks/pre-commit`

```bash
#!/bin/sh
echo "🔍 Running pre-commit checks..."
npm run lint || exit 1
npm run format
if git diff --cached | grep -q "API_KEY"; then
  echo "❌ API key found in staged files!"
  exit 1
fi
```

---

### ✅ Commit-msg hook (Conventional Commits)

`.git/hooks/commit-msg`

```bash
#!/bin/sh
commit_msg=$(cat "$1")
pattern="^(feat|fix|docs|style|refactor|test|chore|perf)(\(.+\))?: .{1,72}$"

if ! echo "$commit_msg" | grep -Eq "$pattern"; then
  echo "❌ Commit message must follow Conventional Commits format!"
  echo "Example: feat(auth): add login support"
  exit 1
fi
```

---

### ✅ Pre-push hook (run tests & security scan)

`.git/hooks/pre-push`

```bash
#!/bin/sh
echo "🚀 Running tests before push..."
npm test || exit 1

echo "🔒 Running security scan..."
trivy fs . || exit 1
```

---

### ✅ Post-merge hook (auto-install dependencies)

`.git/hooks/post-merge`

```bash
#!/bin/sh
if [ -f package.json ]; then
  echo "📦 Installing npm dependencies after merge..."
  npm install
fi
```

---

## 🔧 Managing Hooks with Tools

| Tool           | Language/Usage    | Description                                 |
| -------------- | ----------------- | ------------------------------------------- |
| **Husky**      | JavaScript/NodeJS | Easiest way to manage hooks in JS projects  |
| **pre-commit** | Python            | Manages hooks via `.pre-commit-config.yaml` |
| **Lefthook**   | Polyglot          | Fast, language-agnostic Git hook manager    |
| **Overcommit** | Ruby              | Hook manager for Ruby projects              |

---

### ✅ Example: Husky (JS projects)

```sh
npm install husky --save-dev
npx husky install
npx husky add .husky/pre-commit "npm test"
```

### ✅ Example: pre-commit (Python projects)

```sh
pip install pre-commit
pre-commit install
```

`.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: trailing-whitespace
      - id: check-yaml
      - id: check-json
      - id: check-added-large-files
```

---

## 🏆 Best Practices

- Keep hooks **fast** — long-running tasks frustrate developers.
- Use hooks for **blocking critical issues** (tests, security), not for everything.
- Manage hooks with tools like **Husky** or **pre-commit** for portability.
- Ensure hooks run in **CI/CD as well** (not just locally).
- Document hooks in your repo’s `CONTRIBUTING.md`.

---

## 📚 Resources

- [Git Hooks Docs](https://git-scm.com/docs/githooks)
- [Husky](https://typicode.github.io/husky/)
- [Pre-commit](https://pre-commit.com/)
- [Lefthook](https://github.com/evilmartians/lefthook)
- [Overcommit](https://github.com/sds/overcommit)

---

> ⚡ _“Automate checks at commit-time — catch problems before they reach the repo.”_

```

---
```

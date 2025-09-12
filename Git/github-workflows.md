# ⚙️ GitHub Workflows (GitHub Actions)

**GitHub Actions** lets you **automate tasks** directly inside your GitHub repository using workflows.  
These workflows are written in **YAML** and stored under `.github/workflows/`.

They can run on **push, pull request, schedule, or manual triggers**.  
Common use cases: **CI/CD, code quality checks, release automation, and repo maintenance**.

---

## 📂 Workflow Basics

- Workflows live in:

```

.github/workflows/<workflow-name>.yml

```

- Workflows are composed of:
- **Events** → Triggers (push, PR, schedule, manual)
- **Jobs** → Units of execution
- **Steps** → Commands or actions inside jobs
- **Runners** → Machines that execute jobs (e.g., `ubuntu-latest`)

---

## 📑 Workflow Structure

Example:

```yaml
name: CI Pipeline

on:
push:
  branches: [main, develop]
pull_request:
  branches: [main]

jobs:
build:
  runs-on: ubuntu-latest
  steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Set up Node.js
      uses: actions/setup-node@v4
      with:
        node-version: "20"

    - name: Install dependencies
      run: npm install

    - name: Run tests
      run: npm test
```

---

## 🚀 Common Workflow Types

### 🔹 Continuous Integration (CI)

Run tests on every push/PR:

```yaml
name: Node CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: "20" }
      - run: npm ci
      - run: npm test
```

---

### 🔹 Continuous Deployment (CD)

Deploy to production/staging automatically:

```yaml
name: Deploy App
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to server
        run: ./scripts/deploy.sh
```

---

### 🔹 Linting & Formatting

Ensure consistent code style:

```yaml
name: Lint Code
on: [push]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run ESLint
        run: npm run lint
```

---

### 🔹 Release Automation

Create GitHub releases automatically:

```yaml
name: Release
on:
  push:
    tags:
      - "v*.*.*"

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Create Release
        uses: softprops/action-gh-release@v1
        with:
          body: "Automated release notes"
```

---

### 🔹 Scheduled Workflows

Run jobs daily/weekly:

```yaml
name: Daily Cleanup
on:
  schedule:
    - cron: "0 2 * * *" # 2 AM UTC daily

jobs:
  cleanup:
    runs-on: ubuntu-latest
    steps:
      - name: Delete old logs
        run: ./scripts/cleanup.sh
```

---

### 🔹 Documentation / README Updater

Auto-update `README.md` with date or stats:

```yaml
name: Update README
on:
  schedule:
    - cron: "0 */6 * * *" # Every 6 hours

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: ./scripts/update-readme.sh
      - name: Commit changes
        run: |
          git config user.name github-actions
          git config user.email github-actions@github.com
          git commit -am "chore: update README"
          git push
```

---

## 🧰 Useful Official Actions

| Action                      | Purpose                    |
| --------------------------- | -------------------------- |
| `actions/checkout`          | Check out repo code        |
| `actions/setup-node`        | Set up Node.js environment |
| `actions/setup-java`        | Set up Java environment    |
| `actions/setup-python`      | Set up Python environment  |
| `actions/cache`             | Cache dependencies         |
| `actions/upload-artifact`   | Upload build artifacts     |
| `actions/download-artifact` | Download build artifacts   |

---

## 🏆 Best Practices

- Use **matrix builds** to test multiple versions of Node/Python/Java.
- Cache dependencies with `actions/cache` for faster builds.
- Restrict workflows with `paths` or `branches` filters to avoid unnecessary runs.
- Store **secrets in GitHub Secrets** (`${{ secrets.MY_SECRET }}`).
- Use **reusable workflows** (`workflow_call`) for shared CI/CD pipelines.
- Monitor & control workflow costs (minutes are billed in private repos).

---

## 📚 Resources

- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [Awesome Actions (Community List)](https://github.com/sdras/awesome-actions)
- [GitHub Marketplace for Actions](https://github.com/marketplace?type=actions)

---

> ⚡ _“Workflows turn your repository into an automated powerhouse — CI/CD, tests, deployments, and beyond.”_

```

---
```

# 🐙 GitHub Best Practices

This document lists **best practices for using GitHub effectively** in professional and personal projects.  
Following these practices ensures **clean commit history, better collaboration, improved automation, and strong security**.

---

## 📋 Categories Overview

| 📂 Category            | 📄 Description                                         |
| ---------------------- | ------------------------------------------------------ |
| **Repository Setup**   | How to structure & initialize a repository             |
| **Branching**          | Git branching strategies (naming, workflow)            |
| **Commits & PRs**      | Commit messages, pull requests, reviews                |
| **Issues & Labels**    | Tracking work effectively with GitHub Issues           |
| **Security**           | Dependabot, secrets, branch protection, access control |
| **Automation**         | Using GitHub Actions for CI/CD & maintenance           |
| **Documentation**      | README, Wiki, and contributing guidelines              |
| **Collaboration**      | Managing teams, discussions, project boards            |
| **Release Management** | Tags, releases, and versioning best practices          |

---

## 🏗️ Repository Setup

| ✅ Must Have Files                 | 📄 Purpose                                  |
| ---------------------------------- | ------------------------------------------- |
| `README.md`                        | Project overview, setup, usage              |
| `LICENSE`                          | Legal terms for usage                       |
| `.gitignore`                       | Exclude build artifacts, IDE files, OS junk |
| `CONTRIBUTING.md`                  | Guidelines for contributors                 |
| `CODE_OF_CONDUCT.md`               | Community standards                         |
| `.editorconfig`                    | Consistent coding styles across IDEs        |
| `.github/ISSUE_TEMPLATE`           | Standard templates for issues               |
| `.github/pull_request_template.md` | Consistent PR templates                     |

---

## 🌿 Branching Strategy

| 🌿 Branch Type | 📝 Naming Example               | 🎯 Purpose                          |
| -------------- | ------------------------------- | ----------------------------------- |
| **main**       | `main`                          | Production-ready code               |
| **feature**    | `feature/login-auth`            | New features                        |
| **bugfix**     | `bugfix/null-pointer-exception` | Non-critical bug fixes              |
| **hotfix**     | `hotfix/critical-db-issue`      | Urgent fixes in production          |
| **release**    | `release/v2.1.0`                | Pre-release stabilization & testing |

---

## 📝 Commit Messages

### 🔹 Recommended Approaches

| 🏷️ Type                  | ✍️ Format Example                                                             | 📖 Purpose                                     |
| ------------------------ | ----------------------------------------------------------------------------- | ---------------------------------------------- |
| **Conventional Commits** | `feat: add JWT authentication`<br>`fix: resolve null pointer in user service` | Industry standard, semantic versioning support |
| **Prefix by Scope**      | `ui: fix login button alignment`<br>`api: add pagination support`             | Clear ownership of changes by scope            |
| **Imperative Style**     | `Add retry logic for Kafka consumer`                                          | Reads like an instruction                      |
| **Reference Issues**     | `fix: handle timeout error (closes #42)`                                      | Links commits directly to tracked issues       |
| **Atomic Commits**       | One logical change per commit                                                 | Easy to revert/understand history              |

---

### 🔹 Commit Types (Conventional Commits)

| 🔑 Type      | 📖 Purpose                                                           | ✅ Example                                  |
| ------------ | -------------------------------------------------------------------- | ------------------------------------------- |
| **feat**     | Introduces a **new feature**                                         | `feat: add user authentication with JWT`    |
| **fix**      | A **bug fix**                                                        | `fix: resolve null pointer in user service` |
| **docs**     | Documentation changes only                                           | `docs: update API usage in README`          |
| **style**    | Code style/formatting changes (no logic changes, e.g., spaces, lint) | `style: format code using Prettier`         |
| **refactor** | Restructure code without changing behavior                           | `refactor: simplify user service logic`     |
| **test**     | Add or update tests                                                  | `test: add unit tests for order service`    |
| **chore**    | Maintenance tasks (configs, CI/CD, build scripts)                    | `chore: update Gradle build configuration`  |
| **perf**     | Performance improvements                                             | `perf: optimize DB query with index`        |

---

### 🔹 Bad Practices to Avoid

| ❌ Anti-Pattern          | 🚫 Example                    | ✅ Instead Use                                  |
| ------------------------ | ----------------------------- | ----------------------------------------------- |
| Too vague                | `fixed stuff`, `update`       | `fix: resolve timeout in user API`              |
| Mixed changes            | UI + backend changes together | Split into `feat(ui): ...` and `feat(api): ...` |
| No reference to issue/PR | `fixed bug`                   | `fix: handle NPE (closes #101)`                 |

---

## 🔀 Pull Requests (PRs)

| 📌 Best Practice   | ✅ Recommendation                             |
| ------------------ | --------------------------------------------- |
| **Small PRs**      | Keep changes focused for easier review        |
| **PR Templates**   | Use checklists, descriptions, screenshots     |
| **Draft PRs**      | For ongoing/incomplete work                   |
| **Linked Issues**  | Reference issues: `closes #123`               |
| **Code Reviews**   | At least 1–2 approvals before merge           |
| **Merge Strategy** | Prefer **Squash & Merge** for cleaner history |

---

## 🎫 Issues & Labels

| 📌 Practice            | ✅ Recommendation                                                                         |
| ---------------------- | ----------------------------------------------------------------------------------------- |
| **Standard Labels**    | `bug`, `enhancement`, `documentation`, `help wanted`, `good first issue`, `priority-high` |
| **Milestones**         | Use for sprints or releases (`Sprint 5`, `v2.0.0`)                                        |
| **Templates**          | Predefined issue templates improve consistency                                            |
| **Auto-close via PRs** | `fixes #42` or `closes #101`                                                              |

---

## 🔒 Security Best Practices

| 🔒 Area            | ✅ Recommendation                                              |
| ------------------ | -------------------------------------------------------------- |
| **Branch Rules**   | Require PR reviews, status checks, disallow force-push         |
| **Dependencies**   | Enable Dependabot for updates & security alerts                |
| **Secrets**        | Use GitHub Secrets, never commit credentials                   |
| **Access**         | Grant least-privilege access; use teams for role-based control |
| **Token Rotation** | Rotate PATs & deployment keys regularly                        |

---

## ⚡ Automation with GitHub Actions

| ⚙️ Workflow Type       | 🔧 Example Tools / Actions                        |
| ---------------------- | ------------------------------------------------- |
| **CI/CD**              | Build & test on push (Maven, Gradle, npm, pytest) |
| **Linting/Formatting** | ESLint, Prettier, Checkstyle, Black               |
| **Security Scans**     | CodeQL, Snyk, Trivy                               |
| **Release Automation** | Auto-tagging, changelog via Release Drafter       |
| **Maintenance**        | Auto-close stale issues, update README timestamp  |

---

## 📚 Documentation

| 📂 File / Tool  | 📝 Purpose                                    |
| --------------- | --------------------------------------------- |
| **README.md**   | Overview, setup, usage, contribution guide    |
| **Wiki**        | Extended documentation                        |
| **Docs folder** | Technical docs, architecture diagrams         |
| **Badges**      | Build status, coverage, last updated, license |

---

## 🤝 Collaboration & Project Management

| 🧑‍🤝‍🧑 Tool / Practice      | ✅ Recommendation                      |
| ----------------------- | -------------------------------------- |
| **GitHub Discussions**  | Use for Q&A and long-form ideas        |
| **Projects (Kanban)**   | Track issues & PRs in Agile workflows  |
| **Reviewers/Assignees** | Assign PRs & issues for accountability |
| **Branch Cleanup**      | Delete merged branches                 |

---

## 🚀 Release Management

| 📦 Practice             | ✅ Recommendation                          |
| ----------------------- | ------------------------------------------ |
| **Semantic Versioning** | `MAJOR.MINOR.PATCH` → `2.1.3`              |
| **Tags**                | Use annotated tags (`git tag -a v1.0.0`)   |
| **Automated Releases**  | Use Release Drafter, GitHub Actions        |
| **Artifacts**           | Attach binaries, Docker images, JARs, etc. |

---

## 🙋 Contribution Guidelines

| 📌 Practice         | ✅ Recommendation                             |
| ------------------- | --------------------------------------------- |
| **Branching**       | Always create feature branches                |
| **Testing**         | Add unit/integration tests for new features   |
| **Formatting**      | Run linters & formatters before pushing       |
| **Descriptive PRs** | Include context, link issues, add screenshots |
| **Code Reviews**    | Be constructive, suggest improvements         |

---

## 🧑‍💻 Author

**Siddhant Patni**  
[🌐 GitHub](https://github.com/siddhantpatni0407)

---

## 📜 License

This document is part of the [developer-toolkit](../README.md) project.  
Feel free to use, adapt, and share under the [MIT License](../LICENSE).

---

> ⚡ _“A clean repo is a happy repo. Automate what you can, document what you can’t, and secure what you must.”_

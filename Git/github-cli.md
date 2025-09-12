# 🐙 GitHub CLI (`gh`)

The **GitHub CLI** (`gh`) is a powerful tool that lets you manage repositories, issues, pull requests, releases, and workflows **directly from your terminal** — no need to switch to the GitHub web UI for common tasks.

---

## 📦 Installation

### Windows

- **Winget:**
  ```sh
  winget install --id GitHub.cli
  ```

````

* **Scoop:**

  ```sh
  scoop install gh
  ```
* **MSI Installer:**
  [Download MSI](https://github.com/cli/cli/releases)

### macOS

* **Homebrew:**

  ```sh
  brew install gh
  ```

### Linux

* **Debian/Ubuntu (apt):**

  ```sh
  sudo apt update
  sudo apt install gh
  ```
* **RHEL/Fedora (yum/dnf):**

  ```sh
  sudo dnf install 'https://github.com/cli/cli/releases/latest/download/gh_2.0.0_linux_amd64.rpm'
  ```
* **Arch Linux (pacman):**

  ```sh
  sudo pacman -S github-cli
  ```
* **Snap:**

  ```sh
  sudo snap install gh
  ```

Verify installation:

```sh
gh --version
```

---

## 🔑 Authentication

Authenticate with GitHub:

```sh
gh auth login
```

Options:

* Choose **GitHub.com** or **GitHub Enterprise**.
* Select **HTTPS** (recommended) or SSH.
* Authenticate using:

  * Browser login
  * Personal Access Token (PAT)

Check status:

```sh
gh auth status
```

Log out:

```sh
gh auth logout
```

---

## 🚀 Common Commands

### 🔹 Repository Management

| 📂 Task        | 🛠️ Command Example                |
| -------------- | ---------------------------------- |
| Clone repo     | `gh repo clone owner/repo`         |
| Create repo    | `gh repo create my-repo --public`  |
| Fork repo      | `gh repo fork owner/repo`          |
| List repos     | `gh repo list username --limit 10` |
| View repo info | `gh repo view owner/repo --web`    |

---

### 🔹 Issues

| 📂 Task          | 🛠️ Command Example                                     |
| ---------------- | ------------------------------------------------------- |
| Create issue     | `gh issue create --title "Bug: login" --body "Details"` |
| List issues      | `gh issue list --label bug`                             |
| View issue       | `gh issue view 42`                                      |
| Comment on issue | `gh issue comment 42 --body "Working on this!"`         |
| Close issue      | `gh issue close 42`                                     |

---

### 🔹 Pull Requests (PRs)

| 📂 Task     | 🛠️ Command Example                             |
| ----------- | ----------------------------------------------- |
| Create PR   | `gh pr create --base main --head feature/login` |
| View PR     | `gh pr view 123`                                |
| Checkout PR | `gh pr checkout 123`                            |
| Merge PR    | `gh pr merge 123 --squash --delete-branch`      |
| List PRs    | `gh pr list --state open`                       |

---

### 🔹 Actions & Workflows

| 📂 Task            | 🛠️ Command Example         |
| ------------------ | --------------------------- |
| View workflow runs | `gh run list`               |
| View workflow logs | `gh run view 42 --log`      |
| Trigger workflow   | `gh workflow run build.yml` |

---

### 🔹 Releases

| 📂 Task        | 🛠️ Command Example                                  |
| -------------- | ---------------------------------------------------- |
| Create release | `gh release create v1.0.0 --notes "Initial release"` |
| View releases  | `gh release list`                                    |
| Upload asset   | `gh release upload v1.0.0 ./build/output.zip`        |

---

### 🔹 Gists

| 📂 Task     | 🛠️ Command Example                |
| ----------- | ---------------------------------- |
| Create gist | `gh gist create file.txt --public` |
| List gists  | `gh gist list`                     |
| View gist   | `gh gist view <gist-id>`           |

---

### 🔹 Discussions

| 📂 Task           | 🛠️ Command Example                                                       |
| ----------------- | ------------------------------------------------------------------------- |
| List discussions  | `gh discussion list`                                                      |
| Create discussion | `gh discussion create --title "Design Ideas" --body "..." --category Q&A` |

---

## ⚙️ Advanced Usage

* **Aliases**: Shortcuts for long commands

  ```sh
  gh alias set co 'pr checkout'
  gh co 123
  ```

* **Extensions**: Install community commands

  ```sh
  gh extension install dlvhdr/gh-prs
  ```

* **Interactive Mode**: Step-by-step prompts

  ```sh
  gh issue create -w
  ```

* **Scripting with `gh`**:
  Example: List all PR titles in a repo

  ```sh
  gh pr list --json title -q ".[].title"
  ```

---

## 💡 Tips & Tricks

* Use `gh repo view --web` to open a repo in your browser instantly.
* Combine `gh` with **jq** for JSON parsing in scripts.
* Create **custom dashboards** using `gh api` calls.
* Automate **release notes** with `gh release`.

---

## 📚 Resources

* [GitHub CLI Docs](https://cli.github.com/manual/)
* [GitHub CLI Extensions](https://github.com/topics/gh-extension)
* [GitHub CLI Source Code](https://github.com/cli/cli)

---

> ⚡ *“With `gh`, you can do 80% of GitHub tasks without leaving the terminal.”*

```

---

````

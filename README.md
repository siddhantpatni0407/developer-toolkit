# 🚀 developer-toolkit

Welcome to **developer-toolkit** — a centralized, personal knowledge base and command reference for developers.

This repository consolidates essential CLI commands, setup steps, environment configurations, and productivity tips across a wide range of technologies and tools used in modern software development.

> 💡 Whether you're spinning up a new project, setting up a dev environment, or just forgot that one Docker flag — this toolkit has you covered.

---

## 📅 Last Updated: `2025-09-18 23:48 +0530`

---

## 📁 Categories Overview

<details open>
<summary>🔹 Setup & Environment (💡 Start Here)</summary>

| 🗂️ Category            | 📄 Description                          | 🔗 Documentation Link                                                |
| ---------------------- | --------------------------------------- | -------------------------------------------------------------------- |
| **Softwares List**     | Full list of developer software & tools | [ReadMe-Softwares-List.md](./Setup/ReadMe-Softwares-List.md)         |
| **IDE Plugins**        | IntelliJ IDEA & VS Code plugin list     | [ReadMe-IDE-plugins.md](./Setup/ReadMe-IDE-plugins.md)               |
| **Browser Extensions** | Developer browser extensions            | [ReadMe-browser-extensions.md](./Setup/ReadMe-browser-extensions.md) |

</details>

---

<details>
<summary>🔹 Version Control</summary>

| 🗂️ Category          | 📄 Description                                              | 🔗 Documentation Link                                      |
| -------------------- | ----------------------------------------------------------- | ---------------------------------------------------------- |
| **Git**              | Version control basics, setup, shortcuts, and CLI usage     | [git-commands.md](./Git/git-commands.md)                   |
| **GitHub CLI**       | Manage repos, issues, PRs directly from the terminal        | [github-cli.md](./Git/github-cli.md)                       |
| **GitHub Flow**      | Simple workflow with main + feature branches                | [github-best-practices.md](./Git/github-best-practices.md) |
| **Git Hooks**        | Automate tasks on commit, push, or merge (pre-commit, etc.) | [git-hooks.md](./Git/git-hooks.md)                         |
| **GitHub Workflows** | CI/CD, automation, linting, releases with GitHub Actions    | [github-workflows.md](./Git/github-workflows.md)           |

</details>

---

<details>
<summary>🔹 Programming Languages</summary>

| 🗂️ Category | 📄 Description                                                | 🔗 Documentation Link                                             |
| ----------- | ------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Java**    | Java CLI usage, builds, and environment setup                 | [java-commands-windows.md](./Java/java-commands-windows.md)       |
| **Python**  | Virtual environments, pip, and commands for Python            | [python-commands-windows.md](./Python/python-commands-windows.md) |
| **React**   | React CLI commands, tooling setup, and tips                   | [react-commands.md](./React/react-commands.md)                    |
| **React**   | React project standards, folder structure, and best practices | [react-best-practices.md](./React/react-best-practices.md)        |

</details>

---

<details>
<summary>🔹 Databases</summary>

| 🗂️ Category    | 📄 Description                                 | 🔗 Documentation Link                                                                                                                                              |
| -------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **PostgreSQL** | PgAdmin setup, DB commands, and best practices | [PgAdmin](https://www.pgadmin.org/download/) (external)                                                                                                            |
| **MongoDB**    | Common commands, queries, and setup (Windows)  | [README-MongoDB-Commands-Windows.md](./MongoDB/README-MongoDB-Commands-Windows.md)<br>[README-MongoDB-Setup-Windows.md](./MongoDB/README-MongoDB-Setup-Windows.md) |

</details>

---

<details>
<summary>🔹 Containers & Orchestration</summary>

| 🗂️ Category    | 📄 Description                                                              | 🔗 Documentation Link                                                         |
| -------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Docker**     | Commands, setup, Dockerfile basics                                          | [docker-commands.md](./Docker/docker-commands.md)                             |
| **Docker**     | Full Windows installation & container management guide                      | [README-Docker-Windows.md](./Docker/README-Docker-Windows.md)                 |
| **Kubernetes** | Kubectl usage, Minikube commands, deployments, services, cluster management | [kubernetes-commands.md](./Kubernetes/kubernetes-commands.md)                 |
| **Kubernetes** | Full Windows guide for Minikube setup & cluster management                  | [README-K8S-Minikube-Windows.md](./Kubernetes/README-K8S-Minikube-Windows.md) |

</details>

---

<details>
<summary>🔹 Cloud & Messaging</summary>

| 🗂️ Category      | 📄 Description                                                    | 🔗 Documentation Link                                                     |
| ---------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **AWS Kinesis**  | LocalStack-based Kinesis setup, CLI commands, and troubleshooting | [kinesis-commands.md](./AWS/Kinesis/kinesis-commands.md)                  |
| **AWS SQS**      | LocalStack-based SQS setup, CLI commands, and troubleshooting     | [sqs-commands.md](./AWS/SQS/sqs-commands.md)                              |
| **Apache Kafka** | Kafka setup (Windows), topic mgmt, producers/consumers, debugging | [kafka-command-windows.md](./AWS/Apache%20Kafka/kafka-command-windows.md) |

</details>

---

<details>
<summary>🔹 General Tools & Documentation</summary>

| 🗂️ Category       | 📄 Description                           | 🔗 Documentation Link                                                                      |
| ----------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------ |
| **General Tools** | Terminal tips, VS Code setup, utilities  | [windows-terminal-commands.md](./General%20Tools/windows-terminal-commands.md)             |
| **Documentation** | References, best practices, setup guides | [official-documentation-reference.md](./Documentation/official-documentation-reference.md) |

</details>

---

<details>
<summary>🔹 AI</summary>

| 🗂️ Category        | 📄 Description                                      | 🔗 Documentation Link                                        |
| ------------------ | --------------------------------------------------- | ------------------------------------------------------------ |
| **GitHub Copilot** | Best practices for using GitHub Copilot effectively | [best-practices.md](./AI/GitHub%20Copilot/best-practices.md) |
| **GitHub Copilot** | Useful commands and shortcuts for GitHub Copilot    | [commands.md](./AI/GitHub%20Copilot/commands.md)             |
| **GitHub Copilot** | Overview of Copilot models and their best uses      | [model-usages.md](./AI/GitHub%20Copilot/model-usages.md)     |
| **ChatGPT**        | Best practices for interacting with ChatGPT         | [best-practices.md](./AI/ChatGPT/best-practices.md)          |
| **ChatGPT**        | Overview of ChatGPT models and their best uses      | [model-usages.md](./AI/ChatGPT/model-usages.md)              |

</details>

---

## 🎯 Project Goals

- 🔁 **Reusability** — Avoid repetitive setups by reusing tried-and-true configs.
- ⚡ **Speed** — Quickly bootstrap projects or troubleshoot without digging through docs.
- 📚 **Learning** — Reinforce knowledge through documented experience.
- 🛠️ **Practicality** — Keep the focus on commands and setups actually used in real-world dev workflows.

---

## 🙋‍♂️ How to Use

- Browse categories (expand/collapse as needed) ☝️
- Copy-paste commands as needed 💻
- Use locally or star ⭐ the repo for quick reference
- Contribute via PRs 🔧 if you’d like to add improvements

---

## 🧑‍💻 Author

**Siddhant Patni**
[🌐 GitHub](https://github.com/siddhantpatni0407)

---

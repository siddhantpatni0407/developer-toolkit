# MongoDB Installation & Setup (Windows) – Detailed Guide

This guide explains how to install **MongoDB**, **Mongo Shell (mongosh)**, and **MongoDB Compass** on Windows. It also covers verification, PATH setup, testing, service management, and troubleshooting.

---

## Table of Contents

- [MongoDB Installation \& Setup (Windows) – Detailed Guide](#mongodb-installation--setup-windows--detailed-guide)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Install MongoDB Server](#install-mongodb-server)
    - [Option 1: MSI Installer (Recommended)](#option-1-msi-installer-recommended)
    - [Option 2: Chocolatey](#option-2-chocolatey)
  - [Install MongoDB Shell (mongosh)](#install-mongodb-shell-mongosh)
  - [Install MongoDB Compass (GUI)](#install-mongodb-compass-gui)
  - [Verify Installation](#verify-installation)
  - [Configure PATH Environment Variable (if needed)](#configure-path-environment-variable-if-needed)
  - [Connect \& Test MongoDB](#connect--test-mongodb)
  - [Backup \& Restore](#backup--restore)
  - [Troubleshooting](#troubleshooting)
  - [Notes \& Best Practices](#notes--best-practices)

---

## Prerequisites

- Windows 10 / 11 (64-bit)
- PowerShell or Command Prompt familiarity
- Optional: Chocolatey for easier installation
- Optional: VS Code or any editor for scripts

> 💡 Tip: For Windows Home edition, use WSL2 if you want Linux-like MongoDB setup.

---

## Install MongoDB Server

### Option 1: MSI Installer (Recommended)

1. Download from [MongoDB Download Center](https://www.mongodb.com/try/download/community)
2. Select **Windows**, version, and **MSI** package.
3. Run the installer:

   - Choose **Complete** installation.
   - Check **Install MongoDB as a Service** (Automatic start recommended).
   - Optionally, select **Install MongoDB Compass**.

4. Finish installation.

---

### Option 2: Chocolatey

```powershell
choco install mongodb -y
```

- MongoDB service starts automatically.
- Default service name: `MongoDB`.

---

## Install MongoDB Shell (mongosh)

1. Download from [https://www.mongodb.com/try/download/shell](https://www.mongodb.com/try/download/shell)
2. Run MSI installer and ensure **Add mongosh to PATH** is checked.
3. Verify installation:

```powershell
mongosh --version
```

---

## Install MongoDB Compass (GUI)

1. Download from [https://www.mongodb.com/try/download/compass](https://www.mongodb.com/try/download/compass)
2. Run installer.
3. Launch Compass and connect to:

```
mongodb://localhost:27017
```

---

## Verify Installation

1. Check MongoDB service:

```powershell
Get-Service -Name MongoDB
```

2. Start/stop service if needed:

```powershell
Start-Service -Name MongoDB
Stop-Service -Name MongoDB
```

3. Test MongoDB shell:

```powershell
mongosh
```

- Should connect to `localhost:27017`.

---

## Configure PATH Environment Variable (if needed)

1. Add MongoDB `bin` folder to system PATH:

   - Default path: `C:\Program Files\MongoDB\Server\<version>\bin`

2. Restart PowerShell / CMD to reflect changes.
3. Test:

```powershell
mongosh --version
```

---

## Connect & Test MongoDB

```js
// Switch to test database
use test

// Insert a document
db.test.insertOne({ name: "Siddhant", email: "siddhant@example.com" });

// Retrieve documents
db.test.find();

// Show all databases
show dbs;

// Show collections
show collections;
```

---

## Backup & Restore

```powershell
# Backup database
mongodump --db test --out C:\backups\testBackup

# Restore database
mongorestore --db test C:\backups\testBackup\test
```

> 💡 Tip: Use timestamped backup folders for regular backups.

---

## Troubleshooting

- `mongosh : The term 'mongosh' is not recognized` → Ensure PATH includes MongoDB `bin`.
- `Cannot start MongoDB service` → Check if another MongoDB instance is running or ports conflict.
- `Error binding to port 27017` → Stop other services using the port, or change port in `mongod.cfg`.

---

## Notes & Best Practices

- MongoDB service starts automatically; you can configure it as Manual if preferred.
- Use **Compass** for GUI management and **mongosh** for CLI.
- Enable authentication for production use.
- Use indexes on frequently queried fields to improve performance.
- Backup regularly using `mongodump`.
- For scripting and automation, use PowerShell scripts to start/stop services.

---

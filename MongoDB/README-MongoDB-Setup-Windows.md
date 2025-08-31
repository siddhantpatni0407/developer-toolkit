# MongoDB Installation & Setup (Windows) – Detailed Guide

This guide explains how to install **MongoDB**, **Mongo Shell (mongosh)**, **MongoDB Compass**, and **MongoDB Database Tools** on Windows. It also covers verification, PATH setup, testing, service management, and **backup & restore**.

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
  - [Install MongoDB Database Tools (Command Line)](#install-mongodb-database-tools-command-line)
  - [Verify Installation](#verify-installation)
  - [Connect \& Test MongoDB](#connect--test-mongodb)
  - [Backup \& Restore](#backup--restore)
    - [Basic Backup \& Restore](#basic-backup--restore)
    - [Backup All Databases](#backup-all-databases)
    - [Restore All Databases](#restore-all-databases)
    - [Additional Tips](#additional-tips)
  - [Troubleshooting](#troubleshooting)
  - [Notes \& Best Practices](#notes--best-practices)

---

## Prerequisites

* Windows 10 / 11 (64-bit)
* PowerShell or Command Prompt familiarity
* Optional: Chocolatey for easier installation
* Optional: VS Code or any editor for scripts

> 💡 Tip: For Windows Home edition, use WSL2 for Linux-like MongoDB setup if preferred.

---

## Install MongoDB Server

### Option 1: MSI Installer (Recommended)

1. Download from [MongoDB Download Center](https://www.mongodb.com/try/download/community)
2. Select **Windows**, version, and **MSI** package.
3. Run the installer:

   * Choose **Complete** installation.
   * Check **Install MongoDB as a Service** (Automatic start recommended).
   * Optionally, select **Install MongoDB Compass**.
4. Finish installation.

---

### Option 2: Chocolatey

```powershell
choco install mongodb -y
```

* MongoDB service starts automatically.
* Default service name: `MongoDB`.

---

## Install MongoDB Shell (mongosh)

1. Download from [MongoDB Shell Download](https://www.mongodb.com/try/download/shell)
2. Run MSI installer and ensure **Add mongosh to PATH** is checked.
3. Verify installation:

```powershell
mongosh --version
```

---

## Install MongoDB Compass (GUI)

1. Download from [MongoDB Compass Download](https://www.mongodb.com/try/download/compass)
2. Run installer.
3. Launch Compass and connect to:

```
mongodb://localhost:27017
```

---

## Install MongoDB Database Tools (Command Line)

The **MongoDB Database Tools** include `mongodump`, `mongorestore`, `mongoimport`, `mongoexport`, `bsondump`, etc.

1. Download from [MongoDB Database Tools](https://www.mongodb.com/try/download/database-tools)
2. Select **Windows** and version compatible with your MongoDB server.
3. Extract the `.zip` file to a folder, e.g., `C:\mongodb-database-tools`.
4. Add the folder to your **PATH** environment variable:

```powershell
setx PATH "$env:PATH;C:\mongodb-database-tools\bin"
```

5. Restart PowerShell / CMD and verify:

```powershell
mongodump --version
mongorestore --version
mongoimport --version
mongoexport --version
```

> 💡 Tip: These tools are required for full backup/restore and import/export operations.

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

* Should connect to `localhost:27017`.

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

### Basic Backup & Restore

```powershell
# Backup a database
mongodump --db test --out C:\backups\testBackup

# Restore a database
mongorestore --db test C:\backups\testBackup\test
```

### Backup All Databases

```powershell
mongodump --out C:\backups\allDBsBackup
```

### Restore All Databases

```powershell
mongorestore C:\backups\allDBsBackup
```

### Additional Tips

* Use timestamped folders:

```powershell
$timestamp = Get-Date -Format "yyyyMMdd_HHmmss"
mongodump --db test --out "C:\backups\testBackup_$timestamp"
```

* For authenticated databases:

```powershell
mongodump --username <user> --password <pass> --authenticationDatabase admin --db test --out C:\backups\testBackup
mongorestore --username <user> --password <pass> --authenticationDatabase admin --db test C:\backups\testBackup\test
```

---

## Troubleshooting

* `mongosh : The term 'mongosh' is not recognized` → Ensure PATH includes MongoDB `bin`.
* `Cannot start MongoDB service` → Check if another MongoDB instance is running or ports conflict.
* `Error binding to port 27017` → Stop other services using the port, or change port in `mongod.cfg`.
* `mongodump / mongorestore : command not found` → Verify PATH includes MongoDB Database Tools `bin` folder.

---

## Notes & Best Practices

* MongoDB service starts automatically; can configure as Manual if preferred.
* Use **Compass** for GUI management and **mongosh** for CLI.
* Enable authentication for production.
* Use indexes on frequently queried fields for performance.
* Backup regularly using `mongodump`.
* Automate backup/restore using PowerShell scripts in production or testing.

---

## 🛠️ Configuring and Managing Log Rotation using Logrotate on Ubuntu

<p align="center">
  <img src="https://www.pc-freak.net/images/logrotate-linux-logo.png" alt="Logrotate Logo" width="150"/>
</p>

---

## 👤 Author Information
| Created | Version | Author | Comment | Reviewer |
| --- | --- | --- | --- | --- |
| 14-04-2025 | V1 | Shivani Narula | Internal Review | Siddharth Pawar |
| 16-04-2025 | V1.1 | Shivani Narula | Internal Review | Siddharth Pawar |

---

## 📚 Table of Contents

- [🧩 Introduction](#-introduction)
- [❓ Why Use Log Rotation?](#-why-use-log-rotation)
- [📁 What is Logrotate?](#-what-is-logrotate)
- [🔧 Prerequisites & Setup](#-prerequisites--setup)
  - [⚙️ Step 1: Install Logrotate](#️-step-1-install-logrotate-if-not-already-installed)
  - [📁 Step 2: Create Log File for Your App](#-step-2-create-log-file-for-your-app)
- [🧾 Configuration](#-configuration)
  - [🛠️ Step 3: Create Logrotate Config](#️-step-3-create-logrotate-config)
- [🧪 Testing Setup](#-testing-setup)
  - [🧪 Step 4: Test the Setup](#-step-4-test-the-setup)
- [🔁 Continuous Rotation](#-continuous-rotation)
  - [🔁 Step 5: Add More Logs and Rotate Again](#-step-5-add-more-logs-and-rotate-again)
- [🛠️ Troubleshooting Tips](#️-troubleshooting-tips)
- [📦 Best Practices](#-best-practices)
- [📘 References](#-references)
- [📇 Contacts](#-contacts)

---

### 🧩 Introduction
This SOP guides you through configuring **Logrotate** on Ubuntu — a robust tool that automates log management. You’ll learn **why** log rotation matters, **what** Logrotate is, and **how** to configure it with real-world examples.

As applications generate logs, these files can grow large and clutter your storage if not managed properly. To keep systems clean, efficient, and compliant, **log rotation** is essential.

---

### 📁 What is Logrotate?

**Logrotate** is a Linux utility that manages the automatic rotation and compression of log files. It prevents log files from consuming excessive disk space by rotating, compressing, and eventually deleting old logs.

---

### ❓**Why Use Log Rotation?**
Log rotation is essential for maintaining system health, performance, and compliance by managing growing log files efficiently.

> - **Prevent Disk Overflow**: Large logs can consume all available disk space.  
> - **Improve Performance**: Smaller log files are quicker to read, write, and analyze.  
> - **Enable Compliance**: Keep logs only for the duration required by policies.  
> - **Simplify Debugging**: Archived logs keep historical issues traceable and organized.  

---

## 🔧 Prerequisites & Setup

---

### ⚙️ Step 1: Install Logrotate (if not already installed)

```bash
sudo apt update
sudo apt install logrotate
```

Check the version:

```bash
logrotate --version
```

---

### 📁 Step 2: Create Log File for Your App

Let’s assume your app writes logs to `/var/log/myapp1/myapp1.log`.

```bash
sudo mkdir -p /var/log/myapp1
sudo touch /var/log/myapp1/myapp1.log
sudo chown root:adm /var/log/myapp1/myapp1.log
```

---

## 🧾 Configuration

---

### 🛠️ Step 3: Create Logrotate Config

Create a file at `/etc/logrotate.d/myapp1`

```bash
sudo nano /etc/logrotate.d/myapp1
```

Paste the following configuration:

```conf
/var/log/myapp1/myapp1.log {

    # Rotate the log file daily
    daily

    # Keep a maximum of 5 old log files
    rotate 5

    # Do not show an error if the log file is missing
    missingok

    # Compress the old log files
    compress

    # Delay compression by one rotation cycle
    delaycompress

    # Do not rotate the log file if it is empty
    notifempty

    # After rotation, create a new log file with these permissions and ownership
    # adm is a standard group for managing log file access securely.
    create 0640 root adm
}
```

✅ This configuration:
- Rotates log **daily**
- Keeps last **5 logs**
- Compresses old logs (with 1-cycle delay)
- Skips rotation if log is empty
- Recreates the log file with correct permission

---

## 🧪 Testing Setup

---

### 🧪 Step 4: Test the Setup

#### a) Add a test log entry

```bash
echo "Test log entry - $(date)" | sudo tee -a /var/log/myapp1/myapp1.log
```

#### b) Simulate Log Rotation (Dry Run)

```bash
sudo logrotate -d /etc/logrotate.d/myapp1
```

#### c) Force Log Rotation

```bash
sudo logrotate -f /etc/logrotate.d/myapp1
```

Check the log folder:

```bash
ls -l /var/log/myapp1/
```

Expected output after first rotation:

```
myapp1.log
myapp1.log.1
```

---

## 🔁 Continuous Rotation

---

### 🔁 Step 5: Add More Logs and Rotate Again

```bash
echo "Another log entry - $(date)" | sudo tee -a /var/log/myapp1/myapp1.log
sudo logrotate -f /etc/logrotate.d/myapp1
```

Check again:

```bash
ls -l /var/log/myapp1/
```

Expected output after two forced rotations:

```
myapp1.log
myapp1.log.1       ← latest rotated log (uncompressed)
myapp1.log.2.gz    ← previous log, now compressed
```

---

### 🛠️ Troubleshooting Tips

| Issue | Solution |
|-------|----------|
| Logs not rotating | Check paths, permissions |
| Rotation too frequent | Verify interval and timestamps |
| App not logging | Use `create` and `postrotate` to reopen file handles |
| Rotation skipped	| Ensure log is not empty if notifempty is set |

---

### 📦 Best Practices

| Practice                                      | Description                                                                 |
|----------------------------------------------|-----------------------------------------------------------------------------|
| `compress` and `delaycompress`               | Save disk space by compressing old logs efficiently                        |
| Always test with `-d`                        | Use dry-run mode before applying changes to ensure no errors               |
| Set retention based on space and compliance  | Configure log retention to match system capacity and policy requirements   |
| Reload app using `postrotate` if required    | Gracefully restart services after log rotation when necessary              |

---

## 📇 Contacts

| Name | Email Address |
| --- | --- |
| Shivani Narula | shivani.narula.snaatak@mygurukulam.co |

---
## 📘 References

📘 **References**

| Links                                                                                                                             | Descriptions                          |
|-----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| [https://linux.die.net/man/8/logrotate](https://linux.die.net/man/8/logrotate)                                                   | man logrotate                         |
| [https://betterstack.com/community/guides/logging/how-to-manage-log-files-with-logrotate-on-ubuntu-20-04/#getting-started-with-logrotate](https://betterstack.com/community/guides/logging/how-to-manage-log-files-with-logrotate-on-ubuntu-20-04/#getting-started-with-logrotate) | Manage Log Files with logrotate       |


siddharth reply 
Attach LOGO
Change Intro
Must be in tabular format
Arrange content

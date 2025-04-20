# React JS | SOP's for npm

<p align="center">
  <img src="https://media2.dev.to/dynamic/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fsu2i78wr05f0cy25th94.png" alt="NPM Logo" width="500"/>
</p>

---
## Author Information
| Created | Version | Last Modified | Author | Comment | Reviewer |
| --- | --- | --- | --- | --- | --- |
| 16-04-2025 | V1.1 | 17-04-2025 | Shivani Narula | Internal Review | Siddharth Pawar |
| 16-04-2025 | V2 | 17-04-2025 | Shivani Narula | L0 Review | Naveen Haswani |

---

## Table of Contents
- [Introduction](#introduction)  
- [Step-by-step-installation-guide](#step-by-step-installation-guide)
  - [Step 1: Check & Install curl](#step-1-check--install-curl)  
  - [Step 2: Check & Install Node.js and npm](#step-2-check--install-nodejs-and-npm)  
  - [Step 3: Testing Setup](#step-3-testing-setup)  
    - [Create React App](#create-react-app)  
- [Troubleshooting Tips](#troubleshooting-tips)  
- [Best Practices](#best-practices)  
- [Conclusion](#conclusion)  
- [Contacts](#contacts)  
- [Reference Table](#references-table)  

---

## Introduction

This document provides a detailed Standard Operating Procedure (SOP) for setting up a ReactJS application using npm (Node Package Manager). It is part of the common application stack used in modern frontend development.

ReactJS, maintained by Meta (Facebook), is a declarative, efficient, and flexible JavaScript library for building user interfaces.

---

### 🔁 Common npm Commands

| Command                     | Purpose                                      |
|-----------------------------|----------------------------------------------|
| `npm install <package>`     | Install a package locally                    |
| `npm install -g <package>`  | Install a package globally                   |
| `npm uninstall <package>`   | Uninstall a local package                    |
| `npm update`                | Update all local packages                    |
| `npm list`                  | View installed packages                      |
| `npm list -g --depth=0`     | View globally installed packages             |
| `npm audit`                 | Run security check on installed packages     |
| `npm cache clean --force`   | Clear the npm cache                          |

---
## Step-by-Step Installation Guide

##  Step 1: Check & Install curl

### Check if curl is installed
Run the following command:
```bash
curl --version
```
> If curl is installed, this will show version details. If not, you'll see an error like `curl: command not found`.

---

### To install curl, run:
> 1️⃣ **Step 1: System Update Command**  
> Before proceeding, it's **highly recommended** to follow the update instructions from the official documentation.  
> 👉 **Follow Step 3 here**: [Ubuntu Basic System Commands](https://github.com/snaatak-Downtime-Crew/Documentation/blob/durgesh_scrums_3/common_stack/operating_system/ubuntu/sop/commoncommands/README.md#1-basic-system-commands)
>
> 
> 2️⃣ **Step 2: Install Curl**  
>```bash
>sudo apt install curl -y
>```
---

## Step 2: Check & Install Node.js and npm

###  First, check if Node.js and npm are already installed:

```bash
node -v
npm -v
```
> If both commands return version numbers, skip to [Step 2: Create React App For Demo](#-step-2-create-react-app-for-demo).

### If not installed, run the following to install:

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```

>📌 **Explanation:**
>- First command sets up the NodeSource repo.  
>- Second command installs both Node.js and npm.  

---

## Step 3: Testing setup

### Create React App
Use `npx` (comes with npm) to create a new React project:
```bash
npx create-react-app my-app
```
> my-app is your project folder name. You can choose any name.
> This command installs React, React-DOM, and required dependencies automatically.

---

### Go into the project directory and start the app:
```bash
cd my-app
npm start
```
---

### Open your browser and go to:
```
http://<your-server-ip>:3000
```
> You should see the default React welcome screen.

---

### Check that the server is listening:
```bash
sudo lsof -i :3000
```
> Expected output should show `node` running and listening on port `3000`. Also verify logs/output in the terminal for build success.

---

## Troubleshooting Tips

| Problem | Solution |
|--------|----------|
| Port 3000 not accessible | Open the port in AWS Security Group or firewall |
| `npx` not found | Ensure Node.js and npm are correctly installed |
| App not starting | Delete `node_modules` and reinstall dependencies using `npm install` |

---

## Best Practices

✅ Do not commit node_modules/ to Git.
It's large and unnecessary—use .gitignore to skip it.

✅ Use .env files for configuration.
Keep sensitive values like API keys outside your code.

✅ Keep dependencies updated.
Run npm update regularly to get the latest and secure versions. 

---

## Conclusion

This SOP helps you set up a ReactJS project using npm in a clear and consistent way. By checking your system, verifying tools like curl, node, and npm, and following step-by-step commands, you can quickly get started with React. Using npm makes it easier to manage packages and build scalable React apps. Follow these steps across all projects to keep your workflow simple, fast, and reliable.

---

## Contacts

| Name           | Email Address                                 |
|----------------|-----------------------------------------------|
| Shivani Narula | shivani.narula.snaatak@mygurukulam.co         |

---

## References

| Links                                                                                      | Descriptions                        |
|--------------------------------------------------------------------------------------------|-------------------------------------|
| [https://create-react-app.dev/docs/getting-started/](https://create-react-app.dev/docs/getting-started/) | ReactJS Official Docs              |
| [https://nodejs.org](https://nodejs.org)                                                   | Node.js Official Website            |
| [https://www.youtube.com/watch?v=1HOuGMGV00g](https://www.youtube.com/watch?v=1HOuGMGV00g) | YouTube: How to Create React App   |

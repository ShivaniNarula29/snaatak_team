# 🚀 Common Stack | Application | React JS | SOP's for npm

<p align="center">
  <img src="https://www.viithiisys.com/images/uploads/reactjs.png" alt="Logrotate Logo" width="500"/>
</p>

---

## 👤 Author Information

| Created     | Version   | Author           | Comment         | Reviewer         |
|-------------|-----------|------------------|------------------|------------------|
| 16-04-2025  | V1 | Shivani Narula   | Internal review  | Siddharth Pawar  |
| 17-04-2025  | V1.1 | Shivani Narula  | Internal review | Siddharth Pawar  |
---

## 📚 Table of Contents

- [🧩 Introduction](#-introduction)  
- [📁 What is ReactJS?](#-what-is-reactjs)
- [❓ Why Use npm to Set Up React?](#-why-use-npm-to-set-up-react)  
- [🔧 Prerequisites & Setup](#-prerequisites--setup)  
- [⚙️ Step 1: Check & Install Node.js and npm](#️-step-1-check--install-nodejs-and-npm)  
- [📁 Step 2: Create React App](#-step-2-create-react-app)  
- [🧪 Testing Setup](#-testing-setup)  
- [🧪 Step 3: Test the Setup](#-step-3-test-the-setup)  
- [🛠️ Troubleshooting Tips](#️-troubleshooting-tips)  
- [📦 Best Practices](#-best-practices)  
- [🧾 Conclusion](#-conclusion)  
- [📘 References](#-references)  
- [📇 Contacts](#-contacts)

---

## 🧩 Introduction

This document provides a detailed Standard Operating Procedure (SOP) for setting up a ReactJS application using npm (Node Package Manager). It is part of the common application stack used in modern frontend development.

ReactJS, maintained by Meta (Facebook), is a declarative, efficient, and flexible JavaScript library for building user interfaces.

---

## 📁 What is ReactJS?

ReactJS is a JavaScript library used for building interactive user interfaces. It allows developers to create large web applications that can change data, without reloading the page.

---

### ❓**Why Use npm to Set Up React?**
npm is the default package manager for Node.js and is widely used in JavaScript development. It simplifies setting up, managing, and scaling React projects with ease.

> - **🆕 Latest Features**: Easily access the most up-to-date React versions and tools.  
> - **⚡ Quick Start**: Use `create-react-app` for instant project scaffolding.  
> - **📦 Dependency Management**: Automatically handles React libraries and updates.  
> - **🌐 Ecosystem Support**: Tap into thousands of packages, tools, and plugins for React.  
> - **🔄 Version Control**: Lock specific package versions for consistent builds.  
> - **🛠️ Developer Tools**: Integrates well with linters, bundlers, and testing tools.    

---

## 🔧 Prerequisites & Setup

Before setting up React using npm, ensure the following prerequisites are met:


### ✅ System Requirements for npm + React.js on Ubuntu

| Component   | Requirement                          |
|------------|---------------------------------------|
| OS         | Ubuntu 18.04 or later                 |
| CPU        | Dual-core 1.5 GHz or faster           |
| RAM        | Minimum: 2 GB (Recommended: 4 GB or more) |
| Storage    | At least 1 GB free (for Node, npm, React) |
| Internet   | Required for downloading packages     |
| Privileges | sudo/root access                      |


### ✅ Tools Required:
- `curl`  
- `Node.js` (with `npm`)  

---


### 🔍 Check if curl is installed

Run the following command:

```bash
curl --version
```

If curl is installed, this will show version details. If not, you'll see an error like `curl: command not found`.

### 🛠️ To install curl, run:

```bash
sudo apt update
sudo apt install curl -y
```

---

## ⚙️ Step 1: Check & Install Node.js and npm

### 🔍 First, check if Node.js and npm are already installed:

```bash
node -v
npm -v
```

If both commands return version numbers, skip to [Step 2: Create React App](#-step-2-create-react-app).

### 🛠️ If not installed, run the following to install:

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```

📌 **Explanation:**
- First command sets up the NodeSource repo.  
- Second command installs both Node.js and npm.  

---

## 📁 Step 2: Create React App

Use `npx` (comes with npm) to create a new React project:

```bash
npx create-react-app my-app
```

🔹 `my-app` is your project folder name. You can choose any name.

This command installs React, React-DOM, and required dependencies automatically.

---

## 🧪 Testing Setup

Go into the project directory and start the app:

```bash
cd my-app
npm start
```

Open your browser and go to:
```
http://<your-server-ip>:3000
```
You should see the default React welcome screen.

---

## 🧪 Step 3: Test the Setup

Check that the server is listening:

```bash
sudo lsof -i :3000
```

Expected output should show `node` running and listening on port `3000`.

Also verify logs/output in the terminal for build success.

---

## 🛠️ Troubleshooting Tips

| Problem | Solution |
|--------|----------|
| Port 3000 not accessible | Open the port in AWS Security Group or firewall |
| `npx` not found | Ensure Node.js and npm are correctly installed |
| App not starting | Delete `node_modules` and reinstall dependencies using `npm install` |

---

## 📦 Best Practices

✅ Do not commit node_modules/ to Git.
It's large and unnecessary—use .gitignore to skip it.

✅ Use .env files for configuration.
Keep sensitive values like API keys outside your code.

✅ Keep dependencies updated.
Run npm update regularly to get the latest and secure versions. 

---

## 🧾 Conclusion

This SOP helps you set up a ReactJS project using npm in a clear and consistent way. By checking your system, verifying tools like curl, node, and npm, and following step-by-step commands, you can quickly get started with React. Using npm makes it easier to manage packages and build scalable React apps. Follow these steps across all projects to keep your workflow simple, fast, and reliable.

---

## 📇 Contacts

| Name           | Email Address                                 |
|----------------|-----------------------------------------------|
| Shivani Narula | shivani.narula.snaatak@mygurukulam.co         |

---

📘 **References**

| Links                                                                                      | Descriptions                        |
|--------------------------------------------------------------------------------------------|-------------------------------------|
| [https://create-react-app.dev/docs/getting-started/](https://create-react-app.dev/docs/getting-started/) | ReactJS Official Docs              |
| [https://nodejs.org](https://nodejs.org)                                                   | Node.js Official Website            |
| [https://www.youtube.com/watch?v=1HOuGMGV00g](https://www.youtube.com/watch?v=1HOuGMGV00g) | YouTube: How to Create React App   |

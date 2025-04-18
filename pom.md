# ☕ JAVA | POM.xml Documentation

<p align="center">
  <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQmSmJgXu6kW8ONXMTLq0LD6BJGFV3Hoc0DRg&s" alt="Maven Logo" width="400"/>
</p>

---

## 👤 Author Information

| Created | Version | Last Modified | Author | Comment | Reviewer |
| --- | --- | --- | --- | --- | --- |
| 18-04-2025 | V1 | 18-04-2025 | Shivani Narula | Internal Reviewer | Siddharth Pawar |

---

## 📁 Table of Contents

- [Introduction](#introduction)
- [What is pom.xml?](#what-is-pomxml)
- [Why is it Used?](#why-is-it-used)
- [Key Features](#key-features)
- [Getting Started](#getting-started)  
   - [Prerequisites](#prerequisites)  
   - [Installation](#installation)  
   - [Directory Structure](#directory-structure)  
- [Structure of pom.xml](#structure-of-pomxml)
- [How to Define Dependencies](#how-to-define-dependencies)
- [Best Practices](#best-practices)
- [Real-World Example](#real-world-example)
- [Conclusion](#conclusion)
- [Contact](#contact)
- [References](#references)

---

## ✨ Introduction

In Java projects using Maven, `pom.xml` is the heart of the project’s configuration. It tells Maven how to build your application, manage dependencies, and organize plugins.

---

## 📦 What is `pom.xml`?

- `pom.xml` stands for **Project Object Model XML**.
- It’s a special XML file used by **Apache Maven** to define your project setup.
- It contains details like:
  - Project name, version, and description
  - Java dependencies (external libraries)
  - Build plugins and configuration
  - Project structure (like parent/child modules)

---

## ❓ Why is it Important?

> -  **Manages Dependencies**: Automatically downloads and updates libraries (like Spring, Hibernate).
> -  **Controls Build Process**: Compiles, tests, and packages your app.
> -  **Supports Reusability**: Shared configs via parent/child modules.
> -  **Reduces Manual Work**: Automates tasks like versioning, testing, and packaging.

---

## ⚙️ Key Features

| Feature | Description |
|--------|-------------|
| Dependency Management | Automatically pulls required libraries from Maven Central or other repos |
| Plugin Support | Integrates tools for testing, packaging, etc. |
| Profiles | Enables different builds for dev, test, prod |
| Multi-module Support | Defines parent-child relationships |
| Build Lifecycle | Manages phases like compile, test, package, install, deploy |
| Version Control | Allows you to lock or update dependency versions |
| Project Info | Defines project name, version, description, etc. |

---
## 🚀 Getting Started

### 🔹 Prerequisites

- Java JDK 17 or 21 (recommended)
- Apache Maven (v3.6+ recommended)
- An IDE (e.g., IntelliJ IDEA, Eclipse)

### 🔹 Installation

Install Maven (if not already installed):

```bash
sudo apt update
sudo apt install maven

```

Verify:

```bash
mvn -v

```

### 🔹 Directory Structure

```
my-app/
├── pom.xml
└── src/
    ├── main/
    │   └── java/
    └── test/
        └── java/

```

---

## 🔁 Maven `pom.xml` Workflow

This section outlines the high-level workflow Maven follows when it processes the `pom.xml` file:

![image](https://github.com/user-attachments/assets/9921f68f-73c8-4b3d-b449-4af31941f380)


1. **🔧 Initialization**  
   Maven reads the `pom.xml` file and initializes the build process using the specified configurations.

2. **📦 Dependency Resolution**  
   It checks for required dependencies and downloads them from remote repositories (like Maven Central).

3. **🏗️ Build Lifecycle Execution**  
   Executes the standard Maven lifecycle phases:  
   - `validate`  
   - `compile`  
   - `test`  
   - `package`  
   - `verify`  
   - `install`  
   - `deploy`

4. **🔌 Plugin Execution**  
   Executes plugins configured in the `pom.xml`, such as:  
   - Code analysis tools  
   - Compiler plugins  
   - Test runners  
   - Report generators

5. **📁 Packaging**  
   The compiled code is packaged into formats like:  
   - `.jar` – Java ARchive  
   - `.war` – Web ARchive  
   - `.ear` – Enterprise ARchive  

6. **🚀 Deployment**  
   Deploys the packaged application to a remote repository or a production/test server.

> 💡 This workflow ensures builds are repeatable, consistent, and maintainable across environments.

---

## 📦 Important Tags in `pom.xml`

The following table outlines the most commonly used and practically important tags in any real-world Maven project.

| Tag             | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| `<groupId>`      | Unique org or project name (like `com.mycompany.app`)                  |
| `<artifactId>`   | Name of the project or module                                           |
| `<version>`      | Project version (e.g., `1.0.0`)                                         |
| `<dependencies>` | Section listing required libraries                                      |
| `<build>`        | Contains build-related info (plugins, final name, resources, etc.)      |
| `<repositories>` | Define custom repo URLs (if not using Maven Central)                    |
| `<properties>`   | Global project settings (e.g., Java version, encoding)                  |
| `<profiles>`     | Conditional build settings for different environments                   |

> ✅ These tags help Maven uniquely identify your project, resolve dependencies, and manage the build lifecycle effectively.

---

## 🧱 Structure of `pom.xml`

A typical `pom.xml` starts with the basic tags and can be extended with optional but commonly used sections for flexibility and control.

### 🔹 Basic Example:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>my-app</artifactId>
  <version>1.0.0</version>
</project>
```

---

## 📌 How to Define Dependencies

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>3.1.0</version>
  </dependency>
</dependencies>
```

> - **groupId** – Organization or company name
> - **artifactId** – Library/module name
> - **version** – Specific version to use

Maven will fetch this from its central repository.

---

## ✅ Best Practices for Dependency Versioning

### 1. **Avoid Using SNAPSHOT Versions in Production**

- **SNAPSHOT** versions (like `1.2.0-SNAPSHOT`) are **unstable** and meant for **development/testing**.
- They change frequently and may cause unexpected behavior.

✔ Use **fixed/stable versions** like `1.2.0` in production

❌ Avoid `1.2.0-SNAPSHOT` in final releases

---

### 2. **Use Dependency Management for Version Control**

If you have **multiple modules** or **repeat the same dependency**, define versions in a `<dependencyManagement>` block in the parent `pom.xml`.

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.13.3</version>
    </dependency>
  </dependencies>
</dependencyManagement>
```

Then in child modules:

```xml
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
</dependency>
```

---

### 3. **Use Properties to Declare Versions**

Avoid hardcoding versions multiple times.

```xml
<properties>
  <jackson.version>2.13.3</jackson.version>
</properties>

<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>${jackson.version}</version>
</dependency>
```

Update the version in **one place only**, and it applies everywhere.

---

### 4. **Pin Versions Explicitly**

Never omit the `<version>` tag unless you manage it in a parent or BOM (Bill of Materials).

✅ Always specify version **somewhere**

❌ Don’t rely on Maven to pick the latest — it may break later due to updates

---

### 5. **Use BOMs for Consistent Versioning**

A **BOM** is a `pom.xml` file from a library author that predefines compatible versions of multiple related libraries.

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-dependencies</artifactId>
      <version>3.2.1</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

---

### 6. **Regularly Update Dependencies**

Outdated versions can have:

- Bugs
- Security vulnerabilities
- Missing new features

Use tools like:

- `mvn versions:display-dependency-updates`
- Dependabot (GitHub)
- OWASP Dependency Check

---

### 7. **Avoid Using Version Ranges**

Maven supports things like:

```xml
<version>[1.0,2.0)</version>
```

> - Always specify versions to avoid unexpected changes.
> - Use a parent POM for multi-module projects.
> - Define testing frameworks like JUnit in `pom.xml`.
> - Use build plugins like `maven-compiler-plugin`.
> - Add meaningful comments for maintainers.

---

## 🌐 Real-World Example

Suppose you're building a web app using Spring Boot:

- Add `spring-boot-starter-web` in `dependencies`
- Add `maven-compiler-plugin` for Java version
- Define `dev`, `test`, and `prod` profiles
- Maven will handle compilation, dependency download, and packaging

🎯 Result: Your build process becomes smooth, fast, and repeatable!

---

## Licensing

The `pom.xml` file itself is not licensed, but the project and its dependencies must comply with their respective licenses. Maven and its core plugins are licensed under the **Apache License 2.0**.

---

## 🧠 Conclusion

Understanding and managing pom.xml is essential for any Maven-based Java project. This documentation helps developers and DevOps engineers structure their project dependencies, build lifecycle, and plugin configurations effectively while promoting best practices for versioning and maintainability.

> - 📦 Central place for managing dependencies  
> - 🔄 Automates build, test, and package lifecycle  
> - 💡 Promotes consistency across teams and environments  
> - 🛠️ Ideal for both single and multi-module Java projects  

It keeps your Java project clean, scalable, and easy to maintain.

---

## 📇 Contact

| Name | Email Address |
|------|----------------|
| Shivani Narula | shivani.narula.snaatak@mygurukulam.co |

---

## 📚 Reference Table

| Link | Description |
|------|-------------|
| [https://maven.apache.org/pom.html](https://maven.apache.org/pom.html) | Official Maven POM Reference |
| [https://maven.apache.org/guides/introduction/introduction-to-the-pom.html](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) | Intro to POM |
| [https://spring.io/guides/gs/maven/](https://spring.io/guides/gs/maven/) | Spring Guide for Maven |

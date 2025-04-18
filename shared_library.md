# 📚 Shared Library Documentation

<p align="center">
  <img src="https://miro.medium.com/v2/resize:fit:1116/1*5A8OrocBg3OhG4XHYoF3tQ.jpeg" width="500"/>
</p>

---

## 👤 Author Information
| Created | Version | Last Modified | Author | Comment | Reviewer |
| --- | --- | --- | --- | --- | --- |
| 18-04-2025 | V1 | 18-04-2025 | Shivani Narula | Internal Review | Siddharth Pawar |

---

## 📑 Table of Contents

- [Introduction](#introduction)
- [What is a Shared Library?](#what-is-a-shared-library)
- [Why Use a Shared Library?](#why-use-a-shared-library)
- [Advantages](#-advantages)
- [Disadvantages](#-disadvantages)
- [Workflow](#workflow)
  - [Structure (Example for Jenkins Shared Library)](#-structure-example-for-jenkins-shared-library)
  - [Execution Flow](#-execution-flow)
- [vars vs src – Key Differences](#vars-vs-src--key-differences)
- [Best Practices](#best-practices)
- [Conclusion](#-conclusion)
- [Contacts](#-contacts)
- [Reference Table](#-reference-table)

---

## Introduction
A shared library is a reusable collection of code or scripts used across multiple automation pipelines. It helps standardize and simplify automation by centralizing common tasks.

---

## **What is a Shared Library?**

A **Shared Library** is a modular, reusable, and centralized set of scripts, functions, or code blocks (typically in languages like Groovy, Python, or Bash) that can be included in various automation pipelines, infrastructure provisioning scripts, or deployments to promote DRY (Don't Repeat Yourself) principles.

In Jenkins, this refers to a custom library used to define reusable pipeline steps.

---

## **Why Use a Shared Library?**

- Promotes **code reuse** across multiple projects.
- Simplifies maintenance by centralizing logic.
- Reduces duplication and inconsistencies.
- Enables **version control** and easy rollbacks.
- Ensures **standardization** across teams or environments.

---

### ✅ Advantages

| Feature | `vars/` Advantages                                              | `src/` Advantages                                                   |
|---------|-----------------------------------------------------------------|----------------------------------------------------------------------|
| Simplicity | Easy to write and use directly in `Jenkinsfile`.               | Organizes complex logic in a clean, OOP manner.                      |
| Auto-discovery | Automatically available as global functions.                | Enables modular and reusable code with packages.                     |
| Quick Access | Great for quick prototyping or simple pipeline steps.        | Promotes good design with separation of concerns.                    |
| Readability | Makes pipeline scripts shorter and cleaner.                   | Encourages unit testing and better structure.                        |

---

### ❌ Disadvantages

| Feature | `vars/` Disadvantages                                           | `src/` Disadvantages                                                 |
|---------|----------------------------------------------------------------|----------------------------------------------------------------------|
| Scalability | Not ideal for large or complex logic.                         | Requires more setup and understanding of Groovy/Java conventions.   |
| Testability | Harder to test functions written in `vars/`.                  | Needs more boilerplate to write classes and pass context (`steps`). |
| Namespace Pollution | All `vars/*.groovy` files become global — risk of naming conflicts. | Must explicitly import and construct classes (not plug-and-play).   |
| Encapsulation | Limited ability to hide or encapsulate logic.               | Slightly more verbose when calling utility functions.               |

---

## **Workflow**

### 🧱 Structure (Example for Jenkins Shared Library)
```
(root)
├── vars/
│   └── deployApp.groovy         # Entry points (exposed pipeline functions)
├── src/
│   └── org/
│       └── example/
│           └── Helper.groovy    # Supporting reusable classes and methods
├── resources/
│   └── config.yaml              # Any static config files
└── README.md
```

### ✔ Execution Flow
1. Jenkinsfile calls a method defined in `vars/`.
2. That method may internally use classes/methods in `src/`.
3. Output is returned to the pipeline.
4. Library version is defined in Jenkins pipeline `@Library('libname@version')`.

---

## **vars vs src – Key Differences**

| Feature      | `vars/`                              | `src/`                                      |
|--------------|--------------------------------------|---------------------------------------------|
| Purpose      | Entry points for pipelines           | Internal reusable logic                     |
| Accessibility| Auto-loaded by Jenkins               | Must be explicitly imported                 |
| Scope        | Groovy scripting                     | Fully qualified Java/Groovy classes         |
| Usage        | `deployApp()`                        | `new org.example.Helper().doSomething()`    |

---

## **Best Practices**

🔹 **Structure your library**:
   - Use `vars/` for exposed methods.
   - Use `src/` for helper classes and logic separation.
   - Document functions and inputs clearly.

🔹 **Version control**:
   - Tag releases (e.g., `v1.0.0`) for consistent use across Jenkinsfiles.

🔹 **Testing**:
   - Unit test `src/` classes (with tools like Spock or JUnit).
   - Lint Groovy or YAML files before merging.

🔹 **Isolation**:
   - Avoid tightly coupling shared libs to environment-specific values.

🔹 **Naming conventions**:
   - Use clear, consistent naming for functions, classes, and variables.

🔹 **Keep secrets out**:
   - Never store credentials or tokens in the shared library repo.

---

## 📝 Conclusion

Shared libraries are essential for scaling Jenkins pipelines with clean, maintainable, and standardized code. Using both vars and src correctly helps separate simple steps from reusable logic, making your CI/CD process more efficient and robust.

---

## 📇 Contacts

| Name | Email Address |
| --- | --- |
| Shivani Narula | shivani.narula.snaatak@mygurukulam.co |

---

## 📘 Reference Table

| Links                                                                                                                             | Descriptions                          |
|-----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| https://www.jenkins.io/doc/book/pipeline/shared-libraries/                                                  | Jenkins official shared library docs |
| https://techforyou.medium.com/shared-libraries-in-jenkins-pipeline-a-comprehensive-guide-with-examples-83ddf0eec46e             | Shared Libraries tutorial and guide  |

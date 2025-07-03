
# Terraform CI Shared Library Documentation

<div align="center">
  <img src="https://github.com/user-attachments/assets/1e55f580-7c77-4a28-ac71-2c3034cb0df6" alt="Terraform CI Flow" width="300" height="200">
</div>

---

## Author Information

| Created | Version | Last Modified | Author | Comment | Reviewer |
| --- | --- | --- | --- | --- | --- |
| 02-07-2025 | V1 |     | Shivani Narula | Internal Review | Komal |

---

## Table of Contents

1. [What is the Terraform CI Shared Library?](#what-is-the-terraform-ci-shared-library)
2. [Why Use a Shared Library for Terraform CI?](#why-use-a-shared-library-for-terraform-ci)
3. [Prerequisites](#prerequisites)
4. [Architecture Diagram](#architecture-diagram)
5. [Key Features](#key-features)
6. [Functions Supported](#functions-supported)
7. [Jenkins Usage Example](#jenkins-usage-example)
8. [Inputs and Outputs](#inputs-and-outputs)  
   - [Inputs](#inputs)  
   - [Outputs](#outputs)
9. [Use Cases](#use-cases)
10. [Real-World Scenario](#real-world-scenario)
11. [Conclusion](#conclusion)
12. [Contacts](#contacts)
13. [Reference Table](#reference-table)

---

### What is the Terraform CI Shared Library?

The Terraform CI Shared Library is a **Jenkins pipeline utility** designed to abstract and automate the **validation (plan)** and **teardown (validate)** of Terraform-based infrastructure using consistent, modular, and secure practices. It simplifies repetitive tasks and provides a unified structure to manage Terraform workflows across multiple microservices and environments (Dev, QA, etc.).

---

### Why Use a Shared Library for Terraform CI?

- **Consistency** across all CI/CD pipelines using Terraform  
- **Modular design** for easy maintenance and scaling  
- **Reduced code duplication** across Jenkinsfiles  
- **Environment-driven workflows** (e.g., different configs for Dev and QA)  
- **Secure handling** of credentials using Jenkins secrets  

---

### Prerequisites

- Jenkins agent with **Terraform CLI installed**
- Terraform modules stored in Git repo using structure like:
  ```
  terraform/
  └── env/
      ├── dev/
      │   └── <module>/
      └── qa/
          └── <module>/
  ```
- Valid backend configuration (e.g., `backend.tf` with remote state like AWS S3)
- Jenkins secret credential configured (e.g., `aws-central-account-creds`)

---

### Architecture Diagram

![Terraform Shared Library Architecture](https://www.padok.fr/hubfs/blog-import/images/terraform-cicd.png)

Flow Summary:

- Developer pushes code to Git  
- Jenkins picks the change and invokes the shared library  
- The library:  
  - Loads credentials  
  - Initializes Terraform backend  
  - Plans and applies (or validates) infra using provided variables  
- Changes are applied to the correct environment (Dev/QA)  

---

### Key Features

| **Feature**                | **Description**                                                                 |
|----------------------------|---------------------------------------------------------------------------------|
| **Reusable Library**        | Centralized logic for all Terraform pipelines                                 |
| **Supports Plan/Validate** | Easily switch between `terraform plan` and `validate`                         |
| **Parameter-Driven**       | Fully dynamic via inputs like environment, module path, and tfvars            |
| **Credential Injection**   | Secure use of cloud provider credentials using Jenkins secrets                 |
| **Environment Isolation**  | Separate workflows for Dev, QA, and other environments                        |
| **Logs & Error Handling**  | Built-in status visibility and error reporting                                |
| **Lightweight Integration**| Requires minimal changes in Jenkinsfile                                        |
| **Backend Support**        | Compatible with remote state backends (e.g., AWS S3, GCS, etc.)                |

---

### Functions Supported

| Function Name          | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `terraformPlan()`     | Runs `init`, `plan`, and `plan` for the specified module and tfvars        |
| `terraformValidate()`   | Executes `init` and `validate` to tear down infra                            |
| `withTerraformEnv()`   | Wraps setup: credentials, working dir, backend initialization, etc.         |

---

### Jenkins Usage Example

```groovy
@Library('terraform-ci-shared-library') _

pipeline {
    agent any

    parameters {
        choice(name: 'ACTION', choices: ['plan', 'validate'], description: 'Terraform action to perform')
        string(name: 'TF_DIR', defaultValue: 'env/dev/network-skeleton', description: 'Terraform module path')
    }

    environment {
        AWS_CRED_ID = 'aws-central-account-creds'
    }

    stages {
        stage('Validate Terraform Plan') {
            steps {
                script {
                    withTerraformEnv(dir: params.TF_DIR, credentialsId: env.AWS_CRED_ID) {
                        if (params.ACTION == 'plan') {
                            terraformPlan()
                        } else {
                            terraformValidate()
                        }
                    }
                }
            }
        }
    }
}
```

---

### Inputs and Outputs

#### Inputs

| Parameter       | Type   | Description                                                |
|----------------|--------|------------------------------------------------------------|
| `dir`          | String | Path to Terraform module (relative to root of repo)        |
| `varFile`      | String | Name of tfvars file to be used                             |
| `credentialsId`| String | Jenkins credential ID for cloud authentication             |

#### Outputs

| Output                  | Description                                                |
|-------------------------|------------------------------------------------------------|
| Terraform Plan/Apply Log| Execution result printed to Jenkins console                |
| Terraform State Update  | Infra changes reflected in remote state                    |
| Exit Status             | Success/failure code for each action                       |

---

### Use Cases

| **Use Case**              | **Description**                                                               |
|---------------------------|-------------------------------------------------------------------------------|
| **Dev Infra Deployment**  | Validate development infrastructure via parameterized pipelines       |
| **QA Infra Teardown**     | Perform QA Terraform validations after testing to save resources                     |
| **Dynamic Module CD**     | Reuse pipeline across multiple microservices with different Terraform modules|
| **Multi-Team CD**         | Allow teams to validate Terraform config independently with a shared, secure library      |

---

### Real-World Scenario

Your team manages 10 microservices across Dev and QA environments using Terraform.  
Each team maintains their own module directory, and you want a consistent way to plan/validate infra from Jenkins.

Instead of writing a new Jenkinsfile for each service, you:

- Use one **parameterized Jenkins pipeline**  
- Integrate the **shared CD library**  
- Pass `TF_DIR`, and `ACTION` as parameters  

This results in:

- **Reduced boilerplate**  
- **Team autonomy**  
- **Centralized control and security**

---

### Conclusion

The Terraform CI Shared Library offers a structured, secure, and scalable solution to manage infrastructure validations across environments. It encourages standardization, reduces duplication, and enables rapid onboarding for new modules and teams. With clear functions and a clean API, it fits seamlessly into modern DevOps CI/CD pipelines.

---

### Contacts

| Name | Email Address |
|------|----------------|
| Shivani Narula | shivani.narula.snaatak@mygurukulam.co |

---

### Reference Table

| Descriptions | Links |
|-------|--------------|
|  Terraform CLI Docs | [Visit](https://www.terraform.io/cli) |
| Jenkins Shared Library Docs | [Visit](https://www.jenkins.io/doc/book/pipeline/shared-libraries/) | 
| Terraform GitHub Repo | [Visit](https://github.com/hashicorp/terraform) |

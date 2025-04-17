# Jinja Templating in Ansible
---

<p align="center">
  <img src="https://cdn.hashnode.com/res/hashnode/image/upload/v1613279162379/B_neFB1GX.png" alt="Logrotate Logo" width="400"/>
</p>

---

## 👤 Author Information
| Created | Version | Author | Comment | Reviewer |
| --- | --- | --- | --- | --- |
| 17-04-2025 | V1.1 | Shivani Narula | Internal Review | Siddharth Pawar |

---

## 📚 Table of Contents
- [Introduction](#-introduction)
- [What is Jinja Templating?](#-what-is-jinja-templating)
- [Why Use Jinja in Ansible](#why-use-jinja-in-ansible)
- [Key Features](#-key-features)
- [Advantages](#-advantages)
- [Disadvantages](#️-disadvantages)
- [Use Case](#-use-case)
- [Example](#-example)
- [Conclusion](#-conclusion)

## 📘 Introduction
In Ansible, **Jinja templating** is used to dynamically generate configuration files, scripts, and commands by embedding variables and logic directly into text files. This is a powerful feature that enhances the flexibility and reusability of automation playbooks and roles.

---

## ❓ What is Jinja Templating?
**Jinja2** is a modern templating engine for Python, widely used in Ansible to render variables and logic inside files such as `.yml`, `.j2`, and configuration files.

**Jinja syntax allows the use of:**

- **Variables**: `{{ variable_name }}`
- **Filters**: `{{ variable | filter }}`
- **Conditionals**: `{% if condition %} ... {% endif %}`
- **Loops**: `{% for item in list %} ... {% endfor %}`

---

### ❓**Why Use Jinja in Ansible?**
Jinja templating empowers Ansible to be dynamic, reusable, and adaptable to diverse environments.

> - **⚙️ Dynamic Configurations**: Templates like `nginx.conf`, `prometheus.yml`, and more can be generated with context-aware values.
> - **📦 Host-Specific Variables**: Supports inventory-based customization.
> - **🔁 Reusability**: A single template can serve multiple environments.
> - **🧹 Less Redundancy**: Minimizes hardcoding and duplication in playbooks.
> - **💡 Smarter Logic**: Add conditionals and loops directly in templates.

---

## 🔑 Key Features

| Feature               | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| Simple Syntax         | Easy to learn and read                                                      |
| Pythonic Expressions  | Offers a subset of Python-like logic                                        |
| Filters & Tests       | Modify output or validate data                                              |
| Inheritance & Includes| Supports modular templates and shared structures                            |
| Safe Rendering        | Prevents execution of unsafe code                                           |

---

## ✅ Advantages
- Enhances modularity and reusability
- Makes playbooks environment agnostic
- Supports logic-based rendering (e.g., conditionally add config blocks)
- Reduces manual edits across environments or hosts

---

## ⚠️ Disadvantages
- **Debugging complexity**: Errors in templates may be hard to trace
- **Learning curve**: Non-developers may find logic-heavy templates hard to follow
- **Overuse**: Can lead to difficult-to-maintain templates

---

## 💡 Use Case
**Generating different `nginx.conf` files** for dev, staging, and prod environments dynamically using the same template but different variables.

---

## 📄 Example

### Template: `nginx.conf.j2`
```jinja
server {
    listen 80;
    server_name {{ server_name }};

    location / {
        proxy_pass http://{{ backend }};
    }

    {% if enable_ssl %}
    listen 443 ssl;
    ssl_certificate {{ ssl_cert }};
    ssl_certificate_key {{ ssl_key }};
    {% endif %}
}
```

### Variables File: `group_vars/prod.yml`
```yaml
server_name: example.com
backend: 127.0.0.1:8080
enable_ssl: true
ssl_cert: /etc/ssl/certs/example.crt
ssl_key: /etc/ssl/private/example.key
```

### Rendered Output
```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://127.0.0.1:8080;
    }

    listen 443 ssl;
    ssl_certificate /etc/ssl/certs/example.crt;
    ssl_certificate_key /etc/ssl/private/example.key;
}
```

---

## 🧾 Conclusion
Jinja templating is a vital part of Ansible automation, enabling dynamic content generation, better reusability, and more efficient configuration management. When used thoughtfully, it can significantly reduce manual errors and improve infrastructure consistency.

---

## 📇 Contacts

| Name | Email Address |
| --- | --- |
| Shivani Narula | shivani.narula.snaatak@mygurukulam.co |

---

## 📘 References

| Links                                                                                                                             | Descriptions                          |
|-----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_templating.html                                                  | Ansible Docs - Templating             |
| https://blog.knoldus.com/deploying-custom-files-with-ansible-jinja2-templates/                                                    | Deploying Custom Files with Jinja2    |

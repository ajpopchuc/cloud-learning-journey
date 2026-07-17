# Ajpop's Cloud Learning Journey
Welcome! This repository serves as my professional portfolio, where I document my hands-on projects, technical labs, and architectures as I progress toward becoming a Cloud Architect. Here, you will find my journey through cloud fundamentals, core services, and advanced enterprise infrastructures.

## Core Concepts & Key Learnings 💡

### 🌐 Cloud & Operating System Fundamentals

#### 1. AWS Networking & CIDR Subnetting
When designing a Virtual Private Cloud (VPC), a Cloud Architect must account for the fact that **AWS reserves 5 IP addresses** in every subnet for internal management. Neglecting this can lead to running out of assignable IPs as the infrastructure scales.

*   **`.0` (First IP):** Network address (identifies the subnet).
*   **`.1`:** VPC Router (default gateway).
*   **`.2`:** AWS DNS Server.
*   **`.3`:** Reserved by AWS for future use.
*   **`.255` (Last IP):** Network broadcast address (AWS reserves this, as it does not support traditional broadcast).

> 💡 **In Practice:** If you provision a `/28` subnet (16 total IPs), you only have **11 usable IPs** for your cloud resources.

---

#### 2. Linux Permissions & SSH Key Hardening
To establish a secure remote connection to cloud servers (such as EC2 instances), we rely on SSH keys. Linux strictly enforces security policies; if a private key file is too widely accessible, the SSH client will reject the connection for being insecure.

We use the command `chmod 400 <key-name>.pem` to harden the file. In Linux, permissions are managed across **three distinct groups** (User/Owner, Group, and Others), each evaluated in octal format:
*   **The first digit `4` (Read-only):** Grants read permissions exclusively to the owner, allowing you to use the key.
*   **The second and third digits `0` (No access):** Strips all read, write, and execute permissions for both the group and others.
*   **Write Protection:** By withholding write permissions (`2`) even from the owner, we prevent accidental modification or corruption of the key file.

---

## Completed Labs

| Status | Lab | Description | Link |
| :---: | :--- | :--- | :--- |
| ✅ | [AWS Fundamentals](https://github.com) | Initial account setup, IAM configuration, and billing budgets. | [View Repo](https://github.com) |
| 🔄 | AWS Compute & Networking | Deploying EC2 instances within a custom VPC. | *Coming Soon* |

## Enterprise Capstone Project
*Space reserved for the final enterprise-grade infrastructure project.*

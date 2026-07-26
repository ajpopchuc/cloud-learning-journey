# 🌐 Module 02: AWS VPC Design and Implementation

## 📌 Project Overview
In this hands-on lab, I built a custom isolated virtual network (**Virtual Private Cloud - VPC**) from scratch in AWS. I applied cloud architecture best practices by segmenting public and private traffic, configuring custom route tables, and enabling secure outbound internet access using a NAT Gateway.

---

## 📐 Network Architecture

The resulting resource map illustrates the connectivity between subreds, route tables, and gateway components:

![VPC Resource Map](img/04-resource-map.png)

---

## 🧠 Key Architectural Concepts

* **Primary CIDR Block:** `10.0.0.0/16` (65,536 available IP addresses).
* **AWS Reserved IPs:** AWS reserves **5 IP addresses** in every subnet for internal networking purposes (Network, Gateway, DNS, Future Use, and Broadcast).
* **Public Subnet:** Associated with a route table directing internet-bound traffic to the **Internet Gateway (IGW)** (`0.0.0.0/0 -> IGW`).
* **Private Subnet:** Isolated from inbound internet connections. Uses a **NAT Gateway** residing in the public subnet for outbound requests.

---

## 🛠️ Step-by-Step Implementation

### 1. VPC Creation
* **Name:** `my-vpc-lab`
* **IPv4 CIDR Block:** `10.0.0.0/16`
* **Tenancy:** Default

![VPC Creation](img/01-vpc-created.png)

---

### 2. Subnet Allocation
Divided the primary CIDR block across Availability Zone `us-east-2a`:

| Subnet Name | CIDR Block | Total IPs | Usable IPs | Type |
| :--- | :--- | :--- | :--- | :--- |
| `my-subnet-public-1` | `10.0.1.0/24` | 256 | 251 | Public |
| `my-subnet-private-1` | `10.0.2.0/24` | 256 | 251 | Private |

![Subnets List](img/02-subnets.png)

---

### 3. Internet Gateway & Public Routing
1. Created and attached the Internet Gateway `my-igw-1-lab` to `my-vpc-lab`.
2. Created the custom route table `rtb-publica-1-lab`.
3. Added a default route: `0.0.0.0/0` $\rightarrow$ `my-igw-1-lab`.
4. Associated `my-subnet-public-1` with this route table.

![Internet Gateway](img/03-internet-gateway.png)

---

### 4. Secure Outbound Traffic via NAT Gateway
1. Deployed a **NAT Gateway** (`nat-gateway-1-lab`) inside the **public subnet** (`my-subnet-public-1`).
2. Allocated a static **Elastic IP (EIP)** to the NAT Gateway.
3. Created the private route table `rtb-privada-1-lab` with the route `0.0.0.0/0` $\rightarrow$ `nat-gateway-1-lab`.
4. Associated `my-subnet-private-1` with this route table.

---

## 🧹 Resource Cleanup (Cost Optimization)
To avoid charges for hourly-billed resources (NAT Gateway and Elastic IP), resources were deleted in reverse dependency order:

1. 🗑️ Delete NAT Gateway.
2. 📍 Release Elastic IP address.
3. 🌐 Detach and delete Internet Gateway.
4. 🏢 Delete VPC (automatically cleans up associated subnets and route tables).

---
*Project completed as part of preparation for the AWS Certified Solutions Architect - Associate (SAA-C03) exam.*
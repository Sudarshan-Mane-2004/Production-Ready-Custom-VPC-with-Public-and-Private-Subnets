# 🚀 Secure VPC Architecture

## Production-Ready Custom VPC with Public and Private Subnets

---

## 📌 Project Overview

This project demonstrates how to design and implement a **secure, production-ready AWS network architecture** using a custom VPC.

In real-world cloud environments, not all servers should be exposed to the internet. This architecture separates public-facing resources from private internal resources using proper routing and gateways.

This project simulates how companies securely deploy applications in AWS.

---

## 🎯 Aim

Build a secure AWS network that:

* Separates public and private resources
* Allows controlled internet access
* Protects backend servers
* Follows AWS best practices
* Mimics real production architecture

---

## 🧠 Architecture Flow

**Internet → Internet Gateway → Public Subnet → NAT Gateway → Private Subnet**

### Flow Explanation

1. Public EC2 communicates directly with the Internet via Internet Gateway
2. Private EC2 does NOT have direct internet access
3. Private EC2 uses NAT Gateway for outbound internet
4. Route tables control traffic flow
5. Architecture remains secure and scalable

---

# 🏗️ Overall Architecture Diagram

<img width="1536" height="1024" alt="Custom VPC" src="https://github.com/user-attachments/assets/cd7234e7-d50a-4f76-ac17-e28e1d0da475" />

---

# 🛠️ Implementation Steps

---

## ✅ Step 1: Create Custom VPC

### 🔹 What We Did

Created a custom VPC with CIDR block.

### 🔹 Configuration

* Name: `Prod-VPC`
* CIDR: `10.0.0.0/16`

### 🔹 Why We Used It

The VPC is the **isolated network boundary** in AWS.
It allows us to fully control IP ranges, routing, and security.

---

<img width="1915" height="1076" alt="Screenshot 2026-02-27 231518" src="https://github.com/user-attachments/assets/3c4f6b68-f3f4-4f5b-88e9-7196c4424f9e" />


---

## ✅ Step 2: Create Public Subnet

### 🔹 What We Did

Created subnet for internet-facing resources.

### 🔹 Configuration

* Name: `Public-Subnet-A`
* CIDR: `10.0.1.0/24`

### 🔹 Why We Used It

Public subnet is required for:

* Bastion host
* NAT Gateway
* Load balancers
* Public web servers

Resources here can reach the internet directly.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 231621" src="https://github.com/user-attachments/assets/67a43018-a135-4a91-8766-395af7bd4fd0" />


---

## ✅ Step 3: Create Private Subnet

### 🔹 What We Did

Created isolated subnet for secure resources.

### 🔹 Configuration

* Name: `Private-Subnet-A`
* CIDR: `10.0.2.0/24`

### 🔹 Why We Used It

Private subnet protects sensitive resources like:

* Application servers
* Databases
* Backend services

These resources are **not exposed to the internet**.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 231649" src="https://github.com/user-attachments/assets/08ea646c-1a3f-46ef-9651-4bdd41990e6d" />


---

## ✅ Step 4: Attach Internet Gateway

### 🔹 What We Did

Created and attached Internet Gateway to VPC.

### 🔹 Why We Used It

Internet Gateway enables:

* Public subnet internet access
* Incoming/outgoing internet traffic

Without IGW, nothing in the VPC can reach the internet.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 231748" src="https://github.com/user-attachments/assets/744b24ae-964d-4d63-b917-5f2a499056c1" />


---

## ✅ Step 5: Create NAT Gateway (Public Subnet)

### 🔹 What We Did

Created NAT Gateway inside public subnet.

### 🔹 Why We Used It

NAT Gateway allows:

* Private EC2 → internet access
* Blocks inbound internet to private EC2
* Maintains security

This is **critical in production environments**.

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 231826" src="https://github.com/user-attachments/assets/d5491215-ac3d-46d0-b319-161cc2bc85b6" />


---

## ✅ Step 6: Configure Route Tables

---

### 🔹 Public Route Table

**Route:**

```
0.0.0.0/0 → Internet Gateway
```

### Why Used

Allows public subnet resources to access the internet directly.

---

---

### 🔹 Private Route Table

**Route:**

```
0.0.0.0/0 → NAT Gateway
```

### Why Used

Allows private subnet resources to:

* Access internet outbound
* Remain unreachable from internet inbound

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 231935" src="https://github.com/user-attachments/assets/45aee132-0ea3-4616-9e9d-62f05e0f86ee" />


---

## ✅ Step 7: Launch EC2 Instances

---

### 🌐 Public EC2

**Configuration**

* Subnet: Public
* Public IP: Enabled

**Purpose**

* Bastion host
* Public access point

---

---

### 🔒 Private EC2

**Configuration**

* Subnet: Private
* Public IP: Disabled

**Purpose**

* Secure backend server
* Protected from internet

---

<img width="1919" height="1079" alt="Screenshot 2026-02-27 232030" src="https://github.com/user-attachments/assets/f62b8dd7-f6e5-49cf-9eb0-38eda10d3b3f" />


---

---

## ✅ Step 8: Bastion Host Access Flow

Private EC2 is accessed securely via public EC2.

**Flow:**

Laptop → Public EC2 → Private EC2

---

<img width="1536" height="1024" alt="ChatGPT Image Feb 27, 2026, 11_10_26 PM" src="https://github.com/user-attachments/assets/9e492b26-eb53-4d11-96af-6c9e3fc287bc" />


---

---

## 🧪 Testing Performed

### ✅ Public EC2 Test

```bash
ping google.com
```

✔ Direct internet access confirmed

---

### ✅ Private EC2 Test

```bash
ping google.com
```

✔ Works via NAT Gateway
✔ No public IP present

---
---

---

# 🔐 Security Best Practices Demonstrated

* Network isolation
* Private subnet protection
* Controlled outbound internet
* Least privilege networking
* Production VPC design

---

# 🎓 Key Learnings

From this project I learned:

* VPC architecture design
* Public vs private subnet behavior
* Internet Gateway vs NAT Gateway
* Route table traffic control
* Secure EC2 deployment
* Bastion host access pattern
* Real-world AWS networking

---

# 🏁 Final Aim (What This Architecture Achieves)

This architecture ensures:

* High network security
* Controlled internet exposure
* Safe backend deployment
* Production-ready cloud network
* Scalable and maintainable infrastructure

---

# ✅ Conclusion

Through this project, I successfully built a **secure, production-style VPC architecture** that follows AWS best practices.

The implementation demonstrates how modern cloud environments protect private resources while still allowing necessary internet access through controlled mechanisms like NAT Gateway and Bastion Host.

This project strengthened my practical understanding of AWS networking and real-world cloud security design.

---

## 👨‍💻 Author

**Sudarshan Mane**
Aspiring AWS & DevOps Engineer
Focused on building secure and scalable cloud infrastructure.


---


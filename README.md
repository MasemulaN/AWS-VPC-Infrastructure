# AWS-VPC-Infrastructure
# ☁️ Design and Deploy a Secure AWS VPC Infrastructure

> **A secure AWS networking project demonstrating VPC design, subnet isolation, secure remote access using a Bastion Host, and outbound internet connectivity through a NAT Gateway.**

---

## 📖 Project Overview

This project demonstrates the deployment of a secure AWS Virtual Private Cloud (VPC) using AWS networking services. The infrastructure follows AWS security best practices by separating resources into **public** and **private** subnets within a **single Availability Zone**, ensuring that private resources remain inaccessible from the public internet while still allowing secure outbound internet access.

The project was completed using the **AWS Free Tier** and serves as a practical implementation of core AWS networking concepts.

---

## 🎯 Project Objectives

- Design a custom VPC
- Deploy public and private subnets
- Configure an Internet Gateway
- Deploy a NAT Gateway with an Elastic IP
- Configure public and private Route Tables
- Secure the network using Security Groups and Network ACLs (NACLs)
- Launch EC2 instances in both subnets
- Access the private EC2 instance through a Bastion Host
- Verify secure internet connectivity from the private subnet

---

## 🏗️ Solution Architecture

The deployed infrastructure consists of:

- **VPC:** `10.0.0.0/16`
- **Public Subnet:** `10.0.25.0/24`
- **Private Subnet:** `10.0.50.0/24`
- Internet Gateway
- NAT Gateway
- Elastic IP
- Public Route Table
- Private Route Table
- Public & Private Network ACLs
- Public & Private Security Groups
- Bastion Host (Public EC2)
- Private EC2 Instance

📌 **Architecture Diagram**

<img width="1021" height="691" alt="NM-AWS-Diagram drawio" src="https://github.com/user-attachments/assets/ecfc1d1f-c480-496f-900f-49115ff4ec1a" />


---

## 🌐 Network Flow

```text
Internet
    │
Internet Gateway
    │
Public Route Table
    │
Public Subnet
    │
Bastion Host (EC2)
    │
SSH
    │
Private EC2 Instance
    │
Private Route Table
    │
NAT Gateway
    │
Internet Gateway
    │
Internet
```

---

## 🔒 Security Implementation

### 🛡️ Security Groups

### Public EC2 (NM-Bastion)

- SSH (22) from the Internet
- Allow all outbound traffic
<img width="1600" height="900" alt="23-public-sg" src="https://github.com/user-attachments/assets/1fd422eb-a989-4201-80ec-0ebef1486bc4" />


### Private EC2 (NM-Private-EC2)

- SSH (22) only from the Bastion Host Security Group
- Allow all outbound traffic
<img width="1599" height="900" alt="22-private-sg" src="https://github.com/user-attachments/assets/71c36ff6-238e-4d29-b25f-26a4155c0836" />

---

### 🚧 Network ACLs

### Public NACL (NM-Public-NACL)

#### Inbound

- SSH (22)
- HTTP (80)
- HTTPS (443)
- Ephemeral Ports (1024–65535)
  <img width="1600" height="900" alt="12-public-nacl-inbound-config" src="https://github.com/user-attachments/assets/e88f7d6f-4f59-4f4e-be84-8b8c1e8bb231" />


#### Outbound

- Allow All
  <img width="1600" height="900" alt="13-public-nacl-outbound-config" src="https://github.com/user-attachments/assets/d2e1fe74-f59b-4622-9748-97808f964608" />

---

### Private NACL (NM-Private-NACL)

#### Inbound

- SSH (22) from the Public Subnet CIDR
- Ephemeral Ports
  <img width="1594" height="900" alt="14-private-nacl-inbound-config" src="https://github.com/user-attachments/assets/4a21fa1f-96ab-46b9-b86b-99c9ae87f780" />

#### Outbound

- HTTP (80)
- HTTPS (443)
- Ephemeral Ports
  <img width="1918" height="1078" alt="27-private-nacl-outbound-rules" src="https://github.com/user-attachments/assets/6e812faa-edb7-418e-ac15-041ce2ecca37" />

---

## ✅ Infrastructure Verification

The following screenshots are included in the repository as proof of deployment:

- ✅ Custom VPC (`10.0.0.0/16`)
  <img width="1600" height="900" alt="24-vpc-overview" src="https://github.com/user-attachments/assets/7d5775e4-a23d-4f86-8a0b-5be2003d8098" />


- ✅ Public & Private Subnets
  <img width="1598" height="900" alt="02-public-subnet" src="https://github.com/user-attachments/assets/6403c8ee-1f70-4205-b24f-5667fbb05cda" />
  <img width="1600" height="900" alt="03-private-subnet" src="https://github.com/user-attachments/assets/7da0aa6b-88c0-46f4-8463-5ad497f0c87b" />
  
- ✅ Route Table Associations
  <img width="1600" height="900" alt="07-public-rt-subnet-association" src="https://github.com/user-attachments/assets/bd466004-e0a9-4de5-9c81-b5c6ecf0b5f9" />
  <img width="1600" height="900" alt="08-private-rt-subnet-association" src="https://github.com/user-attachments/assets/3eaa0cda-6349-45cd-9ae2-a9de6405ba28" />

- ✅ Internet Gateway
  <img width="1600" height="900" alt="04-igw-attached" src="https://github.com/user-attachments/assets/161eff78-158a-4f11-8e02-6f476dc921d7" />

- ✅ NAT Gateway (Available)
  <img width="1600" height="900" alt="16-nat-gateway-created" src="https://github.com/user-attachments/assets/17067603-c808-4534-b37d-11764df20e9a" />

- ✅ Network ACL Configuration
  <img width="1599" height="900" alt="25-NACL-OVERVIEW" src="https://github.com/user-attachments/assets/0b8f6767-62d8-4447-aac5-2edaa6c89947" />

- ✅ Security Group Configuration
  <img width="1600" height="900" alt="21-sg-overview" src="https://github.com/user-attachments/assets/e2d0f7ae-e0a5-4ba6-954f-e4368692374a" />

- ✅ Bastion Host AND Private EC2 Deployment
- <img width="1600" height="900" alt="20-instances-overview" src="https://github.com/user-attachments/assets/bbbd972a-8717-4289-8e92-cfcd922f0808" />

- ✅ Successful SSH Connection and Private EC2 Internet Connectivity
  <img width="1918" height="1078" alt="25-bastion-to-private-ec2-ssh-success" src="https://github.com/user-attachments/assets/49be3da7-6224-43b4-b5dc-db89ed02e889" />



---

## 🔍 Connectivity Verification

### ✔️ How the Private EC2 Instance Reaches the Internet

The Private EC2 instance does **not** have a public IP address and therefore cannot communicate directly with the internet.

When outbound internet access is required (for example, installing software updates), the traffic follows this path:

```text
Private EC2
      │
Private Route Table
      │
NAT Gateway
      │
Internet Gateway
      │
Internet
```

The Private Route Table forwards all outbound traffic (`0.0.0.0/0`) to the NAT Gateway. The NAT Gateway then translates the private IP address to its associated Elastic IP before sending the request through the Internet Gateway.

Internet connectivity was verified using:

```bash
curl https://checkip.amazonaws.com
```

The command returned the NAT Gateway's public IP address, confirming successful outbound internet access.

---

### 🔐 Why the Private EC2 Cannot Be Accessed from the Internet

The Private EC2 instance is intentionally isolated from the public internet because:

- It is deployed inside a **Private Subnet**.
- It **does not have a Public IP Address**.
- The Private Route Table **does not contain a route to the Internet Gateway**.
- Inbound SSH access is restricted to the **Bastion Host Security Group**.
- Network ACLs further restrict unwanted inbound traffic.

As a result, external users cannot directly establish a connection to the Private EC2 instance. Administrative access is only possible by first connecting to the Bastion Host and then securely SSH'ing into the private instance.

---

## 📁 Project Structure

```text
aws-secure-vpc-infrastructure/
│
├── README.md
│
├── architecture/
│   ├── aws-architecture-diagram.png
│
├── screenshots/
│   ├── 01-vpc-created.png
│   ├── 02-subnets-created.png
│   ├── 03-internet-gateway.png
│   ├── 04-route-tables.png
│   ├── 05-network-acls.png
│   ├── 06-security-groups.png
│   ├── 07-nat-gateway.png
│   ├── 08-ec2-instances.png
│   ├── 09-bastion-host-ssh.png
│   ├── 10-bastion-to-private-ssh.png
│   └── 11-private-instance-internet-access.png
└── 
```

---

## 🛠️ AWS Services Used

- Amazon VPC
- Amazon EC2
- Internet Gateway
- NAT Gateway
- Elastic IP
- Route Tables
- Network ACLs
- Security Groups

---

## 📚 Key Learning Outcomes

This project strengthened my understanding of:

- AWS VPC design principles
- Public and private subnet architecture
- Secure network segmentation
- Route table configuration
- Internet Gateway and NAT Gateway functionality
- Security Groups vs Network ACLs
- Secure administration using a Bastion Host
- AWS networking troubleshooting
- Technical documentation and infrastructure validation

---

## 👩‍💻 Author

**Noluthando Masemula**

Software Developer transitioning into **Cloud Computing and DevOps**, building hands-on AWS infrastructure projects to strengthen practical cloud engineering skills.

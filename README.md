# ☁️ Creating a Highly Available Environment – AWS Academy Cloud Architecting

This project demonstrates the design and deployment of a **highly available (HA) web application architecture** on **Amazon Web Services (AWS)**.  
It is part of the **AWS Academy Cloud Architecting Capstone** series and showcases the implementation of cloud reliability, scalability, and fault tolerance principles.

---

## 🧭 Overview

The goal of this project is to transform a **single-instance application** into a **multi-AZ, fault-tolerant infrastructure** using AWS managed services.

The final architecture eliminates single points of failure and ensures continuous availability of resources, even if one Availability Zone (AZ) or component fails.

---

## ⚙️ Architecture Components

| AWS Service | Description | Role in High Availability |
|--------------|-------------|----------------------------|
| **Amazon VPC** | Isolated virtual network with public and private subnets. | Enables multi-AZ deployment and secure traffic routing. |
| **EC2 Instances** | Hosts the web application. | Deployed across multiple AZs for redundancy. |
| **Elastic Load Balancer (ALB)** | Distributes incoming traffic across healthy instances. | Ensures seamless failover and load balancing. |
| **Auto Scaling Group (ASG)** | Automatically adjusts instance capacity. | Maintains system reliability and performance. |
| **Amazon RDS** | Managed relational database. | Configured for Multi-AZ replication to prevent data loss. |
| **NAT Gateway** | Enables outbound internet access for private instances. | Supports AZ redundancy when deployed in pairs. |
| **Security Groups** | Act as virtual firewalls for traffic control. | Enforces least privilege and tier isolation. |
| **CloudWatch** | Monitors system metrics and health. | Automates recovery actions via alarms. |

---

## 🧩 Final Architecture

- Multi-AZ **VPC** with public and private subnets  
- **Elastic Load Balancer** distributing traffic across AZs  
- **Auto Scaling Group** maintaining minimum capacity of two instances  
- **RDS Multi-AZ** database deployment  
- **NAT Gateways** for outbound traffic redundancy  
- **CloudWatch monitoring** and alarms for health checks  

---

## 🧰 Tools and Technologies

- AWS EC2  
- AWS Elastic Load Balancer (ALB)  
- AWS Auto Scaling  
- AWS RDS (MySQL)  
- AWS CloudWatch  
- AWS VPC  
- AWS IAM  

---

## 🧱 Architecture Diagram (Conceptual)

```text
                  ┌────────────────────────────┐
                  │   Elastic Load Balancer    │
                  └────────────┬───────────────┘
                               │
             ┌─────────────────┴──────────────────┐
             │                                    │
      ┌──────────────┐                    ┌──────────────┐
      │ EC2 Instance │                    │ EC2 Instance │
      │ (AZ-1)       │                    │ (AZ-2)       │
      └──────┬───────┘                    └──────┬───────┘
             │                                    │
             └────────────┬────────────┬──────────┘
                          │            │
                  ┌───────▼──────┐ ┌───▼──────────┐
                  │   RDS (AZ-1) │ │ RDS (Standby)│
                  └──────────────┘ └───────────────┘

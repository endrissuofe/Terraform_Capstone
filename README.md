## Terraform Capstone Project: Automated WordPress Deployment on AWS

## 📘 Project Overview
This project demonstrates how to automate the deployment of a **scalable, secure, and cost-effective WordPress website** on AWS using **Terraform**.  
It was designed for **DigitalBoost**, a digital marketing agency that wants to host WordPress for client sites using AWS infrastructure managed as code.

---

## 🧱 Architecture Summary

### Components:
1. **VPC Setup** – Creates an isolated network for all resources.  
2. **Public and Private Subnets with NAT Gateway** – Ensures secure access to the internet for private resources.  
3. **RDS (MySQL)** – Hosts the WordPress database securely in private subnets.  
4. **EFS (Elastic File System)** – Provides shared file storage for WordPress across multiple instances.  
5. **Application Load Balancer (ALB)** – Distributes traffic for high availability.  
6. **Auto Scaling Group (ASG)** – Automatically scales EC2 instances based on traffic.  

---

## 🖼️ Architecture Diagram
![architecture](img/architecture.png)

---

## ⚙️ Prerequisites

- AWS Account (Free Tier compatible)
- Terraform v1.5+ installed  
- AWS CLI configured with proper IAM permissions  
- SSH key pair for EC2 access  
- S3 bucket for Terraform state (optional but recommended)

---

## 🚀 Project Deployment Steps

### 1️⃣ VPC Setup
**Objective:** Create a dedicated Virtual Private Cloud for isolation and security.  
**Terraform Tasks:**
- Define CIDR blocks.  
- Create Internet Gateway, route tables, and associations.  

```bash
terraform apply -target=module.vpc
````

📸 *Screenshot:*
![vpc](img/vpc.png)

---

### 2️⃣ Public and Private Subnets with NAT Gateway

**Objective:** Separate web and database tiers; provide controlled internet access via NAT Gateway.
**Terraform Tasks:**

* Create public and private subnets across availability zones.
* Attach Elastic IP and configure NAT Gateway for outbound traffic.

📸 *Screenshot:*
![nat-gateway](img/nat-gateway.png)

---

### 3️⃣ RDS Setup (MySQL)

**Objective:** Deploy a managed MySQL instance for WordPress data storage.
**Terraform Tasks:**

* Define DB subnet group and RDS instance.
* Restrict inbound access to web tier only via Security Groups.

📸 *Screenshot:*
![rds](img/rds.png)

---

### 4️⃣ EFS Setup

**Objective:** Provide shared file storage for EC2 instances running WordPress.
**Terraform Tasks:**

* Create EFS and mount targets across subnets.
* Configure EC2 user data to mount EFS during instance boot.

📸 *Screenshot:*
![efs](img/efs.png)

---

### 5️⃣ Application Load Balancer

**Objective:** Ensure traffic distribution and fault tolerance.
**Terraform Tasks:**

* Create target group, listeners, and attach EC2 instances.
* Configure ALB security group to allow HTTP/HTTPS traffic.

📸 *Screenshot:*
![alb](img/alb.png)

---

### 6️⃣ Auto Scaling Group

**Objective:** Scale the application automatically based on load.
**Terraform Tasks:**

* Create Launch Template for WordPress EC2 instance.
* Configure scaling policies and CloudWatch alarms.

📸 *Screenshot:*
![asg](img/asg.png)

---

## 🔐 Security Considerations

* Private subnets for RDS and EFS.
* Least privilege security group rules.
* Restricted inbound SSH access.
* NAT Gateway used for outbound updates from private instances.
* IAM roles for EC2 to access S3, CloudWatch, and EFS.

---

## 🧩 Directory Structure

```
terraform-capstone/
├── main.tf
├── variables.tf
├── outputs.tf
├── modules/
│   ├── vpc/
│   ├── subnets/
│   ├── rds/
│   ├── efs/
│   ├── alb/
│   ├── asg/
│   └── security/
└── img/
    ├── architecture.png
    ├── vpc.png
    ├── nat-gateway.png
    ├── rds.png
    ├── efs.png
    ├── alb.png
    ├── asg.png
```

---

## 🧾 Terraform Commands

```bash
terraform init
terraform plan
terraform apply
```

To destroy all AWS resources (to avoid charges):

```bash
terraform destroy
```

📸 *Screenshot:*
![terraform-apply](img/terraform-apply.png)

---

## 🌐 Output

After successful deployment:

* Access WordPress via the **ALB DNS endpoint** shown in the Terraform outputs.
* Complete the WordPress installation in the browser.

📸 *Screenshot:*
![wordpress](img/wordpress.png)

---

## 🧹 Clean-Up

To avoid charges, always destroy your resources:

```bash
terraform destroy
```

Verify in AWS Console that no EC2, RDS, EFS, or NAT Gateway resources remain active.

---

## ✅ Summary

This project automated the setup of a **highly available WordPress site** using Terraform.
It demonstrates infrastructure-as-code best practices, modular design, and AWS scalability principles.

---

**Author:** Drix
**Role:** DevOps Engineer in training
**Platform:** AWS Free Tier + Terraform
```

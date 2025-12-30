# AWS Three Tier Web Architecture Workshop

## 📌 Description
This project is a **hands-on implementation of a Three-Tier Web Architecture on AWS**.  
The workshop walks through manually creating and configuring **network, security, compute, and database components** to build a **scalable, highly available, and secure architecture**.

The goal of this project is to understand how real-world applications are deployed in AWS using best practices.

---

## 🏗 Architecture Overview
![Architecture](https://raw.githubusercontent.com/username/repo/main/images/aws-3tier-architecture.png)


In this architecture:

- A **public-facing Application Load Balancer (ALB)** receives client traffic.
- The **Web Tier** consists of EC2 instances running **Nginx**, serving a **React.js frontend**.
- API requests from the web tier are forwarded to an **internal Application Load Balancer**.
- The **Application Tier** runs **Node.js** services behind the internal ALB.
- The application tier interacts with an **Amazon Aurora MySQL (Multi-AZ)** database.
- **Auto Scaling Groups**, **health checks**, and **load balancing** are used at each tier to ensure availability and scalability.

(Architecture diagram created using Draw.io)

---

## 🧠 Key AWS Services Used
- VPC
- EC2
- Application Load Balancer (ALB)
- Auto Scaling Groups
- IAM
- S3
- RDS (Aurora MySQL – Multi-AZ)
- Route 53
- CloudWatch
- SNS
- CloudTrail
- NAT Gateway
- Internet Gateway

---

## ⚙️ Project Algorithm / Steps

### Step 1: Download Code
- Download the web and app server code from GitHub to your local system.

---

### Step 2: Create S3 Buckets
- Create **one S3 bucket** to store web-server and app-server code.
- Upload code from local system to S3.
- Create **another S3 bucket** for **VPC Flow Logs**.

---

### Step 3: Create IAM Role
Attach the following policies:
- AmazonS3ReadOnlyAccess
- AmazonSSMManagedInstanceCore

---

### Step 4: Create Networking Components
- Create a **VPC**
- Create **public and private subnets**
- Attach **Internet Gateway**
- Create **NAT Gateway**
- Configure **Route Tables**
- Enable **auto-assign public IP** for web-tier public subnets
- Enable **VPC Flow Logs** and store logs in the S3 bucket

---

### Step 5: Create Security Groups
- **External-Load-Balancer-SG**  
  - HTTP (80) → `0.0.0.0/0`

- **Web-Tier-SG**  
  - HTTP (80) → External-ALB-SG

- **Internal-Load-Balancer-SG**  
  - HTTP (80) → Web-Tier-SG

- **App-Tier-SG**  
  - Port 4000 → Internal-ALB-SG

- **DB-Tier-SG**  
  - MySQL (3306) → App-Tier-SG

---

### Step 6: Create Database Layer
- Create **DB Subnet Group**
- Create **RDS Aurora MySQL (Multi-AZ)**
- Place RDS in the DB subnet group

---

### Step 7: Application Tier Setup
- Launch a **test App Server**
- Install required packages
- Test DB and internal connectivity
- Create **AMI**
- Create **Launch Template**
- Create **Target Group**
- Create **Internal Load Balancer**
- Create **Auto Scaling Group**
- Update `nginx.conf` with Internal ALB DNS
- Upload updated config to S3

---

### Step 8: Web Tier Setup
- Launch a **test Web Server**
- Install **Nginx and Node.js (React)**
- Test connectivity
- Create **AMI**
- Create **Launch Template**
- Create **Target Group**
- Create **External Load Balancer**
- Create **Auto Scaling Group**

---

### Step 9: Route 53 Configuration
- Add **External ALB DNS record** in Route 53 for the application domain

---

### Step 10: Monitoring & Alerts
- Create **CloudWatch alarms**
- Configure **SNS notifications**

---

### Step 11: Enable CloudTrail
- Enable CloudTrail for auditing and logging AWS API activity

---

## 🧹 Step 12: Cleanup (Delete Infrastructure)
To avoid unnecessary AWS charges:

1. Delete CloudFront distribution
2. Delete CloudWatch alarms
3. Delete Route 53 records
4. Delete Load Balancers, Target Groups, ASGs, Launch Templates
5. Delete Security Groups
6. Delete NAT Gateway (wait ~5 minutes)
7. Release Elastic IP
8. Delete VPC
9. Delete RDS instance and DB subnet group

---

## 📖 Workshop Instructions
Refer to: **AWS Three Tier Web Architecture Workshop**

---

## ✅ Outcome
By completing this project, you will gain hands-on experience in:
- Designing a real-world AWS architecture
- Implementing secure networking
- Using load balancers and auto scaling
- Deploying scalable web and application tiers
- Managing AWS resources efficiently

---

## 👤 Author
**Vipul Pandey**  
Cloud & Systems Engineer  


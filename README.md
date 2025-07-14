# AWS-Project-Scalable-Web-Application
AWS Project: Scalable Web Application with ALB, ASG, RDS, CloudWatch, and SNS.
# 🛠️ AWS Project: Scalable Web Application

## 📌 Project Overview

This project deploys a highly available and scalable web application architecture on AWS using EC2, Application Load Balancer (ALB), Auto Scaling Groups (ASG), and RDS. It also integrates monitoring and alerting using CloudWatch and SNS.

---

## ⚙️ Architecture Components

### 1. **Amazon EC2**
- Hosts the Apache web server
- User data bootstraps the server with an index page
- Deployed in multiple Availability Zones

### 2. **Auto Scaling Group (ASG)**
- Automatically scales EC2 instances based on CPU utilization
- Uses a Launch Template with a key pair for SSH access

### 3. **Application Load Balancer (ALB)**
- Distributes traffic to healthy EC2 instances
- Target group configured to listen on port 80

### 4. **Amazon RDS (Optional)**
- MySQL/PostgreSQL database engine
- Deployed in a DB Subnet Group across 2+ subnets
- Public access can be enabled for testing

### 5. **Amazon CloudWatch + SNS**
- Monitors EC2 metrics (like CPUUtilization)
- Sends email alerts via SNS topics

---

## 🚀 Deployment Instructions

### 🔸 EC2 + Apache Setup

1. Launch an EC2 instance or ASG with user data:
   ```bash
   # User data (Amazon Linux)
   sudo yum install -y httpd
   sudo systemctl start httpd
   sudo systemctl enable httpd
   echo "<h1>Deployed via Auto Scaling</h1>" > /var/www/html/index.html

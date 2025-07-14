# AWS-Project-Scalable-Web-Application
AWS Project: Scalable Web Application with ALB, ASG, RDS, CloudWatch, and SNS.
# 🛠️ AWS Project: Scalable Web Application


## 📸 Architecture Diagram
![ScreenRecording2025-07-14193138-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/29d80075-f577-485f-99f8-66692713f213)


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

### 4. ** Amazon RDS **
- MySQL/PostgreSQL database engine
- Deployed in a DB Subnet Group across 2+ subnets
- Public access can be enabled for testing

### 5. **Amazon CloudWatch + SNS**
- Monitors EC2 metrics (like CPUUtilization)
- Sends email alerts via SNS topics
  <img width="733" height="323" alt="image" src="https://github.com/user-attachments/assets/93616b38-0e40-44a1-b4ee-3479a156c6fc" />


---

## 🚀 Deployment Instructions

### 🔸 EC2 + Apache Setup

1. Launch an EC2 instance or ASG with user data:
   ```bash
   # User data (Amazon Linux)
   sudo yum install -y httpd
   sudo systemctl start httpd
   sudo systemctl enable httpd
   echo "<h1>Welcome to Manara SSA Project</h1>" > /var/www/html/index.html
Allow HTTP (port 80) in the instance security group.

🔸 Auto Scaling Group (ASG)
Create a Launch Template:

AMI: Amazon Linux 2

Instance type: t2.micro (Free Tier)

Key pair: Create or use existing

User data: Add Apache install script

Create an ASG:

Use launch template

Select 2+ subnets in different AZs

Attach to target group (created with ALB)

🔸 Application Load Balancer (ALB)
Create a Target Group:

Type: Instance

Protocol: HTTP (port 80)

Create the ALB:

Internet-facing

Attach it to at least 2 public subnets

Link the ALB to the previously created target group

Ensure subnet’s route table includes a route to the Internet Gateway

🔸 Amazon RDS (Optional)
Create RDS (MySQL/PostgreSQL):

Choose Free Tier eligible DB

Public access = Yes (for external access)

Subnet group = At least 2 subnets

Security group: Allow port 3306 from your EC2 security group

🔸 CloudWatch + SNS
1. Create SNS Topic
bash
Copy
Edit
aws sns create-topic --name vpc-monitoring-alerts
aws sns subscribe --topic-arn arn:aws:sns:REGION:ACCOUNT_ID:vpc-monitoring-alerts \
  --protocol email --notification-endpoint you@example.com
2. CloudWatch Alarm for EC2
Go to CloudWatch → Alarms → Create Alarm

Metric: EC2 → CPUUtilization

Condition: Greater than 70% for 1 datapoint within 5 min

Action: Send notification to vpc-monitoring-alerts topic


📍 Notes
Make sure the EC2 security group allows SSH (port 22) from your IP.

Public IP may be assigned via Elastic IP or automatically if enabled.

Use sudo systemctl status httpd to verify Apache is running.

📈 Monitoring and Cost Optimization
Enable Auto Scaling policies to minimize costs during low traffic

CloudWatch helps identify spikes in usage

SNS notifies you when thresholds are exceeded

Use Free Tier resources where possible (e.g., t2.micro, db.t3.micro)

## 🏁 Outputs
## ALB DNS: http://webapp-alb-1787114958.us-east-1.elb.amazonaws.com/
<img width="1196" height="385" alt="image" src="https://github.com/user-attachments/assets/bba61cd6-24db-41ac-8a84-00d4913696e5" />


EC2 Instances: auto-created by ASG

RDS Endpoint: Available in the RDS Console

✅ Learning Outcomes
Configure EC2 + Auto Scaling + Load Balancer

Use CloudWatch Alarms and SNS for monitoring

Launch and connect to an RDS instance

Deploy a complete, scalable web application on AWS

📧 Contact
For questions or contributions, please reach out to [mmazen.m23@gmail.com].

# Assignment 5 — Deploy a Highly Available Two-Tier Application on AWS (VPC + ALB + ASG + Multi-AZ RDS)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will design and deploy a highly available two-tier web application on AWS: highly available networking across two Availability Zones, an Application Load Balancer, an Auto Scaling Group for the web tier, and a private Multi-AZ RDS database. You must prove high availability with real failure tests.

---

# Task 1 — Create HA Networking (VPC + 4 Subnets + IGW + NAT + Route Tables)

## Goal

Build a VPC (10.0.0.0/16) with two public and two private subnets across two Availability Zones, an Internet Gateway, a NAT Gateway, and the matching public/private route tables.

### Evidence

#### Screenshot 1 — VPC details showing CIDR 10.0.0.0/16

![Screenshot 1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%201.png)

---

#### Screenshot 2 — Subnets list showing four subnets and their Availability Zones

![Screenshot 2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%202.png)

---

#### Screenshot 3 — Public route table showing the Internet Gateway route and both public-subnet associations

![Screenshot 3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%203.png)

---

#### Screenshot 4 — Private route table showing the NAT Gateway route and both private-subnet associations

![Screenshot 4.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%204.png)

---

#### Screenshot 5 — NAT Gateway status showing Available and the Elastic IP

![Screenshot 5.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%205.png)

---

# Task 2 — Create Security Groups (ALB, EC2, RDS) with Least Privilege

## Goal

Create `ha-alb-sg` (HTTP public), `ha-web-sg` (HTTP only from `ha-alb-sg`, SSH from your IP), and `ha-db-sg` (database port only from `ha-web-sg`).

### Evidence

#### Screenshot 6 — ALB Security Group inbound rules

![Screenshot 6.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%206.png)

---

#### Screenshot 7 — EC2 Security Group inbound rules showing the ALB Security Group reference and SSH from your IP

![Screenshot 7.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%207.png)

---

#### Screenshot 8 — RDS Security Group inbound rule showing the database port allowed only from the EC2 Security Group

![Screenshot 8.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%208.png)

---

# Task 3 — Deploy Database Tier (RDS Multi-AZ in Private Subnets)

## Goal

Launch a private, Multi-AZ RDS database (MySQL or PostgreSQL) using the private DB Subnet Group and `ha-db-sg`.

### Evidence

#### Screenshot 9 — RDS summary showing Multi-AZ = Yes and Publicly accessible = No

![Screenshot 9.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%209.png)

![Screenshot 9-1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%209-1.png)

---

#### Screenshot 10 — RDS connectivity section showing the DB Subnet Group and Security Group

![Screenshot 10.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2010.png)

---

# Task 4 — Build a Launch Template (User Data Installs App + Connects to DB)

## Goal

Create a Launch Template whose user data installs the web-server runtime, deploys the application, configures the database connection, and starts the required services.

### Evidence

#### Screenshot 11 — Launch Template details showing that user data exists, including a visible snippet

![Screenshot 11.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2011.png)

---

#### Screenshot 12 — A running instance created from the template showing that the application responds on port 80 through a local test or browser using its public IP

![Screenshot 12.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2012.png)

---

# Task 5 — Create an Application Load Balancer (ALB) Across 2 Public Subnets

## Goal

Create an internet-facing ALB across both public subnets with an HTTP listener and a healthy instance target group.

### Evidence

#### Screenshot 13 — ALB details showing two public subnets in two Availability Zones

![Screenshot 13.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2013.png)

---

#### Screenshot 14 — Target group showing at least one healthy target

![Screenshot 14.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2014.png)

---

# Task 6 — Create Auto Scaling Group (ASG) in 2 Public Subnets

## Goal

Create an Auto Scaling Group from the Launch Template across both public subnets, with desired capacity 2, minimum 2, and maximum 4, registered to the ALB target group.

### Evidence

#### Screenshot 15 — Auto Scaling Group showing desired, minimum, and maximum capacity and the selected subnet Availability Zones

![Screenshot 15.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2015.png)

---

#### Screenshot 16 — EC2 instances list showing two running instances in different Availability Zones

![Screenshot 16.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2016.png)

---

# Task 7 — Configure App to Use RDS + Validate Read/Write

## Goal

Confirm the application communicates with the RDS database through the ALB DNS name with at least one read and one write operation.

### Evidence

#### Screenshot 17 — Browser showing the application loaded through the ALB DNS name with the URL visible

![Screenshot 17.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2017.png)

---

#### Screenshot 18 — Proof of a database write through a UI message or database query output

![Screenshot 18.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2018.png)

---

# Task 8 — High Availability Tests (Must Do Both)

## Goal

Test A: terminate one web instance and confirm the Auto Scaling Group replaces it automatically without interrupting the ALB.

Test B: simulate an Availability Zone impact (stop, detach, or reduce desired capacity in one AZ) and confirm the application stays available.

### Evidence

#### Screenshot 19 — EC2 showing the terminated instance and the newly launched instance; timestamps are helpful

![Screenshot 19.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2019.png)

---

#### Screenshot 20 — Target group showing healthy targets after replacement

![Screenshot 20.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2020.png)

---

#### Screenshot 21 — Evidence that an instance was removed, detached, placed in Standby, or stopped in one Availability Zone

![Screenshot 21.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2021.png)

---

#### Screenshot 22 — Browser showing that the ALB DNS endpoint still works during the change

![Screenshot 22.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2022.png)

---

# Task 9 — Architecture and Test-Results Summary

## Goal

Summarize the VPC/subnet layout, the ALB and Auto Scaling Group setup, the private Multi-AZ RDS setup, and the results of both high-availability tests.

### Evidence

#### Screenshot 23 — A simple architecture diagram, which may be hand-drawn, or an AWS console overview showing the components

![Screenshot 23.jpg](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-06-aws-cloud/screenshots/assignment-05/Screenshot%2023.jpg)

---

### Notes

Summarize the VPC and subnets across the two Availability Zones.

The application was deployed inside the Application-VPC VPC using CIDR 10.0.0.0/16 across two Availability Zones. Two public subnets (Public-Subnet-A and Public-Subnet-B) host the internet-facing Application Load Balancer, while two private subnets (Private-Subnet-A and Private-Subnet-B) host the EC2 web application instances. An Internet Gateway provides public connectivity, while the NAT Gateway provides outbound Internet access for resources in the private subnets.

Summarize the ALB and Auto Scaling Group setup.

An internet-facing Application Load Balancer (application-web-alb) was deployed across both public subnets and configured with an HTTP port 80 listener. The ALB forwards traffic to the application-web-targets target group. An Auto Scaling Group (application-web-asg) was configured across both private subnets with a minimum capacity of 2, desired capacity of 2, and maximum capacity of 4. The two EC2 instances were successfully launched across separate Availability Zones and registered as healthy targets.

Summarize the private Multi-AZ RDS setup.

A private Amazon RDS MySQL database (application-mysql-db) was deployed using a dedicated DB subnet group containing the two private subnets. Multi-AZ deployment was enabled, public access was disabled, and access to MySQL port 3306 was restricted to the web application security group. This keeps the database private and accessible only from the application tier.

Summarize the results of both high-availability tests.

Two high-availability tests were successfully completed. First, the application was accessed through the ALB DNS name and successfully served by the Auto Scaling Group instances, with the registered targets reporting healthy status. Second, the application successfully connected to RDS and performed database read/write operations, demonstrated by the persistent page-view counter increasing between requests. These tests confirmed connectivity and the intended separation of the Internet-facing load-balancing layer, private application layer, and private Multi-AZ database layer.

---

# LinkedIn Post (Required)

## Goal

Publish a LinkedIn post about the high-availability build, including the ALB URL (or a redacted screenshot), three to five lines on what you built and how you tested high availability, and one proof screenshot.

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot of LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Do not expose passwords, connection strings, private keys, or account IDs

---

# Completion Checklist

- ✅ Task 1: VPC, four subnets, IGW, NAT Gateway, and route tables created (Screenshots 1–5)
- ✅ Task 2: Least-privilege ALB, EC2, and RDS security groups created (Screenshots 6–8)
- ✅ Task 3: Private Multi-AZ RDS created (Screenshots 9–10)
- ✅ Task 4: Self-configuring Launch Template created and tested (Screenshots 11–12)
- ✅ Task 5: ALB created across both public subnets (Screenshots 13–14)
- ✅ Task 6: Auto Scaling Group running two instances across two AZs (Screenshots 15–16)
- ✅ Task 7: Application verified through the ALB with a database read and write (Screenshots 17–18)
- ✅ Task 8: Both high-availability tests completed (Screenshots 19–22)
- ✅ Task 9: Architecture and test-results summary completed (Screenshot 23 & Notes)
- ✅ LinkedIn post published and URL submitted
- ✅ No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*

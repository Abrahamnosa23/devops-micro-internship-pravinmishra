# Assignment 1 — AWS Free Tier Account Setup (EpicReads Cloud Onboarding)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will create and verify an AWS Free Tier account as part of onboarding EpicReads — an online bookstore moving to the cloud. You will demonstrate an understanding of AWS fundamentals, Free Tier services, and account setup by answering conceptual questions and capturing proof of a working AWS Console login.

---

# Task 1 — Understanding AWS & Free Tier

## Goal

Demonstrate understanding of AWS basics and Free Tier usage by answering the following questions in your own words (3–4 lines each).

### Answers

#### Question 1 — What is an AWS account, and why do you need it at this stage?

**what is an aws account**

An AWS account is a foundational component of cloud computing that represents a user’s workspace within the AWS platform. It serves as the environment in which all cloud-based activities are created, managed, and controlled. Within this account, users can create and manage various cloud resources such as virtual servers, storage systems, and databases. It also acts as a security boundary, ensuring that only authorized individuals can access the resources inside the account, and functions as a billing unit where all usage costs are tracked and managed.

An AWS account provides several key capabilities that support cloud operations. First, it enables effective resource management, as all services such as EC2 instances (virtual machines), storage, and networking components are created and maintained within the account. This allows users to centrally manage their infrastructure in a structured and organized manner. In addition, the account offers security and access control through AWS Identity and Access Management (IAM), which defines who can access the resources and what specific actions they are permitted to perform. This ensures proper control and governance over cloud resources.

Finally, an AWS account supports billing and cost tracking, where every resource usage whether compute, storage, or network is recorded and billed accordingly. This allows users to monitor their spending, manage budgets, and optimize resource usage effectively. Overall, the AWS account serves as the core operational, security, and financial framework for working within the AWS cloud environment.

**why do you need an aws account at this stage**

At this stage of learning where the focus is on Linux, web servers, and DevOps practices, an AWS account is essential for the following reasons:

a. Access to Real Cloud-Based Linux Servers
- AWS provides services like EC2, which allow you to launch and manage Linux-based virtual machines.
- This enables hands-on practice of:
    - Installing web servers (e.g., Nginx, Apache)
    - Managing server configurations in a real environment
        
b. Ability to Host Web Applications on the Internet
- Web hosting requires infrastructure such as:
    - Servers
    - Public IP addresses
    - Network connectivity
- AWS provides all of these components, enabling applications to be deployed and accessed globally.
    
c. Exposure to Real-World DevOps Practices
- Modern DevOps workflows are built on cloud platforms like AWS.
- Using an AWS account allows learners to:
    - Provision infrastructure
    - Deploy applications
    - Manage environments (development, testing, production)
        
d. Learning Scalability and High Availability
- AWS enables systems to scale according to demand, which is not possible with a local machine.
- This is critical for understanding how production systems handle real users and traffic.
    
e. Introduction to Cloud Security Concepts
- AWS accounts expose learners to important security principles such as:
    - Identity and access control (IAM)
    - Network isolation
    - Resource-level permissions
      
These concepts are especially relevant for DevOps and infrastructure roles.

An AWS account is a fundamental requirement for learning modern cloud-based DevOps practices. It provides:
- A realistic environment for deploying Linux servers
- The ability to host and manage web applications
- A platform to gain hands-on experience with cloud infrastructure, scalability, and security
    
---

#### Question 2 — What is AWS Free Tier, and how long does it last?

The AWS Free Tier is a program provided by Amazon Web Services that allows users, especially learners like those in my DevOps cohort, to explore and use AWS cloud services at little or no cost within defined limits. It is designed to support hands-on learning by giving access to real cloud infrastructure without requiring upfront payment. Through the Free Tier, I am able to experiment with key services such as virtual servers and storage while practicing real-world tasks like deploying and managing web applications.

The AWS Free Tier includes different types of benefits that support learning and experimentation, including:

- Free usage credits that can be applied across various AWS services
- Limited free access to selected services, within specified usage limits
- Always Free services, which provide ongoing free usage every month within certain limits

In terms of duration, the AWS Free Tier is not limited to a single fixed timeframe but is structured in different components. For new users, there is a Free account plan, which allows usage of AWS services without charges for:

- Up to six months, or
- Until the allocated credits are fully used, whichever comes first

Beyond this initial period, AWS continues to offer Always Free services, which:

- Provide free monthly usage limits
- Remain available for as long as the account is active

Additionally, some AWS services include short-term trial offers, which are available for a limited time after activation.

Overall, the AWS Free Tier is important for me at this stage because it allows me to gain practical experience with Linux servers, install web servers, and host applications in a real cloud environment while managing costs. However, it also requires careful monitoring of usage to avoid exceeding limits and incurring charges.

---

#### Question 3 — Name three AWS Free Tier services and their free usage limits.

Under the AWS Free Tier, several services are available to help users practice and build applications within defined usage limits. Three common examples are:

1. Amazon EC2 (Elastic Compute Cloud)

- Provides virtual servers for running applications
- Free Tier limit includes:
    - Up to 750 hours per month of a t2.micro or t3.micro instance

This is important for my DevOps learning because it allows me to create and manage Linux servers for hosting web applications.

2. Amazon S3 (Simple Storage Service)

- Used for storing files, backups, and static websites
- Free Tier limit includes:
    - 5 GB of standard storage
    - 20,000 GET requests per month
    - 2,000 put requests per month

This can be used to store website files, application data, or backups.

3. AWS Lambda

- A serverless compute service used to run code without managing servers
- Free Tier limit includes:
    - 1 million requests per month
    - Plus free compute time within limits

This is useful for automation tasks and backend processing in modern DevOps environments.

These AWS Free Tier services (EC2, S3, and Lambda) provide essential building blocks for cloud computing. They allow learners like me to:

- Practice deploying Linux servers
- Store and manage application data
- Run code without managing infrastructure

All within free usage limits, making them ideal for hands-on DevOps training.

---

# Task 2 — Create AWS Free Tier Account

## Goal

Create a valid AWS Free Tier account and sign in to the AWS Management Console.

> No screenshots required for this task. Completion is verified through Task 3.

---

# Task 3 — Verify AWS Account

## Goal

Confirm that your AWS account setup is complete by navigating to the Account section and capturing proof.

### Evidence

#### Screenshot 1 — AWS Account page showing account name (email may be blurred)

![Week 3 - Assignment 1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-for-devops/screenshots/Week%203%20-%20Assignment%201.png)



---

# Submission Instructions

- Add all required screenshots in your GitHub repository submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- ✅ Task 1 answers written in own words
- ✅ AWS Free Tier account created successfully
- ✅ Signed in to AWS Management Console
- ✅ Screenshot of AWS Account page captured (full name visible, no sensitive data)
- ✅ All required screenshots added to repository

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*

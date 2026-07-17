# Assignment 2 — Deploy a React App on Ubuntu VM Using Nginx

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will deploy a React application on an Ubuntu EC2 instance and serve it using Nginx. You will provision a Linux server, install the required tools, personalize the application with your details, and verify that it is publicly accessible via a browser.

---

# Task 1 — Setup Environment (Node.js & npm)

## Goal

Install Node.js and npm on the Ubuntu VM and verify the installation.

### Evidence

#### Screenshot 1 — Output of `node -v && npm -v` showing installed versions

![Week 3 - Assignment 2 1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%201.png)

---

# Task 2 — Setup Environment (Nginx)

## Goal

Install Nginx, start the service, and confirm it is running.

### Evidence

#### Screenshot 2 — Output of `systemctl status nginx --no-pager` showing Active (running)

![Week 3 - Assignment 2 2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%202.png)

---

# Task 3 — Clone React Application

## Goal

Clone the project repository and verify the project files are present.

### Evidence

#### Screenshot 3 — Output of `ls` inside the `my-react-app` directory showing project files

![Week 3 - Assignment 2 3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%203.png)

---

# Task 4 — Modify Application (Personalization)

## Goal

Update `App.js` with your full name and the current date.

### Evidence

#### Screenshot 4 — `nano App.js` open showing your full name and date filled in

![Week 3 - Assignment 2 4.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%204.png)

---

# Task 5 — Build React Application

## Goal

Install dependencies and generate the production build.

### Evidence

#### Screenshot 5 — Output of `ls` inside `my-react-app` showing the `build/` folder generated

![Week 3 - Assignment 2 5.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%205.png)

---

# Task 6 — Deploy React Build to Nginx Web Root

## Goal

Copy the production build files to the Nginx web root directory.

### Evidence

#### Screenshot 6 — Output of `ls /var/www/html/` showing the deployed build contents

![Week 3 - Assignment 2 6.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%206.png)

---

# Task 7 — Configure Nginx for React Application

## Goal

Apply Nginx configuration for React routing and confirm the service is active.

### Evidence

#### Screenshot 7 — Output of `systemctl is-active nginx` showing `active`

![Week 3 - Assignment 2 7.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%207.png)

---

#### Screenshot 8 — Output of `cat /etc/nginx/sites-available/default` showing the Nginx config

![Week 3 - Assignment 2 8.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%208.png)

![Week 3 - Assignment 2 81.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%2081.png)

---

# Task 8 — Test Deployment

## Goal

Verify the React application is publicly accessible via the server's public IP.

### Evidence

#### Screenshot 9 — Output of `curl ifconfig.me` showing the server's public IP address

![Week 3 - Assignment 2 9.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%209.png)

---

#### Screenshot 10 — Browser showing the deployed React app at `http://<public-ip>` with your name and date visible

![Week 3 - Assignment 2 10.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Week%203%20-%20Assignment%202%2010.png)

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

[LinkedIn Post URL](https://www.linkedin.com/posts/abraham-aigbokhan-3abb28214_dmibypravinmishra-agenticai-claudecode-share-7483926410865192960-aCFL/?utm_source=share&utm_medium=member_desktop&rcm=ACoAADZFnjMBb3DIPPRNvWnnHBks2D59TA5vDHw)

---

#### Screenshot — LinkedIn post showing the deployed application

![Screenshot 2026-07-17 175334.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-02/Screenshot%202026-07-17%20175334.png)

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- ✅ Node.js and npm installed and verified (Screenshot 1)
- ✅ Nginx installed and running (Screenshot 2)
- ✅ Repository cloned and files verified (Screenshot 3)
- ✅ App.js updated with full name and date (Screenshot 4)
- ✅ Production build generated (Screenshot 5)
- ✅ Build files deployed to Nginx web root (Screenshot 6)
- ✅ Nginx configured and active (Screenshots 7 & 8)
- ✅ Public IP retrieved (Screenshot 9)
- ✅ React app accessible in browser with personal details visible (Screenshot 10)
- ✅ LinkedIn post published and URL submitted
- ✅ No sensitive data exposed

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

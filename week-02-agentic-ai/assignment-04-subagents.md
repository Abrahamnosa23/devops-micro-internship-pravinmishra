# Assignment 4 — Building Your AI Team

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build and configure a set of specialized AI subagents inside your project. You will learn how different models and tool permissions define agent behavior, and you will trigger two real agent delegations to analyze security and cost aspects of your Terraform infrastructure.

---

# Task 1 — Create the Agents Folder and Add Files

## Goal

Create the `.claude/agents/` directory and add all required agent files.

### Evidence

#### Screenshot 1 — VS Code sidebar showing `.claude/agents/` with all 3 files

![Screenshot 01.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-02-agentic-ai/screenshots/Assignment-04/Screenshot%2001.png)

---

# Task 2 — Compare the Agent Configurations

## Goal

Analyze the configuration differences between the three agents and demonstrate understanding of model and tool selection.

### Written Answers

#### 1. Why does the cost optimizer use Haiku instead of Sonnet?

The Cost Optimizer uses Haiku because its job is quite focused and straightforward. It mainly scans the Terraform configuration, identifies resources that incur costs, and recommends practical ways to reduce spending. This type of analysis is usually rule-based and doesn't require deep reasoning, so Haiku can do it faster and at a lower cost while still producing accurate recommendations.

On the other hand, the Security Auditor uses Sonnet because security reviews are typically more complex. It needs to assess security risks, understand resource relationships, identify misconfigurations, evaluate IAM permissions, and determine the severity of findings. That level of analysis benefits from Sonnet's stronger reasoning capabilities.

The choice comes down to efficiency. Cost optimization is a simpler review task that Haiku can handle well at a lower cost, while security auditing requires deeper analysis, making Sonnet the better fit.

---

#### 2. Why does the security auditor NOT have Write in its tools list?

The Security Auditor intentionally does not have the Write tool because its role is to act as an independent reviewer, not a modifier of code. Its job is to inspect the Terraform configuration, identify security issues, explain the risks, and recommend exact fixes, but leave the actual code changes to the engineer or another agent.

This separation helps prevent a situation where the same agent both creates and validates its own work. By restricting the Security Auditor to Read, Grep, and Glob, it can focus purely on finding issues and providing recommendations without accidentally introducing changes into the codebase.

---

#### 3. Why does the tf-writer use `inherit` instead of a specific model?

The tf-writer uses inherit because its job is to generate and modify Terraform code, and the complexity of those tasks can vary significantly. Sometimes it may only need to create a simple S3 bucket, while other times it may need to design a complete multi-service AWS architecture. By using inherit, it automatically uses the same model as the parent Claude session instead of being locked to a specific model.

This gives it more flexibility. If I'm using a more capable model for the overall task, the tf-writer benefits from that same reasoning capability when generating infrastructure code. If I'm using a lighter model, it follows that instead.

Compare that to the other agents:

  - cost-optimizer is explicitly pinned to Haiku because its analysis is relatively straightforward and cost-focused.
  - security-auditor is pinned to Sonnet because security reviews require deeper analysis and judgement.
  - tf-writer is responsible for creating the actual infrastructure code, so using inherit allows it to leverage whatever model is most appropriate for the parent workflow.

---

### Evidence

#### Screenshot 2 — `security-auditor.md` frontmatter showing model and tools configuration

![Screenshot 01.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-02-agentic-ai/screenshots/Assignment-04/Screenshot%2001.png)

---

#### Screenshot 3 — `cost-optimizer.md` frontmatter showing the model and tools configuration

![Screenshot 3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-02-agentic-ai/screenshots/Assignment-04/Screenshot%203.png)

---

# Task 3 — Run the Security Auditor

## Goal

Trigger the security auditor agent and analyze the generated security report for your Terraform infrastructure.

### Evidence

#### Screenshot 4 — The delegation message showing Claude launched the security-auditor

![Screenshot 4.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-02-agentic-ai/screenshots/Assignment-04/Screenshot%204.png)

---

#### Screenshot 5 — Security audit report output

![Screenshot 5.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-02-agentic-ai/screenshots/Assignment-04/Screenshot%205.png)

![Screenshot 5 - 1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-02-agentic-ai/screenshots/Assignment-04/Screenshot%205%20-%201.png)

---

# Task 4 — Run the Cost Optimizer

## Goal

Trigger the cost optimizer agent and review the generated cost optimization report.

### Evidence

#### Screenshot 6 — The full cost optimization report

![Screenshot 6.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-02-agentic-ai/screenshots/Assignment-04/Screenshot%206.png)

![Screenshot 6 - 1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-02-agentic-ai/screenshots/Assignment-04/Screenshot%206%20-%201.png)

---

# Submission Instructions

- Ensure all agent files are committed in `.claude/agents/`
- Complete all written answers in your GitHub Repo
- Push final changes to your forked GitHub repository

---

## GitHub Repository URL

Paste your forked repository URL here:

<<<<<<< HEAD:week-02-agentic-ai/solution-assignment-04-subagents.md
[forked repository URL](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra)

[forked repository URL](https://github.com/Abrahamnosa23/Ultimate-Agentic-DevOps-with-Claude-Code)
=======
`Add your URL here`
>>>>>>> upstream/main:week-02-agentic-ai/assignment-04-subagents.md

---

# Completion Checklist

- ✅ `.claude/agents/` folder contains all 3 agent files
- ✅ Screenshot 2 shows correct `security-auditor.md` configuration
- ✅ Screenshot 3 shows correct `cost-optimizer.md` configuration
- ✅ All 3 written answers completed 
- ✅ Security auditor executed successfully
- ✅ Cost optimizer executed successfully
- ✅ Security report is visible with findings
- ✅ Cost report is visible with recommendations
- ✅ All required screenshots added
- ✅ GitHub repo updated with agents

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

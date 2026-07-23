# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

![Week 3 - Assignment 6 11-1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2011-1.png)

![Week 3 - Assignment 6 11-2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2011-2.png)

![Week 3 - Assignment 6 11-3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2011-3.png)

---

#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

![Week 3 - Assignment 6 12-1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2012-1.png)

![Week 3 - Assignment 6 12-2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2012-2.png)

---

### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

Nginx is running when its service status shows "active (running)". This indicates that the web server has started successfully, is operating correctly, and is ready to handle web traffic and serve hosted websites or applications.

---

**2. What proves that the server is listening for HTTP traffic?**

The command curl -I http://localhost returned HTTP/1.1 200 OK, which confirms that the server is actively listening for HTTP traffic and responding successfully to requests. This verifies that Nginx is running properly and serving web content through port 80.

---

**3. Why must you capture a healthy baseline before simulating an incident?**

Capturing a healthy baseline before simulating an incident is important because it provides a reference point for how the system behaves under normal conditions. This allows you to compare the system's state before and after the incident, making it easier to identify issues, measure impact, and confirm that recovery actions were successful. This verifies that any changes observed during testing are a result of the simulated incident and not pre-existing problems.

---

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

![Week 3 - Assignment 6 23.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2023.png)

---

### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

Project-specific operational rules help Claude understand the requirements, standards, and constraints of a particular project. This ensures that recommendations, commands, and actions align with the project's objectives, reduce mistakes, and maintain consistency across tasks. This verifies that Claude provides guidance that is relevant, accurate, and tailored to the specific environment and operational needs.

---

**2. Why is the human required to execute the recovery command?**

The human is required to execute the recovery command because recovery actions can affect critical systems and services. This ensures that a person reviews the situation, verifies the action is safe, and maintains control over changes before they are applied. This verifies that recovery steps are performed with proper oversight, reducing the risk of unintended disruptions or errors.

---

**3. Which rule prevents Claude from making an unsupported diagnosis?**

Claude must not make assumptions or unsupported diagnoses. It should only draw conclusions based on verified evidence and available data.

This rule prevents Claude from making an unsupported diagnosis because it requires conclusions to be backed by actual observations, logs, command outputs, or other evidence. By following this rule, Claude avoids guessing the cause of an issue and instead bases its analysis on facts, helping ensure accurate and reliable troubleshooting.

---

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

![Week 3 - Assignment 6 34-1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2034-1.png)

![Week 3 - Assignment 6 34-2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2034-2.png)

---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The command prompt instructed Claude to inspect the Ubuntu server using only read-only commands and collect information about the current system state. This represents the Gather phase because Claude gathered evidence by checking the Nginx service status, port 80 listening state, localhost HTTP response, root disk usage, and available memory before making any recommendations. This verifies that the incident-triage plan was based on actual system data rather than assumptions.

---

**2. Did Claude follow the instruction not to create files? How did you verify this?**

Claude followed the instruction not to create files because it only performed read-only inspection commands and produced a report based on the results. The output explicitly states that it "inspected the server read-only" and later confirms "Every command above is read-only". This verifies that Claude gathered information from the system without creating, modifying, or saving any files.

---

**3. Why is planning before coding useful in DevOps automation?**

Planning before coding is useful in DevOps automation because it helps identify requirements, define the correct steps, and reduce the risk of errors before making changes to a system. In this task, Claude first gathered information and created an incident-triage plan before suggesting any actions. This verifies that decisions are based on evidence and that automation is performed in a safe, structured, and predictable manner.

---

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

![Week 3 - Assignment 6 45.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2045.png)

---

#### Screenshot 6 — Middle section showing check functions and conditionals

![Week 3 - Assignment 6 46.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2046.png)

---

#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

![Week 3 - Assignment 6 47.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2047.png)

---

#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

![Week 3 - Assignment 6 48-1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2048-1.png)

![Week 3 - Assignment 6 48-2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2048-2.png)

---

### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores the names of the five health-check functions that the script will run during the Linux incident triage process. These functions are check_service, check_port, check_http, check_disk, and check_memory. This allows the script to execute each check automatically using the loop and ensures that all required system health checks are performed in a structured and consistent manner.

---

**2. How does the `for` loop use that array?**

The for loop uses the checks array to run each health-check function automatically, one after another. The loop reads each function name stored in the array and executes it. This allows the script to perform all five checks (check_service, check_port, check_http, check_disk, and check_memory) without having to call each function individually. This makes the script easier to maintain, as new checks can be added to the array and will automatically be included in the execution process.

---

**3. Why are the health checks separated into functions?**

The health checks are separated into functions so that each check has a specific responsibility and can be managed independently. This makes the script easier to read, maintain, and troubleshoot because the logic for checking the service, port, HTTP response, disk usage, and memory is organized into separate sections. If a check needs to be updated or a new one added, it can be modified without affecting the rest of the script. This helps keep the automation structured, reusable, and easier to scale.

---

**4. What is the purpose of `$(...)` in this script?**

The $(...) syntax is used for command substitution, which means it runs a command and stores its output in a variable or inserts the output into another command. In this script, it is used to capture dynamic information such as the current date, hostname, script location, disk usage, and available memory. This makes the script more flexible because it can automatically collect and use real-time system information instead of relying on hardcoded values.

---

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

The script uses different exit codes for HEALTHY, WARN, and FAIL so that other users, scripts, or automation tools can quickly understand the result of the health checks. An exit code of 0 means everything is healthy, 1 means warnings were detected, and 2 means one or more critical failures were found. This allows monitoring and automation systems to respond appropriately based on the severity of the issue and makes the script more useful in real-world DevOps environments.

---

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

![Week 3 - Assignment 6 59.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%2059.png)

---

#### Screenshot 10 — Output showing the captured exit code and final summary

![Week 3 - Assignment 6 510.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20510.png)

---

### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

The healthy baseline has an overall status of HEALTHY. The output showed that all five health checks passed successfully, including the Nginx service status, port 80 listening state, localhost HTTP response, root disk usage, and available memory. This confirms that the server is operating normally and provides a reliable reference point for comparing the system's condition after simulating an incident.

---

**2. Which exact Linux evidence proves the application is serving traffic?**

The command curl -s -o /dev/null -w '%{http_code}' --max-time 5 http://localhost returned 200, which confirms that the application successfully accepted an HTTP request and returned a valid response. This verifies that the application is serving traffic correctly and is accessible through Nginx.

---

**3. Did your script return exit code 0 or 1? Explain why.**

The script returned exit code 0 because all the health checks passed successfully and no warnings or failures were detected. The print_summary() function assigns an exit code of 0 when the overall status is HEALTHY, 1 when warnings are present, and 2 when failures are found. This confirms that the server was operating normally during the baseline assessment and that the system passed all health checks.

---

**4. What is the difference between a warning and a failure in this script?**

A warning in this script indicates a potential issue that requires attention but does not immediately impact the application's availability, such as low available memory or disk usage exceeding the warning threshold. A failure indicates a critical problem that affects the health of the system or application, such as Nginx not running, port 80 not listening, or the HTTP check failing. This allows the script to distinguish between issues that should be monitored and issues that require immediate action.

---

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

![Week 3 - Assignment 6 611.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20611.png)

---

#### Screenshot 12 — `/linux-triage` output for the healthy server

![Week 3 - Assignment 6 612.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20612.png)

---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

The skill has Bash, Read, and Grep, but not Write, because the /linux-triage workflow is designed to be read-only. Bash allows Claude to run the health-check script, Read allows Claude to open files like CLAUDE.md and reports/linux-health-report.txt, and Grep allows Claude to search through evidence. It does not include Write because Claude is not allowed to create, edit, or modify files during triage. This verifies that the skill can gather and analyze evidence safely without changing the system.

---

**2. Why is `disable-model-invocation: true` useful for this skill?**

disable-model-invocation: true is useful because it prevents the skill from relying on extra AI reasoning beyond the defined workflow. This keeps the /linux-triage process controlled, predictable, and evidence-based, ensuring Claude only runs the allowed read-only steps, reads the report, and summarizes the findings without making unsupported assumptions or taking independent actions.

---

**3. What part is performed by Bash, and what part is performed by Claude?**

Bash performs the command execution part of the skill, such as running bash scripts/linux-triage.sh || true and generating the health report from the Linux system checks. Claude performs the analysis part by reading CLAUDE.md, reviewing reports/linux-health-report.txt, identifying the overall status, WARN/FAIL results, exact evidence, likely cause, and providing a safe recovery recommendation for the human to review. This verifies that Bash gathers the system evidence, while Claude interprets and reports the findings without modifying the system.

---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

This is better because Claude is not guessing based on a vague question. The /linux-triage skill first gathers real evidence from the server, such as the Nginx service status, port 80 status, HTTP response code, disk usage, memory, and recent logs. This makes the health assessment more accurate, repeatable, and evidence-based. It also keeps the process safer because Claude only analyzes the collected report and does not make unsupported assumptions or modify the system.

---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

![Week 3 - Assignment 6 713-1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20713-1.png)

![Week 3 - Assignment 6 713-2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20713-2.png)

---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

![Week 3 - Assignment 6 714-1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20714-1.png)

![Week 3 - Assignment 6 714-2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20714-2.png)

---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

![Week 3 - Assignment 6 715.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20715.png)

---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

The three checks that failed were Nginx service status, port 80 listening state, and local HTTP response check. The report showed "[FAIL] Nginx service is not active", "[FAIL] Port 80 is not listening", and "[FAIL] Local HTTP check returned status 000", which indicates that Nginx was not running, the server was not listening on port 80, and the application was not responding to HTTP requests. This confirms that the web service was unavailable during the incident simulation.

---

**2. What evidence supports the conclusion that Nginx is unavailable?**

The evidence that supports the conclusion that Nginx is unavailable is that the health report showed Nginx service is not active, port 80 is not listening, and the local HTTP check returned status 000. This confirms that the Nginx service was down, the server was not accepting HTTP traffic, and the website could not respond to requests.

---

**3. Did Claude execute the recovery command? Why is that important?**

Claude did not execute the recovery command. It only provided a safe recovery command for the human to review and run manually. This is important because recovery commands can change the system state, so keeping execution under human control prevents accidental service changes, maintains accountability, and follows the skill rule that Claude must not restart, modify, or recover the system by itself.

---

**4. Which phase of the Agentic Loop is represented by the Bash report?**

The Bash report represents the Gather phase of the Agentic Loop because it collects real system evidence before Claude analyzes the issue or recommends any recovery action. The report gathers details such as Nginx status, port 80 state, HTTP response, disk usage, memory, and logs, which helps Claude make an evidence-based assessment instead of guessing.

---

**5. Which phase is represented by Claude's explanation?**

Claude’s explanation represents the Analyze phase of the Agentic Loop because Claude reviews the Bash report, interprets the evidence, identifies what failed, explains the likely cause, and recommends a safe recovery command for the human to review. This shows that Claude is not gathering new data at this stage but using the collected evidence to make an informed conclusion.

---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

![Week 3 - Assignment 6 816-1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20816-1.png)

![Week 3 - Assignment 6 816-2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20816-2.png)

---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

![Week 3 - Assignment 6 817.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20817.png)

---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

![Week 3 - Assignment 6 818.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20818.png)

---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

![Week 3 - Assignment 6 819.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20819.png)

---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

The manual action I executed was done using the command "sudo systemctl start nginx". This command was used to start the Nginx service after the health checks identified that Nginx was not active. By running this command manually, I restored the web service and allowed the server to begin listening for HTTP traffic again. This followed the skill's safety requirement that recovery actions must be reviewed and executed by a human rather than by Claude.

---

**2. What evidence proves that the service recovered?**

The evidence that proves the service recovered is that Nginx became active again, port 80 was listening, and the HTTP check returned a successful response. The command systemctl is-active nginx returned active, and the command curl -I http://localhost returned HTTP/1.1 200 OK, which confirms that Nginx recovered successfully and the web application was serving traffic again.

---

**3. Why is the second triage run necessary?**

The second triage run is necessary to confirm that the manual recovery action actually fixed the issue. It provides fresh evidence after running sudo systemctl start nginx, showing whether Nginx is active, port 80 is listening, and the HTTP check is returning a successful response. This verifies that the service recovered properly and that the incident was resolved based on evidence, not assumption.

---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

If an AI agent automatically restarted every failed service, it could make the situation worse by restarting services without understanding the real cause of the problem. For example, the service might fail because of a configuration error, lack of disk space, or another underlying issue that a restart will not fix. Automatic restarts could also cause service disruptions, hide the root cause, create repeated failure loops, or affect other dependent systems. This is why human approval is important, as it ensures recovery actions are reviewed and applied safely based on the available evidence.

---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

AI as a chatbot mainly responds to questions and conversations, while AI in an agentic workflow follows structured rules, gathers real evidence, analyzes the results, and provides recommendations based on verified data to help complete a specific task safely and consistently.

---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Abraham Aigbokhan

**Date:** 23/07/2026

---

**1. Reported Symptom**

The reported symptom was that the web application was unavailable. The website could not serve traffic because Nginx was not active, port 80 was not listening, and the local HTTP check did not return a successful response.

---

**2. Evidence Collected**

The evidence collected showed that the Nginx service was not active, port 80 was not listening, and the local HTTP check returned status 000. These results confirmed that the server was not accepting HTTP traffic and the application was not reachable through Nginx.

---

**3. Most Likely Cause**

The most likely cause was that the Nginx service was stopped or not running. Since Nginx was inactive, the server could not listen on port 80 or respond to HTTP requests.

---

**4. Human-Approved Recovery Action**

The safe recovery action was for a human to review and manually start the Nginx service. This action was performed by a human (myself), not Claude, because it changes the system state.

---

**5. Verification**

After the recovery action, the service should be verified by checking that Nginx is active and that the local website returns a successful HTTP response. The command curl -I http://localhost should return HTTP/1.1 200 OK, confirming that the application is serving traffic again.

---

**6. Safety Decision**

Claude did not execute the recovery command because the skill rules require recovery actions to be reviewed and performed manually by a human. This keeps control, accountability, and safety with the operator and prevents Claude from making changes directly on the server.

---

**7. Agentic Loop Mapping**

The Bash report represents the Gather phase because it collected evidence from the server, including service status, port status, HTTP response, disk usage, memory, and logs. Claude’s explanation represents the Analyze phase because Claude reviewed the collected evidence, identified the likely cause, and suggested a safe recovery command for human review.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

[LinkedIn Post URL](https://www.linkedin.com/posts/abraham-aigbokhan-3abb28214_devops-agenticai-linux-ugcPost-7486138173211750402-472O/?utm_source=share&utm_medium=member_desktop&rcm=ACoAADZFnjMBb3DIPPRNvWnnHBks2D59TA5vDHw)

---

#### Screenshot — Published LinkedIn post

![Week 3 - Assignment 6 LinkedIn Post.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-06/Week%203%20-%20Assignment%206%20LinkedIn%20Post.png)

---

# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

[GitHub Folder Containing Assignment](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/tree/main/week-03-linux-and-bash-for-devops)

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- ✅ Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- ✅ Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- ✅ Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- ✅ Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- ✅ Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- ✅ Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- ✅ Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- ✅ Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- ✅ Incident summary contains all seven required sections
- ✅ LinkedIn post published and URL submitted
- ✅ Full Name visible in all required screenshots and the Bash report
- ✅ Skill does not have Write permission
- ✅ Skill did not execute any recovery commands
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

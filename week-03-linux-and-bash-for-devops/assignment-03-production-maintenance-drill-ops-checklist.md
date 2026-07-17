# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

![Week 3 - Assignment 3 1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%201.png)

![Week 3 - Assignment 3 1.1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%201.1.png)

---

#### Screenshot 2 — Output of `ip a`

![Week 3 - Assignment 3 1.2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%201.2.png)

---

#### Screenshot 3 — Output of `sudo ss -tulpen`

![Week 3 - Assignment 3 1.3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%201.3.png)

---

#### Screenshot 4 — Output of `sudo ufw status`

![Week 3 - Assignment 3 1.4.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%201.4.png)

---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

To prove Nginx is actively listening globally on port 80, you can run core Linux networking utilities such as (ss -tulnp, netstat -tuln, or lsof -i :80) in your terminal. The definitive proof is found directly in the output columns, which will display a socket state explicitly marked as LISTEN bound to the local address 0.0.0.0:80 (or *:80), with the process identified as nginx. This visually confirms that the Nginx master and worker processes have successfully claimed the port and are completely open to receiving inbound traffic from any external network interface assigned to the server.

Additionally, you can verify this binding at the application level by executing a quick local HTTP request using curl -I http://127.0.0.1:80. When the terminal immediately returns a successful response containing a header field like Server: nginx, it provides active, runtime proof that port 80 is live, responding, and being managed by your Nginx web server rather than a competing service.

![proves Nginx is listening.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/proves%20Nginx%20is%20listening.png)

![proves Nginx is listening 2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/proves%20Nginx%20is%20listening%202.png)

---

**2. What proves SSH is active on port 22?**

To prove that SSH is actively listening on port 22, you can use the Linux socket statistics utility by running sudo ss -tulnp or netstat -tuln in your terminal. The definitive proof is a line in the output showing a socket state of LISTEN bound to the local address 0.0.0.0:22 for IPv4 traffic. This output explicitly verifies that the system's Secure Shell daemon (sshd) has successfully claimed port 22 across all network interfaces and is completely open to receiving remote connection requests.

Additionally, you can double-check the health of the underlying service by running sudo systemctl status ssh. When the system manager returns an active (running) status, it confirms that the daemon is functional in the background. You can even perform a local connection check using a command like ssh localhost, if the port immediately responds with an OpenSSH protocol string (such as SSH-2.0-OpenSSH...), it provides absolute confirmation that port 22 is live and interacting correctly.

![proves ssh is listening.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/proves%20ssh%20is%20listening.png)

![proves ssh is listening 2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/proves%20ssh%20is%20listening%202.png)

---

**3. Did you find any unexpected open ports? Explain briefly.**

No, there are no unexpected open ports. Every port listed in my ss -tulnp output is completely standard and expected for a clean Ubuntu EC2 instance configured to serve a web application.

All the extra ports are locked down to internal system interfaces or fundamental networking utilities.

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

![Week 3 - Assignment 3 2.1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%202.1.png)

---

#### Screenshot 2 — Output of `sudo nginx -t`

![Week 3 - Assignment 3 2.2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%202.2.png)

---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

![Week 3 - Assignment 3 2.3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%202.3.png)

---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart in production, my web application will experience immediate downtime. Nginx acts as the public-facing gateway serving my static React build files, its failure means there is no active service listening on port 80 to catch incoming web traffic. 

Anyone trying to access my application through their browser will be met with a generic error page like Connection Refused or This site can’t be reached.

A restart command explicitly kills the currently running, healthy Nginx process before attempting to spin up the new one. If the new configuration contains a syntax error or a broken path, the system is left with no web server running at all.

This results in disrupted user experiences, failed transactions, and if monitoring is setup before the failed restart, alerts will be sent to me the devops engineering managing the server or the devops team.

---

**2. What's your basic rollback plan?**

My basic rollback plan will rely on proactive pre-deployment backups and decoupled directory structures to ensure immediate recovery if a production update fails. Before making any changes, i will always copy my working configuration file (creating a .bak file) and store new build files in separate versioned folders rather than overwriting my active web root. By setting up a symbolic link (symlink) to act as my Nginx web root pointing to the current version directory, i can easily deploy updates to a new folder and switch the link. If the application breaks, reverting is as simple as flipping that symlink back to the last known stable folder.

If a failure occurs, the rollback is safely executed by restoring my backed-up configuration file or pointing my symlink back to the previous version directory. Crucially, i must verify the configuration syntax by running sudo nginx -t before applying the changes, followed by sudo systemctl reload nginx instead of a full restart. Reloading forces Nginx to seamlessly spin up worker processes using the stable configuration without terminating active user connections, achieving a zero-downtime rollback that can then be quickly verified using systemctl is-active nginx.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

![Week 3 - Assignment 3 3.1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%203.1.png)

---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

![Week 3 - Assignment 3 3.2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%203.2.png)

---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

![Week 3 - Assignment 3 3.3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%203.3.png)

---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

My Nginx error log shows absolutely no operational or configuration errors, with the only recent entry being a standard system notice confirming that the server smoothly inherited its network sockets upon startup without conflict. This clean log status provides strong runtime proof of overall environment stability, verifying that my Nginx configuration syntax is perfectly valid and that the web server possesses the necessary file permissions to seamlessly access and serve my static React application assets.

---

**2. If there were no errors, what does that indicate about the system?**

A clean Nginx error log indicates that the web server is operating in a perfectly stable, healthy state. It explicitly confirms that the Nginx configuration is completely valid and free of structural syntax errors, allowing the background daemon to bind to port 80 cleanly. Additionally, it provides definitive proof that Nginx possesses the proper file permissions to read, access, and serve the production React build assets out of the /var/www/html/ directory, ensuring seamless delivery to public visitors hitting my react application.

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

Yes, my curl requests are explicitly visible in the Nginx access log entries. Near the bottom of my log readout, there are two distinct entries originating from the local loopback interface (127.0.0.1) executing HEAD requests, with the User-Agent clearly recorded by the server as "curl/8.18.0".

This visibility provides definitive proof of two key milestones in my infrastructure's traffic flow:

It proves that network traffic is successfully routing through the local network stack, hitting port 80, and being intercepted by Nginx without being blocked by internal firewall rules or permissions.

It confirms that the Nginx logging mechanism is fully operational. The server is not just serving the React application assets cleanly; it is also successfully executing its real-time audit trail, validating that every transaction touching the server is tracked and accounted for.

---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

![Week 3 - Assignment 3 4.1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%204.1.png)

---

#### Screenshot 2 — Output of `free -h`

![Week 3 - Assignment 3 4.2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%204.2.png)

---

#### Screenshot 3 — Output of `df -h`

![Week 3 - Assignment 3 4.3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%204.3.png)

---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

![Week 3 - Assignment 3 4.4.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%204.4.png)

---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

The most critical resource on this server right now is disk space. While the CPU and memory utilization are both healthy, the root filesystem has a relatively small total capacity of 6.7 GB, with 4.1 GB already used and only 2.6 GB remaining. This means that 62% of the available disk space is already consumed. Although this is not yet at a critical threshold, the limited overall storage capacity makes disk space the resource most likely to become a constraint as the server continues to operate, especially if additional applications, logs, updates, or user data are added.

In comparison, the CPU is under almost no load, as shown by the load averages of 0.01, 0.01, and 0.00, indicating that the server is currently handling its workload with ease and there are no performance concerns related to processing power. Memory usage is also within acceptable limits. Out of 908 MB of RAM, only 320 MB is in use, and approximately 587 MB remains available for applications. There is currently no sign of memory pressure.

Based on the available metrics, the server is performing well overall, but disk capacity will be monitored most closely. The current CPU and memory usage provide comfortable headroom, whereas the small root volume size means that future growth in logs, packages, application files, or data could lead to storage shortages more quickly than resource exhaustion in other areas.

---

**2. What happens if disk becomes 100% full in a production server?**

If a production server's disk reaches 100% capacity, applications and services can fail because they can no longer write data to the filesystem. Databases, web applications, log files, backups, and system processes may stop working or become unstable. Users may experience outages, and performance issues, while administrators may lose the ability to collect logs needed for troubleshooting. In severe cases, the server may become unresponsive or fail to boot properly after a restart. This is why disk usage should be monitored closely, with alerts configured before it reaches critical levels.

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

![Week 3 - Assignment 3 5.1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%205.1.png)

---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

![Week 3 - Assignment 3 5.2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%205.2.png)

---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

![Week 3 - Assignment 3 5.3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%205.3.png)

---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

I confirm that the correct version of the application is deployed by comparing the version running on the production server with the version that was intended for deployment. This can be done by checking application version files, release notes, build numbers, Git commit hashes, or deployment logs. I also verify that the latest code changes are present by reviewing the deployed application, checking specific features or fixes included in the release, and ensuring that the deployment completed successfully without errors. If available, I compare the deployed version against the CI/CD pipeline records or source code repository to confirm they match. This provides assurance that the expected application version is running in production.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

![Week 3 - Assignment 3 6.1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%206.1.png)

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

![Week 3 - Assignment 3 6.2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%206.2.png)

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![Week 3 - Assignment 3 6.3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%206.3.png)

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

The configuration failed because of a syntax error in the Nginx configuration file, specifically around the listen directive on line 41 of /etc/nginx/sites-enabled/default. Nginx detected the invalid configuration during the nginx -t validation check and prevented the configuration from being loaded, protecting the service from starting with a broken configuration.

---

**2. How did you fix the issue?**

I fixed the issue by first running the Nginx configuration test command (sudo nginx -t), which identified an error on line 41 of the /etc/nginx/sites-enabled/default file. After locating the affected line, I reviewed the configuration and corrected the syntax error related to the listen directive. The problem was caused by an invalid configuration entry, which prevented Nginx from successfully validating the configuration file. 

Once the correction was made, I ran sudo nginx -t again to confirm that the configuration syntax was valid and that the test passed successfully. Finally, I safely reloaded the Nginx service to apply the corrected configuration and verified that the web service was running normally and serving requests without errors.

---

**3. How can you avoid this kind of issue in real production systems?**

To avoid this type of issue in production, i will always test Nginx configurations before applying them, i will use a staging environment for validation, and keep configurations under version control so changes can be tracked and rolled back if needed. I will also create backups before making changes and follow a formal change management process. 

After validating the configuration with nginx -t, i will use a reload instead of a restart to minimize downtime. I will also enure regular monitoring and alerting which can also help detect and resolve issues quickly before they impact users.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

![Week 3 - Assignment 3 7.1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%207.1.png)

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![Week 3 - Assignment 3 7.2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%207.2.png)

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

The application broke because the main application file (index.html) was removed from the web server's document root (/var/www/html). When a user accessed the website, Nginx could no longer find the default page to serve, which caused the application to become unavailable and return an error page. Since index.html serves as the entry point for the website, removing it effectively made the web server unable to display the application's content. This scenario simulates a failed deployment where essential application files are missing, corrupted, or not copied to the production server during deployment.

---

**2. How did you fix the issue and restore the application?**

I fixed the issue by first verifying that the index.html file was missing from the /var/www/html directory, which confirmed that the application's main content was no longer available to the web server. I then restored the file from the backup location by moving it back to its original directory. After restoring the file, I verified that it was present in the web root and tested the website to ensure that Nginx could serve the application correctly. 

Finally, I confirmed that the website was accessible and functioning normally, which proved that the missing deployment content had been successfully restored and the application had recovered.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

To prevent this kind of issue in a real production environment, I would implement a controlled deployment process that includes automated checks, backups, and validation steps. Before deploying any changes, I would ensure that all required application files are included in the deployment package and test the deployment in a staging environment. I would also maintain backups of the application files so that missing content can be restored quickly if a deployment fails. Using version control systems helps ensure that the correct files are deployed consistently and reduces the risk of accidental deletion.

Additionally, I would perform post-deployment verification by checking that critical files exist, confirming that the application is accessible, and reviewing application and web server logs for errors. Monitoring and alerting should also be configured to quickly detect when a website becomes unavailable. These practices help identify deployment issues early and significantly reduce the chances of service disruption caused by missing or incomplete application content.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

SSH key-based authentication is more secure than passwords because it uses cryptographic keys instead of credentials that can be guessed, reused, or stolen. The private key stays on the user's device and is never sent across the network, making it much harder for attackers to compromise. SSH keys are also far more resistant to brute-force attacks due to their complexity.

Additionally, SSH keys provide better access control and accountability since each user can have a unique key that can be revoked individually if needed. Unlike shared passwords, this reduces security risks and makes it easier to manage and audit access to production systems.

---

**2. Why should only required ports be open on a production server?**

Only the required ports should be open on a production server because every open port creates a potential entry point for attackers. Unnecessary ports increase the server's attack surface and may expose vulnerable or unused services. By allowing only essential ports, such as those needed for web traffic or administration, organizations reduce security risks, improve system security, and make monitoring and troubleshooting easier. This follows the principle of least privilege and helps protect the server from unauthorized access and attacks.

---

**3. Why is it important for Nginx to be enabled on boot?**

It is important for Nginx to be enabled on boot because it ensures the web server starts automatically whenever the server is restarted. This helps keep websites and applications available without requiring manual intervention. Enabling Nginx on boot reduces downtime, improves reliability, and prevents situations where a server is running but the web service remains offline after a reboot.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Sharing secrets, keys, or credentials publicly can lead to unauthorized access to systems, applications, and sensitive data. Attackers may use exposed credentials to steal information, modify systems, deploy malicious software, or incur unexpected costs, especially in cloud environments. It can also result in data breaches, service disruptions, compliance violations, reputational damage, and financial losses. To reduce these risks, credentials should be kept secure, managed through approved secret-management solutions, and rotated immediately if they are accidentally exposed.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Cloud resources should be stopped or terminated when they are no longer needed to avoid unnecessary costs, improve security, and ensure efficient resource management. Running resources such as virtual machines, databases, and storage services continue to consume cloud resources and may incur charges even when they are not being actively used. Unused resources can also increase the attack surface of an environment, creating potential security risks if they are left unmonitored or improperly configured.

Removing unnecessary resources helps organizations control spending, maintain a cleaner cloud environment, and reduce the risk of misconfigurations or unauthorized access. It also makes it easier to manage and monitor active workloads. Regularly reviewing and decommissioning unused cloud resources is a cloud best practice that improves both security and operational efficiency.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

[LinkedIn post URL](https://www.linkedin.com/posts/abraham-aigbokhan-3abb28214_dmi-cohort-4-live-micro-internship-waiting-share-7483983525290106881-edRb/?utm_source=share&utm_medium=member_desktop&rcm=ACoAADZFnjMBb3DIPPRNvWnnHBks2D59TA5vDHw)

---

#### Screenshot — Published LinkedIn post

![Week 3 - Assignment 3 linkedIn post.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-03/Week%203%20-%20Assignment%203%20linkedIn%20post.png)


---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- ✅ Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- ✅ Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- ✅ Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- ✅ Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- ✅ Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- ✅ Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- ✅ Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- ✅ Task 8: Security & Reliability Notes answered
- ✅ LinkedIn post published and URL submitted
- ✅ Full Name visible in all required screenshots
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

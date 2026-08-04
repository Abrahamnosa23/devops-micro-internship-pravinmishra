# Week 00 - Internet and Networking

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

# 🧑‍💻 Task 1: Using ChatGPT as Your Learning Assistant

## Scenario

You're new to DevOps and will frequently encounter technical questions. ChatGPT can be your learning companion.

## Your Task

Write a clear ChatGPT prompt to help you understand:

> "What is a protocol in networking? Explain with a simple real-life example."

Take a screenshot of your interaction showing:

* Your detailed prompt (with clear expectations)
* ChatGPT's simplified response with an example

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![Task 1 Screenshot](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-00-internet-and-networking/screenshots/Task-1%20Screenshot.png)

Replace `task-1-chatgpt.png` with your actual screenshot file name.

---

## What I Learned (2–3 lines)

I learned that a protocol is a shared set of communication rules for devices.
It works like mailing a letter: devices need the right address and format so data reaches and can be understood by the correct destination.

---

# 🌐 Task 2: Internet and Networking

## Scenario

Your friend is launching an online bookstore named **EpicReads**.

He asked you to explain how users globally can access his website hosted in Finland.

## Your Task

Write a short explanation (**100–150 words**) that includes:

* Packet Switching
* IP Address
* TCP/IP
* HTTP/HTTPS

💡 **Tip:** You may use ChatGPT (as demonstrated in Task 1) to refine your explanation.

## Answer

When someone types EpicReads.com into their browser, their request doesn't travel as one solid stream, it is broken into small chunks called packets (this is packet switching). Each packet independently finds the best route across the internet to your server in Finland, then gets reassembled at the destination.

To know where to go, every device online has a unique IP address which is essentially a postal address for computers.

The whole journey is governed by TCP/IP: IP handles addressing and routing, while TCP makes sure packets arrive complete, in the right order, and error free, resending anything that gets lost.

HTTP/HTTPS is the language browsers and servers use to request and deliver web pages. HTTPS adds encryption, keeping customer data like payment info secure.

Together, all the above lets anyone, anywhere, load EpicReads instantly and safely.

---

# 🏗️ Task 3: Application Architecture & Stack

## Scenario

EpicReads bookstore has two application versions:

### Two-Tier Application

* Frontend
* Database

### Three-Tier Application

* Frontend
* Backend
* Database

## Your Task

* Draw simple diagrams (hand-drawn or tool-based such as draw.io)
* Label each layer clearly
* List at least two common technologies or tools used for each layer
* Submit a screenshot or photo clearly showing your own drawing

## Diagram Screenshot / Photo

Save your diagram image in the `screenshots` folder and update the file name below.

![Application Architecture Diagram](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-00-internet-and-networking/screenshots/Task-3%20Screenshot.png)


Replace `task-3-diagram.png` with your actual diagram file name.

---

## Technologies Used

### Frontend

* React
* Angular
* HTML/CSS/JavaScript
* Vue.js

### Backend

* Node.js (Express)
* Django
* Spring Boot
* .NET

### Database

* MySQL
* PostgreSQL
* MongoDB
* Oracle DB

---

# 🌍 Task 4: Domain Name & DNS (Basic Concepts)

## Scenario

Your friend's bookstore **EpicReads** is currently accessible through:

```text
52.172.142.222:3000
```

He purchased the domain:

```text
epicreads.com
```

## Your Task

In **50–100 words**, explain in your own words:

1. What is DNS (Domain Name System)?
2. Which DNS record type should be used to connect the domain to the given IP, and why?

## Answer

DNS (Domain Name System) is the internet's directory service. It translates human-friendly domain names like epicreads.com into machine-readable IP addresses, so users don't need to memorize numbers like 52.172.142.222.

To connect epicreads.com to that IP address 52.172.142.222, i will use an A record, since it points a domain directly to an IPv4 address. DNS only maps the domain to the IP, the port (3000) is not part of the record, so the server would need to run on the default port 80/443, or use a reverse proxy to forward traffic properly.

---

# 💻 Task 5: Visual Studio Code Setup (Hands-on)

## Your Task

Install Visual Studio Code (if not already installed).

Take a screenshot of your VS Code environment showing:

* Terminal open inside VS Code
* Running a basic command:

### Windows

```powershell
dir
```

### Linux / macOS

```bash
pwd
ls
```

* Your selected VS Code theme clearly visible

⚠️ **Important:** The screenshot must show your username or another identifiable detail to confirm it is your environment.

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![VS Code Setup Screenshot](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-00-internet-and-networking/screenshots/Task-5%20Screenshot-1.png)

![VS Code Setup Screenshot-2](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-00-internet-and-networking/screenshots/Task-5%20Screenshot-2.png)


Replace `task-5-vscode.png` with your actual screenshot file name.

---

# 🔗 Task 6: Publish Your Assignment as a LinkedIn Post

## Objective

Publishing on LinkedIn helps you:

* Build your professional online presence
* Reinforce your learning
* Document your DevOps journey publicly

## Your Task

Summarize your answers from Tasks 1–5 into a LinkedIn post.

Clearly structure your post into the following sections:

* ChatGPT
* Internet & Networking
* App Architecture
* DNS
* VS Code Setup

Add the following credit note at the end of your post:

> **P.S. This post is part of the DevOps Micro Internship (DMI) with Agentic AI — Cohort 3 — by Pravin Mishra. My graded progress is public: https://dmi.pravinmishra.com/s/YOUR-GITHUB-USERNAME.html · Start your DevOps journey: https://dmi.pravinmishra.com/?utm_source=student&utm_medium=ps-linkedin&utm_campaign=cohort3**

---

## LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/abraham-aigbokhan-3abb28214_pravin-mishra-the-cloudadvisory-linkedin-activity-7443248268572061697-m_Nl?utm_source=share&utm_medium=member_desktop&rcm=ACoAADZFnjMBb3DIPPRNvWnnHBks2D59TA5vDHw)

---

## LinkedIn Post Backup Copy

Paste the full text of your LinkedIn post here:

My DevOps Learning Journey, Key Concepts Explored

1. ChatGPT
I have explored how AI can help explain complex concepts in simple terms. Using ChatGPT, I was able to break down networking protocols, packet switching, and web technologies into beginner-friendly explanations, helping me solidify my understanding while also creating teaching examples.

2. Internet & Networking
- Packet Switching: Data is split into small packets that travel independently across the internet and are reassembled at the destination.
- IP Address: A unique numerical label for each device, like a home address, ensuring data reaches the right destination.
- TCP/IP: Rules that guarantee packets arrive correctly and in order.
- HTTP/HTTPS: Protocols for loading web pages, with HTTPS adding security.

Example: When someone in Nigeria visits my friend’s bookstore, EpicReads, packets travel globally, guided by these protocols.

3. App Architecture
- Two-tier apps: Frontend + Database (simpler, direct communication).
- Three-tier apps: Frontend + Backend + Database (more scalable, secure).
- Tools/technologies used: HTML, CSS, JavaScript, React, Angular, Node.js, Django, MySQL, PostgreSQL, MongoDB.

4. DNS
- Domain Name System (DNS): Internet’s phonebook, translating domains into IP addresses.
- A Record: Maps a domain (epicreads.com) to an IPv4 IP (52.172.142.222:3000), so users don’t need to type numeric addresses.

5. VS Code Setup
I set up Visual Studio Code for DevOps development, configured extensions for Python, JavaScript, Docker, and Git integration, ensuring smooth code management and collaboration.

**P.S. This post is part of the DevOps Micro Internship (DMI) with Agentic AI — Cohort 3 — by Pravin Mishra. My graded progress is public: https://dmi.pravinmishra.com/s/YOUR-GITHUB-USERNAME.html · Start your DevOps journey: https://dmi.pravinmishra.com/?utm_source=student&utm_medium=ps-linkedin&utm_campaign=cohort3**

---

# Reflection – Week 0

### What did you find easy?

Explaining networking concepts once I understood the core idea protocols, packet switching, and TCP/IP made sense once I had a real-life analogy to anchor them to. Writing a structured AI prompt was also more intuitive than expected once I saw the role + format + constraints pattern.

---

### What was difficult?

Keeping technical explanations accurate but concise (e.g. explaining DNS and A records in under 100 words) took a few passes. Understanding why three-tier architecture is preferred over two-tier not just what it is required connecting it back to real concerns like security and separation of logic.

---

### What will you improve next week?

I did not finish setting up my vscode, so I want to go back and actually complete it hands-on rather than just reading about it. I would also like to try deploying something small myself like pointing a real domain at a server with an A record instead of only explaining the concept.

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.


## 📌 Resources

- 🌐 **DMI Official Website:** https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 **University:** https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 **Discord Community:** https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 **Blog:** https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ **YouTube Playlist (DMI Cohort 3):** https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 **Pravin Mishra (LinkedIn):** https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 **CloudAdvisory (LinkedIn):** https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track*

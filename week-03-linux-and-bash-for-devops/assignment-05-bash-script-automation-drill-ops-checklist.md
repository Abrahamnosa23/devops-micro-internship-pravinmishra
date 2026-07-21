# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

![Week 3 - Assignment 4 1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%201.png)

![Week 3 - Assignment 4 11.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2011.png)

---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

![Week 3 - Assignment 4 12.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2012.png)

![Week 3 - Assignment 4 121.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%20121.png)

---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash is the command-line shell used in Linux that lets you interact with the operating system by typing commands. It is commonly used to manage files, run programs, administer servers, and automate tasks through scripts, making it an essential tool for Linux and DevOps work.

---

**2. What is the difference between shell and Bash?**

A shell is any program that allows users to interact with an operating system through commands, while Bash is a specific type of shell. Bash is one of the most popular shells used on Linux systems and provides additional features for running commands and automating tasks.

---

**3. Why is it important to confirm the Bash version before writing scripts?**

It is important to confirm the Bash version before writing scripts because some commands and features may only work in certain versions. Checking the version helps ensure the script will run correctly and avoids compatibility issues when using different Linux systems.

---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

![Week 3 - Assignment 4 21.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2021.png)

---

#### Screenshot 2 — Output of `./first-script.sh`

![Week 3 - Assignment 4 22.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2022.png)

---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

![Week 3 - Assignment 4 23.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2023.png)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

The #!/bin/bash line tells the system that the script should be executed using the Bash shell. It ensures the script runs with the correct interpreter, helping avoid errors and ensuring commands behave as expected.

---

**2. Why do we use `chmod +x` before running a script?**

We use chmod +x to make a script executable. Without this permission, the system will treat the script as a regular file and won't allow it to run directly. By adding the execute permission, we can run the script like a program instead of having to open it manually.

---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

Copilot said:

When you run a script with ./script.sh, the system executes it directly using the interpreter specified in the first line of the script (for example, #!/bin/bash), and the script must have execute permissions. When you run bash script.sh, you are explicitly telling Bash to execute the script, so it does not need execute permissions or a shebang line. Using ./script.sh runs the script as an executable file, while bash script.sh runs it through the Bash interpreter directly.

---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

![Week 3 - Assignment 4 31.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2031.png)

---

#### Screenshot 2 — Output of `./user-info.sh`

![Week 3 - Assignment 4 32.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2032.png)

---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable in Bash is a name used to store a value that can be referenced and reused in a script. Variables make scripts more flexible and easier to manage because you can store information such as names, file paths, or command outputs and use them whenever needed without typing the same value repeatedly.

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

We should avoid spaces around the = sign when creating variables because Bash treats spaces as separators between commands and arguments. If spaces are added, Bash will not recognize it as a variable assignment and will return an error. For example, name=John works correctly, but name = John does not because Bash interprets it differently.

---

**3. How do you access the value stored inside a Bash variable?**

Copilot said:

You can access the value stored in a Bash variable by placing a $ sign before the variable name. This tells Bash to retrieve and use the value stored in that variable instead of the variable name itself.

---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

![Week 3 - Assignment 4 41.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2041.png)

---

#### Screenshot 2 — Output of `./tools-checklist.sh`

![Week 3 - Assignment 4 42.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2042.png)

---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array in Bash is a variable that can store multiple values instead of just one. It allows you to keep related data together under a single variable name and access each value using its position in the array. This makes it easier to manage and work with lists of items in a script.

---

**2. Why are arrays useful in scripts?**

Arrays are useful in scripts because they allow you to store and manage multiple values in a single variable. This makes it easier to work with lists of items, process data in loops, and organize information without creating many separate variables, making scripts cleaner and more efficient.
---

**3. What does `"${tools[@]}"` mean?**

"${tools[@]}" is used to access all the elements in an array. It tells Bash to expand the array and treat each item as a separate value. This is commonly used in loops when you want to work through every item stored in the array one by one.

---

**4. What is the purpose of the `for` loop in this script?**

The for loop is used to repeat a set of commands for each item in a list or array. In this script, it goes through each element in the tools array one at a time and performs the specified action on each value. This helps automate repetitive tasks and makes the script more efficient.

---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

![Week 3 - Assignment 4 51.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2051.png)

---

#### Screenshot 2 — Output of `./counter.sh`

![Week 3 - Assignment 4 52.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2052.png)

---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop is a programming structure that allows a set of commands to run repeatedly until a condition is met or all items in a list have been processed. In Bash, loops help automate repetitive tasks, save time, and make scripts more efficient by avoiding the need to write the same commands multiple times.

---

**2. Why do we use loops in Bash scripting?**

We use loops in Bash scripting to automate repetitive tasks. Instead of writing the same command multiple times, a loop can execute it repeatedly for different files, values, or conditions. This makes scripts shorter, easier to manage, and more efficient.

---

**3. How many times did the loop run in your script?**

The loop ran 5 times, as shown by the five completed steps in the output. Each time the loop executed, it displayed a different step number until it reached Step 5 and then ended successfully.

---

**4. What would you change if you wanted the loop to run 10 times?**

To make the loop run 10 times, I would add the numbers 6 through 10 to the for loop list. This would cause the loop to execute once for each number, resulting in 10 iterations instead of 5.

---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

![Week 3 - Assignment 4 61.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2061.png)

---

#### Screenshot 2 — Content of `file-check.sh`

![Week 3 - Assignment 4 62.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2062.png)

---

#### Screenshot 3 — Output of `./file-check.sh`

![Week 3 - Assignment 4 63.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2063.png)

---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

The -d option in Bash is used to check whether a directory exists. It returns true if the specified path is a directory and false if it does not exist or is not a directory. This is useful in scripts when you need to verify that a folder is present before performing actions on it.

---

**2. What does `-f` check in Bash?**

The -f option in Bash is used to check whether a file exists and is a regular file. It returns true if the file is present and false if the file does not exist or if the path points to something else, such as a directory. This is useful in scripts when you need to confirm that a file is available before reading, copying, or modifying it.

---

**3. Why should file and directory paths be stored in variables?**

File and directory paths should be stored in variables to make scripts easier to read, manage, and update. If a path changes, you only need to update it in one place instead of throughout the entire script. This also reduces errors and makes the script more flexible and reusable.

---

**4. What happens if the file does not exist?**

If the file does not exist, the script detects this during the file check and displays a message indicating that the file is missing instead of trying to access it. In my script, the directory existed, but the file student-infosss.txt was not found, so the script returned the message "File does not exist" and continued safely without crashing.

---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

![Week 3 - Assignment 4 71.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2071.png)

---

#### Screenshot 2 — Output showing `Result: Pass`

![Week 3 - Assignment 4 72.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2072.png)

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

![Week 3 - Assignment 4 73.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2073.png)

---

#### Screenshot 4 — Output showing `Result: Retry`

![Week 3 - Assignment 4 74.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2074.png)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

The purpose of if-else in Bash is to make decisions based on conditions. It allows a script to perform one action if a condition is true and a different action if the condition is false. This makes scripts more intelligent and able to handle different situations automatically.

---

**2. What does `-ge` mean?**

The -ge operator in Bash means "greater than or equal to". It is used to compare two numeric values and check whether the first number is greater than or equal to the second. This is commonly used in if statements to make decisions based on numerical comparisons.

---

**3. Why should conditions be tested with different values?**

Conditions should be tested with different values to make sure the script works correctly in all situations. Testing different inputs helps identify errors, confirms that both true and false conditions behave as expected, and ensures the script produces reliable results when used in real-world scenarios.

---

**4. How can conditionals help in automation scripts?**

Conditionals help in automation scripts by allowing the script to make decisions based on specific conditions. They enable the script to react differently depending on the situation, such as checking if a file exists, verifying a service is running, or validating user input. This makes automation more reliable, flexible, and capable of handling real-world scenarios without manual intervention.

---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

![Week 3 - Assignment 4 81.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2081.png)

---

#### Screenshot 2 — Output of `./final-automation.sh`

![Week 3 - Assignment 4 82.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2082.png)

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

![Week 3 - Assignment 4 83.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Week%203%20-%20Assignment%204%2083.png)

---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function in Bash is a reusable block of commands grouped together under a single name. Instead of writing the same code multiple times, you can place it inside a function and call it whenever needed. This makes scripts easier to organize, maintain, and reuse.

---

**2. Why are functions useful in scripts?**

Functions are useful in scripts because they allow you to reuse the same set of commands whenever needed without rewriting the code. This makes scripts shorter, easier to read, maintain, and troubleshoot. Functions also help organize scripts into smaller, more manageable sections, improving efficiency and reducing errors.

---

**3. Which functions did you create in this script?**

In this script, I created four functions: print_header(), print_user_details(), check_files(), and print_tools(). The print_header() function displays the assignment title and formatting lines, while print_user_details() prints my name and assignment information. The check_files() function verifies that the required directory and file exist and displays the results of those checks. Finally, the print_tools() function loops through the tools array and prints each tool. Using functions helped organize the script into smaller sections, making it easier to read, maintain, and reuse.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

This final script combines several important Bash concepts into one program. It uses variables to store details such as my name, assignment title, and file paths. It uses an array to store a list of tools and a loop to go through each tool and display it. The script includes conditionals (if-else) to check whether the required file and directory exist and to display the appropriate message based on the result. It works with files and directories by validating their existence before proceeding. Finally, it uses functions to organize related tasks into reusable sections, making the script cleaner, easier to read, and more efficient. Together, these features demonstrate how Bash can be used to automate tasks in a structured and manageable way.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

[LinkedIn Post URL](https://www.linkedin.com/posts/abraham-aigbokhan-3abb28214_devops-linux-bash-ugcPost-7485121049366392832-VvNB/?utm_source=share&utm_medium=member_desktop&rcm=ACoAADZFnjMBb3DIPPRNvWnnHBks2D59TA5vDHw)

---

#### Screenshot — Published LinkedIn post

![Screenshot 2026-07-21 010100.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-03-linux-and-bash-for-devops/screenshots/assignment-05/Screenshot%202026-07-21%20010100.png)

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- ✅ Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- ✅ Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- ✅ Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- ✅ Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- ✅ Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- ✅ Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- ✅ Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- ✅ Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- ✅ All scripts run without errors
- ✅ Full Name visible in all required screenshots
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

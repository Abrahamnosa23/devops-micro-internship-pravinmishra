# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 0 — Output of git remote -v and git branch showing the new branch

![Assignment 6 Screenshot 0.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-04-git-and-github/screenshots/Assignment-06/Assignment%206%20Screenshot%200.png)

---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**


A dedicated feature branch is used to keep the assignment changes isolated from the main branch, ensuring that the stable codebase remains protected while the work can be developed, tested, reviewed, and safely merged through the standard Pull Request process.

---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

![Assignment 6 Screenshot 1.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-04-git-and-github/screenshots/Assignment-06/Assignment%206%20Screenshot%201.png)

---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

Add your answer here.

---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

![Assignment 6 Screenshot 2.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-04-git-and-github/screenshots/Assignment-06/Assignment%206%20Screenshot%202.png)

---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

![Assignment 6 Screenshot 3.png](https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/blob/main/week-04-git-and-github/screenshots/Assignment-06/Assignment%206%20Screenshot%203.png)

---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

hooks/pre-commit is tracked so the hook is version-controlled and shareable. Everyone who clones the repository gets the same security checks, while hooks is local-only, untracked, and is not copied when the repository is cloned.

---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

PreToolUse intercepts a tool request before an AI agent executes it, while hooks/pre-commit intercepts a Git commit before Git creates it. Both act as preventative gates, they inspect a proposed action, apply predefined rules, and can block the action before it causes changes.

---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file



---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The hook matched the secret_pattern line, secret_pattern="(api[_-]?key|secret|password|token|access[_-]?key)[[:space:]]*[:=][[:space:]]*[\"'][^\"']+[\"']"
It matched because the file contained, API_KEY="sk-test-example-..."
The pattern is case-insensitive and recognizes API_KEY, followed by =, and a quoted non-empty value.

---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

Not necessarily. The hook only detects known secret-like names such as api_key, secret, password, token, or access_key followed by a quoted value. A variable with an unusual name, such as config_value, could store a secret without matching the pattern. This shows that fixed rules are predictable and useful for common cases, but they cannot understand context or reliably detect every secret. They should be combined with careful human review and, where appropriate, more advanced secret-scanning tools.

---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`



---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement



---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

/pr-ready has Bash and Read so it can inspect the staged Git diff and analyze the changes. It does not have Write because it must remain read-only and should not modify files, commit changes, push code, or create a pull request.

---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

The skill is intended only to inspect and analyze staged changes. Removing Write permissions ensures it cannot modify files, commit code, push changes, or take actions on my behalf.
Not exactly. The pre-commit hook detected the fake secret because it matched a predefined pattern. The AI skill also identified the secret but could additionally point out issues such as debug statements, mixed-purpose changes, poor naming, or unclear intent that are difficult to capture with fixed rules.

---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)



---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description



---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I removed the fake hardcoded secret and deleted the leftover debug statement from the file. After staging the corrected version, the pre-commit hook no longer detected any violations and allowed the commit to proceed.

---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)



---

#### PR Link



---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I reviewed the AI-generated draft and adjusted the wording to accurately reflect my implementation. I added missing context about the pre-commit hook and removed details that were not relevant to my specific changes.

---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

The draft could contain incorrect assumptions, missing information, or descriptions that do not accurately represent the changes. This could confuse reviewers and reduce trust in the pull request.

---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

The assignment is for personal practice and verification. Opening the PR against my fork prevents assignment-specific files from being submitted to the shared class repository where they do not belong.

---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

The pre-commit hook scans staged files and the /pr-ready skill reads the staged diff. Both are gathering information from the pending changes.

---

**2. Which step(s) represent Analyze?**

The hook analyzes files against predefined security rules, while the AI skill analyzes the staged diff for risks, context, and PR readiness.

---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

Human Act occurs when I decide how to fix issues, run git commit, push the branch, and open the pull request. These actions should remain under human control because they affect the repository state and require accountability.

---

**4. Which step is Verify?**

Verification occurs when I rerun the pre-commit checks, rerun /pr-ready, confirm the commit succeeds, and review the final pull request before submission.

---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

The hook provides consistent enforcement of known security rules, while the AI skill provides context-aware review and judgment. Together they cover both predictable risks and issues that require interpretation.

---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

https://lnkd.in/p/excshrMD

---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

- Pre-commit hooks can prevent security issues before code is committed.
- AI review complements but does not replace deterministic security controls.
- Least-privilege principles apply to AI skills just as they do to users.
- Human approval remains critical for commits, pushes, and pull requests.
- The Agentic Loop helps structure secure and responsible automation.

---

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/Abrahamnosa23/devops-micro-internship-pravinmishra/

---

# Completion Checklist

- ✅ Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- ✅ `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- ✅ `core.hooksPath` configured to point at `hooks/`
- ✅ Pre-commit hook shown blocking the risky commit
- ✅ `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- ✅ `/pr-ready` run against the risky diff and shown flagging issues
- ✅ Risky file fixed; `git commit` succeeds cleanly
- ✅ `/pr-ready` re-run showing a clean report and drafted PR title/description
- ✅ Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- ✅ Agentic Loop mapping (Task 7) completed in your own words
- ✅ LinkedIn post published and URL submitted
- ✅ All required screenshots added
- ✅ GitHub repository URL provided

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

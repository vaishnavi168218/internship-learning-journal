# TDS – Git & GitHub Setup (Session 5 Notes)

**Course:** Tools in Data Science  
**Session Focus:** Git & GitHub fundamentals for TDS coursework  
**Key Topics:** Git installation, GitHub repositories, SSH keys, cloning, commits, push errors, Copilot  
**Session Type:** Live hands-on setup and troubleshooting

---

## Session Objectives
- Understand whether assignments can be completed without watching videos
- Learn why proper tool setup is essential for TDS
- Set up Git and GitHub correctly for long-term coursework
- Use SSH for secure GitHub authentication
- Handle common Git and GitHub errors confidently
- Push locally generated code to GitHub repositories

---

## 1. Course Structure and Tooling Expectations
- Watching session videos is strongly recommended to avoid setup and conceptual gaps
- Assignments depend heavily on:
  - Correct Git and GitHub configuration
  - Linux / WSL familiarity
  - Proper Python environment management
- Early and correct tool setup prevents repeated failures later in the course

---

## 2. Git Installation and Initial Setup
- Installed Git on the local system
- Verified installation using:
  ```bash
  git --version
  ```
- Configured Git identity:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your-email@example.com"
  ```
- Importance:
  - Required for making commits
  - Ensures correct attribution on GitHub

---

## 3. Creating a Repository on GitHub
- Created a new repository using the GitHub web interface
- Added basic files such as README or placeholders
- Understood differences between public and private repositories for coursework

---

## 4. SSH-Based GitHub Authentication
### Why SSH?
- Avoids repeated username/password prompts
- Required after GitHub removed password-based authentication
- More secure and reliable for long-term usage

### SSH Key Generation
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

- SSH keys stored in:
  ```bash
  ~/.ssh/
  ```

### Adding SSH Key to GitHub
- Copied public key:
  ```bash
  cat ~/.ssh/id_ed25519.pub
  ```
- Added key in:
  GitHub → Settings → SSH and GPG keys

---

## 5. Cloning Repository Using SSH
- Cloned repository using:
  ```bash
  git clone git@github.com:username/repo-name.git
  ```
- Troubleshot common issues:
  - Permission denied (publickey)
  - SSH key not added to GitHub
  - Using HTTPS instead of SSH URL

---

## 6. Working Locally with Git
- Added new files locally
- Checked repository status:
  ```bash
  git status
  ```
- Staged changes:
  ```bash
  git add .
  ```
- Committed changes:
  ```bash
  git commit -m "Initial commit"
  ```

---

## 7. Pushing Changes to GitHub
- Pushed commits to GitHub:
  ```bash
  git push origin main
  ```
- Troubleshot push errors:
  - No permission to push
  - Incorrect remote URL
  - Repository ownership or access issues

---

## 8. Why Linux / WSL Is Recommended
- Most production systems run on Linux
- Git, Python, and deployment tools behave more predictably
- WSL provides a real Linux environment on Windows
- Avoids issues caused by Windows-specific file systems

---

## 9. Python Environments with UV (Introduction)
- Introduced UV for:
  - Project isolation
  - Faster dependency management
- Reinforced the importance of consistent environments across projects

---

## 10. Introduction to GitHub Copilot
- Overview of Copilot as an AI coding assistant
- Copilot helps with:
  - Boilerplate code
  - Faster iteration and prototyping
- Warning:
  - Code must be understood before use
  - Blind copying leads to learning gaps and interview failures

---

## 11. Pushing Generated Code to GitHub
- Generated code locally (manual or AI-assisted)
- Verified correctness before committing
- Followed proper Git workflow to push code to GitHub

---

## Key Learning Outcome
This session built a strong foundation in Git and GitHub usage, enabling confident version control, secure authentication, effective collaboration, and error handling required throughout the TDS course.

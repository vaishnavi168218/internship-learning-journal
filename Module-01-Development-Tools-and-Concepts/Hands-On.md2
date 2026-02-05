# Installing WSL & Ubuntu on Windows
## Tools in Data Science (TDS) Bootcamp – Session 2

This document contains the complete hands-on activity and learnings from Session 2 of the TDS Bootcamp, focused on setting up a Linux development environment using Windows Subsystem for Linux (WSL).

---

## Hands-On: WSL & Ubuntu Setup

### Objective
- Install and configure WSL 2 with Ubuntu
- Manage Linux distributions
- Understand Linux–Windows file system integration
- Prepare the environment for Git and future TDS work

---

### Step 1: Open PowerShell as Administrator
PowerShell was opened in Administrator mode to manage WSL configurations.

---

### Step 2: Check Existing WSL Distributions
```bash
wsl --list --verbose
```

Observation:
- Multiple Ubuntu distributions were present
- All distributions were using WSL version 2

---

### Step 3: Shut Down All WSL Instances
```bash
wsl --shutdown
```

This safely stopped all running WSL environments.

---

### Step 4: Remove Unused Ubuntu Distribution
```bash
wsl --unregister Ubuntu
```

This removed the older Ubuntu installation completely.

---

### Step 5: Verify Remaining Distributions
```bash
wsl --list
```

Result:
- Ubuntu 24.04 remained
- It was set as the default distribution

---

### Step 6: Set WSL 2 as Default
```bash
wsl --set-default-version 2
```

This ensures all future Linux installations use WSL 2.

---

### Step 7: Launch Ubuntu
```bash
wsl
```
or
```bash
ubuntu
```

On first launch:
- A Linux username was created
- A password was configured

---

### Step 8: Update Linux Packages
```bash
sudo apt update
sudo apt upgrade
```

This keeps the system stable and avoids compatibility issues.

---

### Step 9: Understand File System Structure
- Linux home directory:
```bash
/home/username
```

- Windows C drive mounted at:
```bash
/mnt/c
```

This allows seamless access to Windows files from Linux.

---

### Step 10: Install and Configure Git
```bash
sudo apt install git
```

Verify installation:
```bash
git --version
```

Configure Git:
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

## Conclusion
WSL with Ubuntu provides a lightweight and efficient Linux development environment on Windows. This setup forms the foundation for Linux-based tooling, Git usage, and deployment workflows throughout the TDS course.


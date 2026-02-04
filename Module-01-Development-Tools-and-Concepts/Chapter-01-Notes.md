# TDS Bootcamp – Session 1 (04 Jan 2026)

## Session Overview
- **Course:** Tools in Data Science (TDS)
- **Session:** Bootcamp – Session 1
- **Focus:** Linux for Data Science
- **Key Areas:** WSL2 setup, Linux CLI basics, development environment management
- **Reference Video:** https://youtu.be/CpN8MjOZ-iI

---

## Purpose of the Session
- Understand why Linux is mandatory for Data Science and MLOps
- Prepare a Linux-based environment before starting TDS coursework
- Develop a deployment-first mindset from the beginning

---

## Core Concepts Covered

### 1. Why Linux is Mandatory for Data Science
- Most servers, containers, and production systems run on Linux
- TDS assignments and evaluations require a Linux environment
- Windows-only setups lead to compatibility and deployment issues
- Early Linux exposure reduces future debugging effort

---

### 2. Computing Analogy (Car Analogy)
- Tools must be understood before effective usage
- Knowing system internals improves troubleshooting skills
- Focus on fundamentals rather than shortcuts

---

### 3. MLOps and Deployment Mindset
- Deployment should be planned before model training
- Data science includes more than building models
- Real-world workflows involve:
  - Environment setup
  - Reproducibility
  - Deployment and maintenance

---

### 4. Environment Choices
- **WSL2 (Windows Subsystem for Linux 2)**
  - Recommended for Windows users
  - Lightweight and well-integrated
- **Virtual Machines**
  - Heavier but useful for isolation
- **Dual Boot**
  - Risky and not recommended
- **macOS**
  - Unix-based by default
  - Uses Homebrew for package management

---

### 5. Hardware and BIOS Requirements
- Hardware virtualization must be enabled in BIOS
- Required for:
  - WSL2
  - Docker
  - Virtual Machines
- Intel VT-x or AMD-V support is mandatory

---

##  WSL2 and Ubuntu Setup

### Installation Highlights
- Installed WSL2 with Ubuntu as the Linux distribution
- Configured Linux username and password
- Restarted system to resolve installation issues

### Post-Installation Steps
- Updated system packages immediately:
```bash
sudo apt update
sudo apt upgrade

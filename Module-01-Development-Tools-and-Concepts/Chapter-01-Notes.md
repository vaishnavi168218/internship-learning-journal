# TDS Bootcamp – Session 1 (Linux for Data Science)

## Session Overview
- **Course:** Tools in Data Science (TDS)
- **Session:** Bootcamp – Session 1
- **Primary Focus:** Linux fundamentals for Data Science
- **Reference Video:** (https://youtu.be/B7iHBHCruCc?si=2OkuIVoslibxB6nM)

---

## Purpose of the Session
- Explain the role of Linux in Data Science and MLOps
- Prepare students with a mandatory Linux environment
- Introduce a deployment-first approach to problem solving

---

## Why Linux is Mandatory
- Most production systems and servers run on Linux
- Containers and cloud platforms are Linux-based
- TDS assignments are designed for Linux environments
- Windows-only setups cause compatibility and deployment issues
- Early Linux exposure reduces debugging effort later

---

## Deployment-First Mindset
- Data science is more than training models
- Deployment should be planned before model development
- Real-world workflows include:
  - Environment setup
  - Version control
  - Reproducibility
  - Deployment and monitoring

---

## Environment Options Explained
- **WSL2 (Windows Subsystem for Linux 2)**
  - Recommended for Windows users
  - Lightweight and well-integrated
- **Virtual Machines**
  - Provide isolation but are resource-heavy
- **Dual Boot**
  - Risky and not recommended
- **macOS**
  - Unix-based by default
  - Uses Homebrew for package management

---

## Hardware and BIOS Requirements
- Hardware virtualization must be enabled
- Required for WSL2, Docker, and VMs
- Intel VT-x or AMD-V support is necessary

---

## Linux File System Overview
- Root directory (`/`) is the base of the file system
- User files are stored under `/home`
- Windows drives are mounted under `/mnt`
- Linux paths are case-sensitive
- Uses forward slashes (`/`) instead of backslashes

---

## ⌨️ Command Line Basics
- Navigation using terminal commands
- Understanding working directories
- Use of pipelines to chain commands
- Importance of CLI for automation and efficiency

---

## Windows and Linux Integration
- Linux files can be accessed from Windows Explorer
- WSL provides seamless file sharing between systems
- Enables smooth development workflow across environments

---

## Troubleshooting and System Management
- Linux distributions can be uninstalled and reinstalled if corrupted
- WSL installations can be moved to another drive
- Export and import options help create backups
- Restarting the system often resolves setup issues

---

## Session Summary
This session establishes the foundational importance of Linux, introduces environment choices, and prepares students for production-oriented data science workflows required throughout the TDS course.


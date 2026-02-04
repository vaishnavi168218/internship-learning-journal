# TDS Bootcamp – Session 1  
## Hands-On: Linux & WSL2 Setup

## 1. System Preparation
- Opened **Turn Windows features on or off**
- Enabled:
  - Windows Subsystem for Linux
  - Virtual Machine Platform
  - Windows Hypervisor Platform
- Restarted the system

---

## 2. Installing WSL2 and Ubuntu
- Opened **PowerShell as Administrator**
- Installed WSL and default Ubuntu:
```bash
wsl --install
Ensured WSL2 is the default version:
wsl --set-default-version 2

3. Initial Ubuntu Configuration
-Launched Ubuntu from Start Menu
-Created Linux username (no spaces/special characters)
-Set Linux password

4. Post-Installation Update
-Updated and upgraded system packages:
sudo apt update
sudo apt upgrade

5. Command Line Practice
Navigated directories using terminal commands
Identified current working directory
Explored Linux directory structure:
-/
-/home
-/mnt/c
6. Windows–Linux File Access
-Accessed Linux files via Windows Explorer:
-\\wsl$\Ubuntu
7. WSL Management & Troubleshooting

Learned how to:
-Uninstall and reinstall Linux distributions
-Reset WSL if corrupted
-Export WSL distributions for backup
-Import distributions when needed
-Move WSL installation to another drive (e.g., D:)

Hands-On Outcome
-Successfully installed WSL2 with Ubuntu
-Verified Linux terminal access
-Completed system updates
-Gained familiarity with Linux CLI and file system




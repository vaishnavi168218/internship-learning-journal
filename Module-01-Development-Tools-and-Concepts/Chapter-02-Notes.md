# Installing WSL & Ubuntu on Windows  
## TDS Bootcamp – Session 2

## What is WSL?
WSL (Windows Subsystem for Linux) allows users to run a Linux environment directly on Windows without using virtual machines or dual booting.

It enables:
- Running Linux commands on Windows
- Using Linux tools alongside Windows applications
- Maintaining a seamless development workflow

---

## System Requirements
- Windows 10 (version 2004 or later) or Windows 11  
- Administrator access  
- Active internet connection  

---

## Step-by-Step Installation of WSL & Ubuntu

### Step 1: Open Windows PowerShell
Open **PowerShell as Administrator**.

You should see:
Windows PowerShell
Copyright (C) Microsoft Corporation.
All rights reserved.


---

### Step 2: Check Existing WSL Distributions
Run the following command:
```bash
wsl --list --verbose
Observed output:
NAME            STATE     VERSION
Ubuntu          Stopped   2
Ubuntu-24.04    Stopped   2
This indicates:
-Multiple Ubuntu distributions are installed
-Both are running on WSL version 2

Step 3: Shut Down All WSL Instances
wsl --shutdown
This safely stops all running WSL environments.

Step 4: Remove Unused Ubuntu Distribution
wsl --unregister Ubuntu
Output:
Unregistering.
The operation completed successfully.
This completely removes the old Ubuntu installation.

Step 5: Verify Remaining Distributions
wsl --list
Output:
Windows Subsystem for Linux Distributions:
Ubuntu-24.04 (Default)
Ubuntu 24.04 is now set as the default distribution.

Step 6: Ensure WSL 2 is the Default Version
wsl --set-default-version 2
Output:
The operation completed successfully.
This confirms that all future Linux installations will use WSL 2.
Launching Ubuntu
Run either of the following commands:
wsl
or
ubuntu
On first launch, you will be prompted to create:
-A Linux username
-A password

Common Troubleshooting
Issue: wsl command not found

Fix:
wsl --install
Restart the system after installation.
Issue: Ubuntu not visible in Installed Apps
Ubuntu can still function through WSL even if it does not appear as a standard Windows app.
Check installed distributions using:
wsl --list

Introduction to Git (Inside Ubuntu)
Install Git
sudo apt update
sudo apt install git

Verify Git Installation
git --version

Configure Git
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
This configuration is required for commits and GitHub usage.

Reference Video
This hands-on setup was performed by following the tutorial below:
YouTube Link:
https://youtu.be/RoRy1jKewhA


Hands-On Guide: Installing WSL & Ubuntu on Windows
📌 What is WSL?
WSL (Windows Subsystem for Linux) allows users to run a Linux environment directly on Windows without using virtual machines or dual booting.
It enables:
-Running Linux commands on Windows
-Using Linux tools alongside Windows apps
-Seamless development workflow

System Requirements
Windows 10 (version 2004+) or Windows 11
Administrator access
Internet connection
🧑‍💻 Step-by-Step Installation of WSL & Ubuntu
🔹 Step 1: Open Windows PowerShell
Open PowerShell as Administrator.
You should see:
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.
🔹 Step 2: Check Existing WSL Distributions
Run:
wsl --list --verbose
📌 Output observed:
NAME            STATE           VERSION
* Ubuntu          Stopped         2
  Ubuntu-24.04    Stopped         2
✔ This shows:
Multiple Ubuntu distributions installed
Both running on WSL version 2
🔹 Step 3: Shut Down All WSL Instances
wsl --shutdown
✔ This safely stops all running WSL environments.
🔹 Step 4: Remove Unused Ubuntu Distribution
wsl --unregister Ubuntu
📌 Output:
Unregistering.
The operation completed successfully.
✔ This removes the old Ubuntu installation completely.
🔹 Step 5: Verify Remaining Distributions
wsl --list
📌 Output:
Windows Subsystem for Linux Distributions:
Ubuntu-24.04 (Default)
✔ Ubuntu 24.04 is now the default distribution.
🔹 Step 6: Ensure WSL 2 is Default
wsl --set-default-version 2
📌 Output:
The operation completed successfully.
✔ Confirms that all future Linux installations will use WSL 2.

🐧 Launch Ubuntu
Run:
wsl
or
ubuntu
On first launch:
You’ll be asked to create:
Linux username:vaish
Password
📂 Understanding File System
Linux Home:
/home/username
Windows Drive Access:
C: → /mnt/c
This allows easy file sharing between Windows and Linux.
🔧 Common Troubleshooting
❌ Issue: WSL command not found
Fix:
wsl --install
Restart the system after installation.
❌ Issue: Ubuntu not visible in Installed Apps
✔ Ubuntu can still work via WSL, even if it doesn’t appear as a normal Windows app.
Use:
wsl --list


Introduction to Git (Inside Ubuntu)
🔹 Install Git
sudo apt update
sudo apt install git

🔹 Verify Git Installation
git --version

🔹 Configure Git
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"


✔ Required for commits and GitHub usage.

🎥 Reference Video

This hands-on setup was performed by following the tutorial:

🔗 A hands-on guide to installing and setting up Windows Subsystem for Linux (WSL) and Ubuntu, including troubleshooting and an introduction to Git
📺 YouTube Link:
https://youtu.be/RoRy1jKewhA?si=WHVhlOx61Q4lQrBt

✅ Key Learnings
-Understood WSL and its purpose
-Installed Ubuntu using WSL 2
-Managed multiple Linux distributions
-Learned basic WSL troubleshooting

Installed and configured Git inside Ubuntu

📌 Conclusion
WSL with Ubuntu provides a powerful Linux development environment within Windows, making it ideal for data science, development, and version control workflows.

# 📘 Tools in Data Science – Session 4 Notes
**Topic:** Development Environment Setup for Data Science & AI  
**Session:** Week 1 – Session 4  
**Platform:** macOS / Linux (Applicable to WSL on Windows)  

---

## 🎯 Session Objective
- Set up a clean, reproducible, and efficient development environment
- Avoid common Python, dependency, and version conflicts
- Prepare system for data science and AI workflows

---

## 🛠️ Tools Covered
- VS Code
- Git & GitHub
- GitHub Copilot
- Homebrew
- pyenv (Python version manager)
- UV (Fast project & dependency manager)
- GitHub CLI
- LLM CLI tools (Gemini)

---

## 🧩 Environment Setup Steps

### 1️⃣ VS Code Installation
- Download from official site
- Move app from Downloads to Applications folder
- Ensures proper updates and system integration
- Install extensions later (Copilot, Python, etc.)

---

### 2️⃣ GitHub Education & Copilot
- Claimed GitHub Education Pack
- Enabled Copilot Pro access
- Installed GitHub Copilot extension in VS Code
- Logged in using student GitHub account

---

### 3️⃣ Homebrew Installation
- Installed Homebrew as system package manager
- Enabled installing tools via terminal

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
Added Homebrew to PATH
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

4️⃣ Python Version Management with pyenv

-Installed pyenv using Homebrew

-Installed build dependencies

-Installed latest Python version

-Avoided system Python conflicts
brew install pyenv
brew install openssl readline sqlite3 xz zlib tcl-tk
env PYTHON_CONFIGURE_OPTS="--enable-framework" pyenv install 3.12.11

Set Python version per project (recommended)
pyenv local 3.12.11
5️⃣ Project & Dependency Management using UV

Installed UV (fast replacement for pip + venv)

-Created Python projects easily

-Managed dependencies efficiently

curl --proto '=https' --tlsv1.2 -LsSf https://install.uv.io | sh
uv init my_project
uv add flask
uv remove flask
6️⃣ GitHub CLI Setup

Installed GitHub CLI to manage repositories via terminal

brew install gh

Created and pushed repository directly from CLI

git init
git add .
git commit -m "Initial commit"
gh repo create username/repo-name --public --source=. --remote=origin --push

7️⃣ Python Version Isolation per Project

-Used pyenv local inside each project folder

-Ensured project-specific Python consistency

-Prevented dependency and version clashes

8️⃣ LLM Command Line Tool Setup

Installed LLM CLI tool

Integrated Gemini model for AI tasks

llm install llm-gemini
llm keys set gemini YOUR_API_KEY
llm -m gemini-1.5-flash "What is 4+2?"


Explored CLI-based AI workflows

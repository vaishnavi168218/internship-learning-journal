# Live Session Notes – Git, WSL, GitHub Codespaces, Hugging Face Spaces & GitHub Actions

## Session Overview
This session focused on modern development workflow including:
- Proper Git usage inside WSL
- VS Code Remote WSL setup
- Cloud development using GitHub Codespaces
- Deploying applications using Hugging Face Spaces
- Automation using GitHub Actions

---

# 1. Git, WSL and VS Code Setup

## Key Clarifications

- Git configuration and SSH keys exist in the environment where Git runs.
- If using WSL → configure Git and SSH inside WSL.
- Virtual environments created in Windows are not compatible with WSL.
- Best practice: Perform Git, Docker, Python installs, and development inside WSL.

## SSH Setup Example (Inside WSL)

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
ssh-keygen -t ed25519 -C "your@email.com"
```

## Best Practice Workflow

1. Clone repository inside WSL  
2. Open folder in VS Code using Remote – WSL extension  
3. Create virtual environment inside WSL  
4. Install dependencies inside WSL  

Avoid mixing Windows and WSL environments.

---

# 2. GitHub Codespaces

## What It Is
Cloud-hosted development environment that runs VS Code in the browser or desktop.

## Why Use It
- No local setup required
- Identical environment for entire team
- Solves “works on my machine” problem
- Supports multiple hardware configurations (2–32 cores, 8–128GB RAM)

## Free Tier Limits
- 120 core-hours/month (Free)
- 180 core-hours/month (Pro/Student)
- 30 minutes idle timeout

## Configuration Files

```
.devcontainer/devcontainer.json
Dockerfile (optional)
```

## devcontainer.json Defines:
- Base image
- VS Code extensions
- Pre-installed tools
- Forwarded ports
- postCreateCommand

Example structure:

```json
{
  "name": "My Dev Container",
  "image": "mcr.microsoft.com/devcontainers/python:3.11",
  "postCreateCommand": "pip install -r requirements.txt",
  "forwardPorts": [8000]
}
```

## Use Cases
- Quick onboarding
- Consistent team environments
- Temporary high-performance machines
- Avoid dependency conflicts

---

# 3. Hugging Face Spaces

## Purpose
Deploy ML demos, FastAPI apps, Gradio or Streamlit projects easily.

## Deployment Methods
1. Git repository + Dockerfile (flexible)
2. Gradio/Streamlit templates (quick setup)

## Workflow

```bash
git clone <space_repo>
git add .
git commit -m "Update"
git push
```

Push triggers build and deployment automatically.

## Important Notes
- Free CPU tier sleeps after ~48 hours inactivity
- Use Git LFS for files >100MB
- Do not push virtual environments or large datasets

## Minimal Dockerfile Example

```dockerfile
FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "main.py"]
```

Best for public ML demos and prototypes.

---

# 4. GitHub Actions

## What It Is
Automation and CI/CD system inside GitHub.

## Workflow Location

```
.github/workflows/workflow.yml
```

## Common Triggers

- push
- pull_request
- workflow_dispatch (manual)
- schedule (cron jobs)

## Example Workflow

```yaml
name: Daily Task

on:
  schedule:
    - cron: '0 12 * * *'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: echo "Automation running"
```

## Real-World Use Cases

- Run tests on pull requests
- Deploy to Hugging Face / Vercel after merge
- Scheduled data collection
- Auto-assign reviewers
- Build documentation
- Update JSON/data files automatically

---

# Summary Table

| Tool | Purpose | Key Files | Limits | Best Use Case |
|------|---------|----------|--------|---------------|
| GitHub Codespaces | Cloud dev environment | .devcontainer/devcontainer.json | 120–180 core-hours/month | Onboarding, consistent setup |
| Hugging Face Spaces | Deploy ML demos | Dockerfile | Sleeps after ~48h | Public ML apps |
| GitHub Actions | Automation & CI/CD | .github/workflows/*.yml | Free minutes quota | Testing, deployment, scheduling |

---

# Instructor’s Key Advice

- Do development inside WSL, not Windows.
- Use VS Code Remote – WSL extension.
- Keep repositories small (<1–2GB).
- Never commit data, virtual environments, or node_modules.
- Use Git LFS for large files.
- Monitor Codespaces and Actions usage quotas.

---

# Overall Workflow Learned

Local Development (WSL)  
→ Cloud Development (Codespaces)  
→ Deployment (Hugging Face Spaces)  
→ Automation (GitHub Actions)  

Complete modern DevOps-enabled development pipeline.

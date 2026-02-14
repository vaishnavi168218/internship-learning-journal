# Hands-On: WSL Setup, GitHub Codespaces, Hugging Face Spaces & GitHub Actions

## Objective
- Set up proper Git workflow inside WSL
- Use GitHub Codespaces for cloud development
- Deploy a FastAPI app to Hugging Face Spaces
- Automate tasks using GitHub Actions

---

# Step 1: Proper Git Setup Inside WSL

## Open WSL Terminal

Configure Git:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Generate SSH key:

```bash
ssh-keygen -t ed25519 -C "your@email.com"
cat ~/.ssh/id_ed25519.pub
```

Add the SSH key to GitHub → Settings → SSH Keys.

Clone repository using SSH:

```bash
git clone git@github.com:username/repo.git
cd repo
```

Open in VS Code (Remote WSL):

```bash
code .
```

Create virtual environment inside WSL:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

---

# Step 2: Use GitHub Codespaces

## Create Codespace

1. Go to your GitHub repository  
2. Click Code → Codespaces → Create Codespace  

VS Code opens in browser.

## Configure Dev Container

Create folder:

```
.devcontainer/devcontainer.json
```

Example configuration:

```json
{
  "name": "Python Dev Environment",
  "image": "mcr.microsoft.com/devcontainers/python:3.11",
  "postCreateCommand": "pip install -r requirements.txt",
  "forwardPorts": [8000]
}
```

Commit and push:

```bash
git add .
git commit -m "Add devcontainer config"
git push
```

Codespace rebuilds automatically.

---

# Step 3: Deploy FastAPI App to Hugging Face Spaces

## Create Minimal FastAPI App (main.py)

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Hello from Hugging Face Space"}
```

## Create requirements.txt

```
fastapi
uvicorn
```

## Create Dockerfile

```dockerfile
FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "7860"]
```

## Create Hugging Face Space

1. Go to huggingface.co → Create Space  
2. Choose Docker option  
3. Clone the Space repository  

```bash
git clone https://huggingface.co/spaces/username/space-name
cd space-name
```

Copy project files into this folder.

Commit and push:

```bash
git add .
git commit -m "Deploy FastAPI app"
git push
```

Hugging Face automatically builds and deploys.

Access:
```
https://huggingface.co/spaces/username/space-name
```

---

# Step 4: Automate with GitHub Actions

## Create Workflow Folder

```
.github/workflows/
```

Create file:

```
.github/workflows/daily.yml
```

## Example Scheduled Workflow

```yaml
name: Daily Automation

on:
  schedule:
    - cron: '0 12 * * *'
  workflow_dispatch:

jobs:
  run-script:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run script
        run: echo "Automation successful"
```

Commit and push:

```bash
git add .
git commit -m "Add GitHub Action"
git push
```

Check execution:
GitHub → Actions tab.

---

# Step 5: Monitor Usage & Best Practices

- Keep repositories small (<1–2GB)
- Do not commit:
  - virtual environments
  - large datasets
  - node_modules
- Use Git LFS for files >100MB
- Monitor Codespaces monthly usage
- Be mindful of Hugging Face Space sleep after inactivity

---

# Practiced On

- Configured Git correctly inside WSL
- Used VS Code Remote WSL
- Created cloud dev environment using Codespaces
- Defined reproducible environment using devcontainer.json
- Built and containerized FastAPI app
- Deployed app using Hugging Face Spaces
- Automated workflow using GitHub Actions
- Understood CI/CD basics

---

# Final Workflow

Local Dev (WSL)  
→ Cloud Dev (Codespaces)  
→ Containerized Deployment (Hugging Face Spaces)  
→ Automation (GitHub Actions)  

Complete modern development and deployment pipeline.

#Git, WSL, Codespaces & GitHub Actions

---

## Experiment 1 — Open WSL Terminal in VS Code

### What I Did
Switched from the default PowerShell terminal in VS Code to a WSL
(Ubuntu) terminal and verified that Git configurations made inside
WSL are available in the VS Code terminal.

### Steps I Followed
```
1. Open VS Code
2. Open Terminal panel (Ctrl + `)
3. Click the dropdown arrow next to the + icon
4. Select WSL from the list
5. A new terminal opens with Ubuntu prompt
```

### What I Observed
```bash
# WSL terminal prompt looks like this
username@machine:/mnt/c/Users/you$

# Verify you are in WSL
uname -a
# Output: Linux ... (confirms Linux/WSL environment)

# Check current directory
pwd
```

### Key Observation
```
PowerShell prompt: PS C:\Users\you>
WSL prompt:        username@machine:/mnt/c$

They are completely different environments.
Git configs set in WSL don't exist in PowerShell and vice versa.
```

### Also Installed
```
Extensions → Search "WSL" → Install WSL by Microsoft
This connects VS Code fully to WSL environment


---

## Experiment 2 — Configure Git Inside WSL

### What They Did
Set up Git configuration and SSH key inside WSL terminal so that
all GitHub operations (clone, push, pull) work without passwords.

### Commands They Ran
```bash
# Step 1 — Set Git identity
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Step 2 — Generate SSH key
ssh-keygen -t ed25519 -C "your@email.com"
# Press Enter for all prompts (use defaults)

# Step 3 — View the public key
cat ~/.ssh/id_ed25519.pub
# Copy the entire output
```

### Steps on GitHub
```
1. Go to github.com → Settings
2. SSH and GPG Keys → New SSH Key
3. Title: WSL Machine (or any name)
4. Paste the public key
5. Save
```

### How They Verified It Worked
```bash
# Test SSH connection to GitHub
ssh -T git@github.com
# Output: Hi username! You've successfully authenticated.
```

### Key Observation
```
One SSH key setup in WSL → works for ALL your GitHub repositories
You never need to enter a password again for git push/pull


---

## Experiment 3 — Virtual Environment in WSL

### What They Did
Demonstrated that virtual environments created in PowerShell
(Windows) do NOT work in WSL. Showed the correct way to create
and activate a virtual environment inside WSL.


### What They Did to Fix It
```bash
# Inside WSL terminal — delete the broken venv
rm -rf venv

# Create new venv inside WSL
python3 -m venv venv

# Activate — WSL/Linux way
source venv/bin/activate

# Prompt changes to show venv is active
(venv) username@machine:$

# Reinstall from requirements.txt
pip install -r requirements.txt
```

### Key Observation
```
Windows venv activation:  venv\Scripts\activate      ← only works in PowerShell
WSL/Linux venv activation: source venv/bin/activate  ← only works in WSL

Never mix the two.


---

## Experiment 4 — Create a GitHub Codespace

### What They Did
Created a new GitHub repository and launched a Codespace from it,
showing how a cloud VS Code environment opens in the browser with
the repo already cloned inside.

### Steps They Followed
```
1. Go to github.com → New Repository
2. Name: codespaces-demo
3. Visibility: Public
4. Click Create Repository

5. On the repo page → click green Code button
6. Go to Codespaces tab
7. Click Create codespace on main
8. Select machine type: 2-core (default)
9. Select region: nearest to you
10. Wait ~1 minute for environment to spin up
```

## Experiment 5 — Configure Dev Container

### What They Did
Created a `.devcontainer` folder with two files — a `Dockerfile`
and `devcontainer.json` — to define a reproducible cloud development
environment. Any new Codespace created from this repo automatically
gets the configured tools and extensions.

### Folder Structure I Created
```
codespaces-demo/
└── .devcontainer/
    ├── devcontainer.json
    └── Dockerfile
```

### devcontainer.json I Used
```json
{
  "name": "TDS Dev Container",
  "build": {
    "dockerfile": "Dockerfile"
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-python.python",
        "charliermarsh.ruff"
      ]
    }
  },
  "postCreateCommand": "pip install -r requirements.txt"
}
```

### Dockerfile We Used
```dockerfile
FROM python:3.11
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
```

### How To Committ It
```bash
git add .devcontainer/
git commit -m "Add dev container config"
git push
```

### What Happens When Someone Creates a New Codespace
```
GitHub reads .devcontainer/devcontainer.json
→ Builds image from Dockerfile
→ Installs Python extensions in VS Code
→ Runs postCreateCommand (pip install -r requirements.txt)
→ Environment is ready with everything pre-installed
→ No manual setup needed by the new developer

---

## Experiment 6 — Multiple Dev Container Configs

### What They Did
Showed that one repository can have multiple different dev container
configurations — for example one for developers and one for testers.
When creating a Codespace, GitHub asks which config to use.

### Folder Structure They Created
```
.devcontainer/
├── devcontainer.json          ← default config (shown first)
└── g-container.json           ← alternate config for different team
```

### Second Config I Added (g-container.json)
```json
{
  "name": "Testing Environment",
  "build": {
    "dockerfile": "Dockerfile"
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-python.python"
      ]
    }
  },
  "postCreateCommand": "pip install pytest"
}
---

## Experiment 7 — Deploy FastAPI to Hugging Face

### What They Did
Created a simple FastAPI "Hello World" app, added a Dockerfile,
pushed it to Hugging Face Spaces, and shared the live URL for
others in the session to access.

### Files They Created

**requirements.txt**
```
fastapi
uvicorn
```

**app.py**
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello World"}
```

**Dockerfile**
```dockerfile
FROM python:3.11

RUN useradd -m -u 1000 user
USER user
ENV HOME=/home/user \
    PATH=/home/user/.local/bin:$PATH

WORKDIR $HOME/app

COPY --chown=user requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY --chown=user . .

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```

### Steps To Be Followed on Hugging Face
```
1. huggingface.co → New Space
2. Name: hugging-face-demo
3. SDK: Docker → Blank template
4. Hardware: CPU Basic (free)
5. Visibility: Public
6. Create Space

7. Clone the space locally:
   git clone https://huggingface.co/spaces/USERNAME/hugging-face-demo

8. Copy app.py, requirements.txt, Dockerfile into the cloned folder

9. Push:
   git add .
   git commit -m "Simple FastAPI app"
   git push
   (Username: HF username, Password: HF token)
```

### How They Generated the HF Token
```
huggingface.co → Settings → Access Tokens → New Token
Give write access → Copy token → use as password when pushing
```

### What We Observed
```
After push → Space starts building (takes ~1-2 minutes)
→ Build logs visible in the Space page
→ App goes live at: https://USERNAME-hugging-face-demo.hf.space
→ Visiting the URL returns: {"message": "Hello World"}
```
---

## Experiment 8 — ISS Tracker with GitHub Actions

### What They Did
Created a GitHub Actions workflow that runs daily at 12 PM UTC,
fetches the current coordinates of the International Space Station
from a public API, and saves them to a `.jsonl` file in the repo —
all automatically without any human involvement.

### Folder Structure
```
your-repo/
└── .github/
    └── workflows/
        └── test.yml
```

### Workflow File They Created (test.yml)
```yaml
name: ISS Location Tracker

on:
  schedule:
    - cron: '0 12 * * *'    # Every day at 12:00 PM UTC
  workflow_dispatch:          # Allow manual trigger

jobs:
  track:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: pip install requests

      - name: Fetch ISS location
        run: |
          python -c "
          import requests, json
          from datetime import datetime
          r = requests.get('http://api.open-notify.org/iss-now.json').json()
          entry = {
            'timestamp': datetime.utcnow().isoformat(),
            'lat': r['iss_position']['latitude'],
            'lon': r['iss_position']['longitude']
          }
          with open('iss_log.jsonl', 'a') as f:
              f.write(json.dumps(entry) + '\n')
          "

      - name: Commit and push results
        run: |
          git config user.name "github-actions"
          git config user.email "actions@github.com"
          git add iss_log.jsonl
          git commit -m "Update ISS location" || echo "No changes"
          git push
```

### What I Observed After Running
```
Actions tab → workflow ran successfully
→ iss_log.jsonl appeared in the repo (they didn't create it)
→ File was created BY the GitHub Action itself
→ Contents looked like:
  {"timestamp": "2024-10-01T12:00:01", "lat": "23.45", "lon": "78.12"}

---

## Experiment 9 — Trigger GitHub Action Manually

### What They Did
Demonstrated the `workflow_dispatch` trigger which allows running
a workflow manually from the GitHub Actions tab — without needing
to push code or wait for a scheduled time.

### Steps They Followed
```
1. Go to GitHub repo → Actions tab
2. Click the workflow name on the left sidebar (ISS Location Tracker)
3. Click Run workflow button (top right of the run list)
4. Click the green Run workflow button in the dropdown
5. Watch a new row appear showing the workflow is queued/running
6. Click on the running workflow → see live logs for each step
---

## Experiment 10 — GitHub Action on Push

### What We Did
Modified the workflow trigger from schedule-only to also fire
on every push to the main branch — demonstrating how CI/CD
pipelines work in real team projects.

### What They Changed in the YAML
```yaml
# Before — only runs on schedule and manual trigger
on:
  schedule:
    - cron: '0 12 * * *'
  workflow_dispatch:

# After — also runs on every push to main
on:
  schedule:
    - cron: '0 12 * * *'
  workflow_dispatch:
  push:
    branches:
      - main
```

###  CI/CD Use Cases Explaination
```
Push trigger use case 1 — Run tests automatically:
  Developer pushes code → Action runs pytest
  → All tests pass → merge allowed
  → Any test fails  → merge blocked

Push trigger use case 2 — Auto deploy:
  Developer pushes to main → Action deploys to Hugging Face
  → No manual push to HF needed
  → One push to GitHub triggers everything

Pull request trigger use case:
  Someone opens a PR → Action checks code quality
  → Passes → reviewer is notified
  → Fails  → author must fix before review
```






# 🧠 Dev Tools — Core Concepts
---

## 1. WSL (Windows Subsystem for Linux)

| | |
|---|---|
| **Full form** | Windows Subsystem for Linux |
| **Type** | Compatibility layer |
| **Default distro** | Ubuntu |

### What it is
WSL lets you run a full Linux (Ubuntu) environment inside Windows — no dual boot, no virtual machine needed.

### Why it matters
Most dev tools, cloud servers, and production environments run on Linux. Developing in WSL means what works on your machine will work on a server too. PowerShell behaves differently from Linux — WSL bridges that gap.

### Mental Model
> Think of it as having **two operating systems on one laptop** — Windows for everyday use, Ubuntu for all your development work.

### Key Rule
```
✅ Always install Git, Python, Docker, Ollama — everything — inside WSL
❌ Never install dev tools in PowerShell or Windows CMD
```

---

## 2. Virtual Environments

| | |
|---|---|
| **Tool** | `python3 -m venv` |
| **Purpose** | Isolate project dependencies |
| **Scope** | Per project |

### What it is
An isolated Python installation specific to one project — with its own packages, completely separate from your system Python and other projects.

### Why it matters
Different projects often need different versions of the same library. Without isolation, they conflict and break each other.

### Mental Model
> Think of it like **separate lunchboxes** — each project carries only its own food and never mixes with others.

### Critical Warning
```
⚠️  A virtual environment created in PowerShell (Windows) will NOT work in WSL.
✅  Always create and activate your venv from inside WSL terminal.
```

```bash
# ✅ Correct (inside WSL)
python3 -m venv venv
source venv/bin/activate

# ❌ Wrong in WSL (this is Windows syntax)
venv\Scripts\activate
```

---

## 3. Git vs GitHub

> These are two completely different things — commonly confused.

| | Git | GitHub |
|---|---|---|
| **What** | Version control tool | Cloud hosting platform |
| **Runs on** | Your local machine | Internet (cloud) |
| **Purpose** | Tracks file changes over time | Hosts & shares Git repos |
| **Without internet** | ✅ Works offline | ❌ Needs internet |

### Git
A tool that runs locally and records every change you make to your project files — like a detailed undo history for your entire codebase.

### GitHub
A website that stores your Git repositories in the cloud so teams can collaborate, review code, and manage projects together.

### Mental Model
> **Git** = Microsoft Word's Track Changes feature  
> **GitHub** = Google Drive that stores and shares the document

### Other Git Hosting Platforms
```
GitHub     → most popular, owned by Microsoft
GitLab     → popular in enterprises
Hugging Face → specialized for ML models & datasets
```

---

## 4. SSH Keys

| | |
|---|---|
| **Type** | Cryptographic key pair |
| **Algorithm** | ed25519 (recommended) |
| **Purpose** | Passwordless authentication |

### What it is
A pair of keys — **public** and **private** — used to prove your identity to remote services like GitHub or Hugging Face without typing a password each time.

### How it works
```
Your Machine                    GitHub
─────────────                   ──────────────
🔑 Private Key   ◄──────────►  🔒 Public Key (lock)
   (kept secret)                (you gave this to GitHub)

When you connect → GitHub checks if your private key
                   matches the public key (lock) on file.
```

### Mental Model
> The **public key is a padlock** you give to GitHub.  
> The **private key is the only key** that opens it — and it never leaves your machine.

### Per-Platform Keys
```
GitHub       → needs its own SSH key (or token)
Hugging Face → needs its own SSH key (or token)

💡 You can use the same key for both, but separate keys are preferred.
   Name them clearly: github_ed25519, huggingface_ed25519
```

---

## 5. Git Branching

| | |
|---|---|
| **Default branch** | `main` (or `master`) |
| **Purpose** | Parallel, isolated development |
| **When to use** | New features, bug fixes, experiments |

### What it is
A branch is a separate, independent copy of your codebase. You work on it freely without affecting the main stable version. When ready, you merge it back.

### Why it matters
- Build new features without breaking working code
- Multiple people work on different things simultaneously
- If something breaks on a branch, `main` is safe

### Mental Model
```
main ──────────────────────────────────────► (stable, production-ready)
          │                       ▲
          └──► feature-branch ────┘
               (your new work)
```

### When You Need Branches
```
✅ Collaborating with multiple people
✅ Working on multiple features at the same time
✅ Experimenting with something that might break

❌ Solo projects with simple linear work → branching optional
```

---

## 6. Containers & Docker

| | |
|---|---|
| **Tool** | Docker |
| **Output** | Container (running instance of an image) |
| **Base file** | `Dockerfile` |

### What it is
A container packages your application along with **everything it needs to run** — OS libraries, dependencies, config — into one portable unit that behaves identically anywhere.

### Why it matters
Eliminates the classic **"works on my machine"** problem. The same container runs identically on your laptop, your teammate's machine, and any cloud server.

### Container vs Virtual Machine

| | Container | Virtual Machine |
|---|---|---|
| **Size** | Lightweight (MBs) | Heavy (GBs) |
| **Startup** | Seconds | Minutes |
| **OS** | Shares host OS kernel | Full separate OS |
| **Isolation** | Process level | Hardware level |

### Mental Model
> A container is like a **shipping container** — it holds everything needed for the goods inside, and can be loaded onto any ship (server) anywhere in the world.

### Dockerfile
The recipe that defines what goes into your container:
```dockerfile
FROM python:3.11          # Start with this base image
WORKDIR /app              # Set working directory inside container
COPY requirements.txt .   # Copy your dependency list
RUN pip install -r requirements.txt   # Install dependencies
COPY . .                  # Copy your code
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]  # Start command
```

---

## 7. GitHub Codespaces

| | |
|---|---|
| **Type** | Cloud-hosted development environment |
| **Based on** | Docker containers |
| **Default OS** | Ubuntu Linux |
| **Access** | Browser, VS Code, or CLI |

### What it is
A full VS Code-like development environment running entirely on GitHub's servers — not on your local machine. You open a browser and your complete configured workspace is ready.

### Why it matters
- New team member can contribute in **minutes** — no local setup
- Environment is defined as code → everyone gets identical setup
- Works from any device (tablet, old laptop, etc.)

### Mental Model
> Instead of spending a day setting up your laptop for a new job,  
> you open a browser and your entire configured workspace is already there.

### Free Tier

| Account | Free Hours/Month | Notes |
|---|---|---|
| Free GitHub | 120 hours | |
| GitHub Student Pack | 180 hours | Apply at education.github.com |

```
⚠️  Hours are multiplied by core count
    2-core machine  → 1 real hour = 2 quota hours
    4-core machine  → 1 real hour = 4 quota hours
```

### Lifecycle
```
Created     → Environment spins up (~1 min)
Inactive    → Auto shuts down after 30 minutes
Not used    → Auto deleted after 30 days
```

---

## 8. devcontainer.json

| | |
|---|---|
| **Location** | `.devcontainer/devcontainer.json` |
| **Format** | JSON |
| **Used by** | GitHub Codespaces, VS Code Dev Containers |

### What it is
A configuration file that tells Codespaces (or VS Code) **exactly how to set up a development environment** — which Docker image to use, which extensions to install, which commands to run after setup.

### Why it matters
Makes environments **reproducible**. Any developer who opens this project gets the exact same setup automatically — no manual installation steps.

### Mental Model
> Think of it as a **recipe card** — it tells the kitchen (cloud/machine) exactly what ingredients and steps are needed to prepare your workspace.

### Structure in Repo
```
your-repo/
├── .devcontainer/
│   ├── devcontainer.json     ← VS Code settings + extensions + commands
│   └── Dockerfile            ← what software to install
├── requirements.txt
└── app.py
```

### Multiple Configs (for Teams)
```
.devcontainer/
├── dev-team/
│   └── devcontainer.json     ← full dev setup
└── testing-team/
    └── devcontainer.json     ← minimal testing setup
```
> When creating a Codespace, GitHub asks which config to use.

---

## 9. Hugging Face Spaces

| | |
|---|---|
| **Website** | huggingface.co |
| **Purpose** | Host & deploy ML models and web apps |
| **Version control** | Git (same commands as GitHub) |
| **Free hardware** | CPU Basic (2 vCPU, 16 GB RAM) |

### What it is
A free platform for deploying and sharing machine learning models and web applications publicly. Under the hood, it uses the same Git commands as GitHub.

### Why it matters
Makes it easy to share a **live, working demo** of your AI project with anyone in the world — without needing your own server or cloud account.

### GitHub vs Hugging Face

| | GitHub | Hugging Face Spaces |
|---|---|---|
| **Hosts** | Source code | Running applications + ML models |
| **Purpose** | Code collaboration | App deployment & model sharing |
| **Large files** | ❌ (max 100 MB) | ✅ via Git LFS (model weights in GBs) |

### Mental Model
> **GitHub** = your workshop where you build things  
> **Hugging Face Spaces** = the storefront where people try and use what you built

### Inactivity Policy
```
Free tier → Space shuts down after 48 hours of inactivity
           Restarts automatically when someone visits the URL
```

---

## 10. GitHub Actions & CI/CD

| | |
|---|---|
| **Config file** | `.github/workflows/*.yml` |
| **Format** | YAML |
| **Triggers** | push, pull_request, schedule, manual |
| **Runs on** | GitHub's cloud servers |

### What it is
An automation system built into GitHub. You write a YAML file describing steps, and GitHub executes them automatically when certain events happen.

### CI — Continuous Integration
Every time someone pushes code, **automated tests run** to check nothing is broken before the code is merged into main.

```
Developer pushes code → GitHub Actions runs tests → 
   ✅ Tests pass → merge allowed
   ❌ Tests fail → merge blocked, fix required
```

### CD — Continuous Deployment
Once code passes all tests, it **automatically deploys** to production without any manual steps.

```
Code merged to main → GitHub Actions deploys → 
   App is live on Hugging Face / cloud server
```

### Why it matters
- Catches bugs **before** they reach production
- Removes manual, error-prone deployment steps
- Enforces code quality standards in team projects

### Mental Model
> Think of it as a **robot assistant** — whenever you submit new work,  
> the robot automatically runs quality checks, and if everything passes,  
> ships it to production for you.

### Common Use Cases

| Use Case | Trigger |
|---|---|
| Run automated tests | Every `git push` |
| Auto-deploy to Hugging Face | Push to `main` branch |
| Fetch & save data daily | Cron schedule |
| Auto-assign PR reviewers | On pull request opened |
| Build documentation | On push to docs branch |

---

## 11. Git LFS (Large File Storage)

| | |
|---|---|
| **Full form** | Large File Storage |
| **Regular Git limit** | 100 MB per file |
| **Use case** | ML model weights, datasets, media |

### What it is
An extension to Git that handles large files by storing them separately and keeping only a **lightweight pointer** in your Git history.

### Why it matters
Git was designed for source code (small text files). ML model weights and datasets are often **gigabytes** — regular Git can't handle them. LFS solves this.

### Mental Model
> Instead of putting a **heavy suitcase in your Git history**,  
> LFS gives you a **luggage tag** (pointer) in the history  
> and stores the actual suitcase in a separate warehouse.

### File Size Reference

| Platform | Regular Limit | With LFS |
|---|---|---|
| GitHub | 100 MB per file | Up to 2 GB per file |
| GitHub total | 15 GB per account | — |
| Hugging Face | Uses LFS by default for model weights | Several GB |

---

## 🔗 How Everything Connects

```
┌─────────────────────────────────────────────────────┐
│             Your Local Machine (WSL)                │
│                                                     │
│  Code Editor (VS Code)  +  Terminal (WSL/Ubuntu)    │
│               │                                     │
│         git push / pull                             │
└───────────────┼─────────────────────────────────────┘
                │
                ▼
┌─────────────────────────────────────────────────────┐
│                   GitHub Repository                 │
│                                                     │
│   ┌─────────────┐  ┌──────────────┐  ┌──────────┐  │
│   │   Codespaces │  │    Actions   │  │   Pages  │  │
│   │  (cloud dev) │  │  (automate)  │  │  (docs)  │  │
│   └─────────────┘  └──────┬───────┘  └──────────┘  │
└────────────────────────────┼────────────────────────┘
                             │
                    auto-deploy on push
                             │
                             ▼
┌─────────────────────────────────────────────────────┐
│              Hugging Face Spaces                    │
│                                                     │
│         🌐 Your live app, accessible to anyone      │
└─────────────────────────────────────────────────────┘
```




*TDS Dev Tools & Deployment Session — Concept Reference*

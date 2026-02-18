# 💡 Key Learnings — Dev Tools & Deployment Session

---

## 1. WSL & Local Setup

### ✅ Do everything inside WSL — not Windows
The single most important learning from this session. Git, Python, Docker, virtual environments — all of it should live inside WSL/Ubuntu. The moment you mix Windows and WSL installations, things break and debugging becomes confusing.

### ✅ VS Code is just a text editor with a terminal
VS Code itself has no special powers. Its terminal is what matters. If your terminal is WSL, all your WSL configurations apply. If it's PowerShell, they don't. Always switch your terminal to WSL inside VS Code.

### ✅ Installing something doesn't care about your current folder
When you install a package in WSL (e.g., `pip install`, `apt install`), it installs into the Linux filesystem regardless of which folder you're currently in. Your current working directory (`pwd`) only affects where files are created — not where programs are installed.

### ✅ WSL mounts your Windows drives
Your Windows C drive is accessible inside WSL at `/mnt/c/`. You can read and write files across both environments interchangeably — but keep your dev work inside WSL's own filesystem for consistency.

---

## 2. Git & GitHub

### ✅ Git is not GitHub — they are separate things
Git is a local tool. GitHub is a cloud platform. You can use Git without GitHub (offline version control). GitHub uses Git as its underlying technology. Confusing the two leads to confusion about what commands do what.

### ✅ One SSH key in WSL works for all your GitHub repos
You don't need a new key per repository. One setup covers everything cloned and pushed from that WSL environment. But each platform (GitHub, Hugging Face) needs its SSH key added to that platform separately.

### ✅ Tokens replace passwords when pushing
When pushing to GitHub or Hugging Face via HTTPS, you use a **personal access token** instead of your account password. Generate it from Settings → Access Tokens and treat it like a password — don't share it.

### ✅ Three ways to connect to GitHub — all do the same thing
CLI, GitHub Desktop, and the web UI all offer the same functionality. Learn one properly rather than partially knowing all three. CLI is the most powerful and transferable skill.

### ✅ Branching is needed for collaboration — optional for solo work
If you're working alone on a straightforward project, you don't necessarily need branches. But the moment you collaborate or work on multiple features simultaneously, branches become essential.

---

## 3. Virtual Environments

### ✅ Never install packages globally
Every project should have its own virtual environment. Global installations cause version conflicts between projects and are hard to debug. This is industry best practice — not just a suggestion.

### ✅ Windows venv ≠ WSL venv
A virtual environment created via PowerShell uses Windows paths and activation scripts. It simply won't work when you try to activate it inside WSL. If this happens — delete the venv, open a WSL terminal, and recreate it there using `requirements.txt`.

### ✅ requirements.txt is your venv's backup
Your virtual environment folder should never be committed to GitHub (add `venv/` to `.gitignore`). Instead, keep a `requirements.txt`. Anyone can recreate your exact environment from it with `pip install -r requirements.txt`.

---

## 4. GitHub Codespaces

### ✅ Codespaces solves the "setup problem" for teams
The biggest friction when someone joins a new project is environment setup — installing the right Python version, dependencies, extensions, etc. Codespaces eliminates this entirely. The environment is defined in code and reproduced automatically.

### ✅ devcontainer.json + Dockerfile = reproducible environment
These two files are the heart of Codespaces. The Dockerfile defines what gets installed. The JSON file defines VS Code settings, extensions, and post-setup commands. Together they ensure every developer gets an identical workspace.

### ✅ Watch your quota — core count multiplies hours used
Free accounts get 120 hours/month. But a 4-core machine burns 4 quota hours per real hour. For learning and small projects, always use the 2-core machine to stretch your free quota.

### ✅ Codespace shuts down after 30 minutes of inactivity
This is by design — to save your quota. Your work is saved (committed files remain in the repo). Uncommitted changes in the workspace survive a shutdown but are lost if the Codespace is deleted (after 30 days).

### ✅ You can have multiple dev container configs for different teams
One repo can have different container setups for developers, testers, and reviewers. Each gets only the tools they need — nothing more, nothing less.

---

## 5. Hugging Face Spaces

### ✅ Hugging Face uses the same Git commands as GitHub
`git clone`, `git push`, `git pull` — identical syntax. The only difference is the remote URL (huggingface.co instead of github.com) and authentication (HF token instead of GitHub token). If you know GitHub, you already know how to use Hugging Face.

### ✅ Docker is what makes deployment on HF work
When you select Docker as your SDK on Hugging Face Spaces, you need a `Dockerfile` in your repo. That file defines exactly how your app runs. Without it, your Space won't build.

### ✅ Port 7860 is the default port for Hugging Face apps
Hugging Face Spaces expects your app to run on port `7860`. Always set `--port 7860` in your Dockerfile's CMD. Using any other port will cause the app to not be accessible.

### ✅ Free Spaces shut down after 48 hours of inactivity
Unlike GitHub Codespaces (30 min), Hugging Face gives you 48 hours before sleeping. The app restarts automatically when someone visits the URL. No data is lost — the container just restarts.

### ✅ Files over 100 MB need Git LFS
GitHub blocks files over 100 MB. Hugging Face uses Git LFS by default for large model weights. If you're working with datasets or model files, set up Git LFS before committing those files.

---

## 6. GitHub Actions

### ✅ GitHub Actions is automation — not just for big companies
It feels like an advanced topic but even simple projects benefit. Auto-running tests on push, auto-deploying to Hugging Face, or fetching data daily — all achievable with a single YAML file.

### ✅ The folder structure is non-negotiable
Your workflow file must live at exactly `.github/workflows/your-file.yml`. The folder names must be exact — `.github` (with the dot) and `workflows` (plural). Any deviation and GitHub won't detect the action.

### ✅ YAML indentation matters — a lot
YAML is indentation-sensitive. One wrong space and the entire workflow fails to parse. Always use spaces (not tabs) and be consistent with indentation levels (2 spaces is standard).

### ✅ Triggers control everything
The `on:` block in your YAML determines when the action runs. You can trigger on `push`, `pull_request`, a `schedule` (cron), or `workflow_dispatch` (manual). You can combine multiple triggers in one workflow.

### ✅ CI/CD removes human error from deployment
Manually deploying is error-prone — wrong branch, missed step, wrong environment. GitHub Actions makes deployment a repeatable, automated process. Push to main → tests run → if passing → deploys automatically. No human steps in between.

### ✅ GitHub Actions runs on GitHub's servers — not yours
The `runs-on: ubuntu-latest` line means GitHub spins up a fresh Ubuntu machine to execute your steps. Nothing runs on your laptop. This is why it works even when your machine is off.

---

## 🔭 Big Picture Learnings

### The tools form a complete workflow
Each tool in this session solves a specific part of the developer workflow:

```
Problem                          Solution
───────────────────────────────────────────────────
Windows ≠ Linux environment  →   WSL
Dependency conflicts         →   Virtual Environments
Tracking code changes        →   Git
Sharing and collaborating    →   GitHub
Team onboarding friction     →   GitHub Codespaces
Deploying apps publicly      →   Hugging Face Spaces
Automating repetitive tasks  →   GitHub Actions
Large file handling          →   Git LFS
```

### Cloud tools don't replace local skills — they extend them
Codespaces, Hugging Face, and GitHub Actions all run Linux under the hood. The same terminal commands you use in WSL work in all of these environments. Learning WSL properly is learning all of these environments at once.

### Git is the common thread across everything
Every single tool in this session — GitHub, Codespaces, Hugging Face Spaces, GitHub Actions — uses Git as its foundation. Push, pull, clone, commit — these commands work across all platforms. Mastering Git is the highest-leverage skill here.

### Reproducibility is the goal
The entire point of Dockerfiles, devcontainer.json, requirements.txt, and GitHub Actions is making your work **reproducible** — by others, on other machines, in the future. A project that only works on your machine isn't a finished project.

---


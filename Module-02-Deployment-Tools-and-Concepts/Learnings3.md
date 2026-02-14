# Learnings – Git, WSL, Codespaces, Hugging Face Spaces & GitHub Actions

## 1. Git & WSL Best Practices

- Development tools (git, python, docker) should run inside WSL.
- Git configuration and SSH keys must be set up in the environment where git is executed.
- Virtual environments created in Windows are not compatible with WSL.
- Use VS Code Remote – WSL extension for proper Linux-based development workflow.
- Avoid mixing Windows paths and WSL paths.

---

## 2. GitHub Codespaces

- Codespaces provides a cloud-hosted development environment.
- Solves “works on my machine” problems through reproducible environments.
- Development environments are defined using `.devcontainer/devcontainer.json`.
- Supports custom images, extensions, forwarded ports, and post-setup commands.
- Has usage limits based on core-hours per month.
- Useful for onboarding, team consistency, and temporary high-performance machines.

---

## 3. Hugging Face Spaces

- Spaces allow deployment of ML or web applications via Git push.
- Dockerfile-based deployment provides maximum flexibility.
- Free CPU tier sleeps after inactivity.
- Git LFS is required for files larger than 100MB.
- Do not push virtual environments, datasets, or unnecessary large files.
- Deployment workflow is similar to GitHub (clone → commit → push).

---

## 4. GitHub Actions (Automation & CI/CD)

- Workflows are stored inside `.github/workflows/`.
- YAML-based configuration defines jobs and triggers.
- Supports triggers such as:
  - push
  - pull_request
  - schedule (cron)
  - workflow_dispatch
- Used for testing, deployment, automation, and scheduled tasks.
- Enables CI (Continuous Integration) and CD (Continuous Deployment).

---

## 5. Overall Workflow Understanding

Local Development (WSL)
→ Cloud Development (Codespaces)
→ Deployment (Hugging Face Spaces)
→ Automation (GitHub Actions)

Complete modern DevOps-enabled development pipeline learned.

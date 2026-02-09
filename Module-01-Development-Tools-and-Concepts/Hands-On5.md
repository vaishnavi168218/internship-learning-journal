# Hands-On: Git & GitHub Setup (TDS)

## 1. Verify Git Installation
```bash
git --version
```

---

## 2. Configure Git (One-Time Setup)
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Verify:
```bash
git config --global --list
```

---

## 3. Generate SSH Key for GitHub
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

Press **Enter** for all prompts.

Check key files:
```bash
ls ~/.ssh
```

---

## 4. Add SSH Key to GitHub
Copy public key:
```bash
cat ~/.ssh/id_ed25519.pub
```

Steps on GitHub:
- GitHub → Settings
- SSH and GPG keys
- New SSH key
- Paste key → Save

Test connection:
```bash
ssh -T git@github.com
```

Expected:
```
Hi username! You've successfully authenticated.
```

---

## 5. Create Repository on GitHub
- Go to GitHub → New repository
- Name repo
- Choose Public/Private
- Do NOT initialize with README (for clean setup)

---

## 6. Clone Repository Using SSH
```bash
git clone git@github.com:username/repo-name.git
cd repo-name
```

---

## 7. Create Files Locally
```bash
touch README.md
```

Edit file:
```bash
nano README.md
```

(Add content, save, exit)

---

## 8. Check Git Status
```bash
git status
```

---

## 9. Stage Files
```bash
git add .
```

---

## 10. Commit Changes
```bash
git commit -m "Initial commit"
```

⚠️ Do NOT use:
```bash
git commit -an "message"
```

---

## 11. Push to GitHub
```bash
git push origin main
```

(If branch is master)
```bash
git push origin master
```

---

## 12. Fix Common Push Errors

### Error: Permission denied (publickey)
✔ SSH key not added → repeat Step 4

### Error: Repository not found
✔ Check repo name and SSH URL

### Error: No upstream branch
```bash
git push -u origin main
```

---

## 13. Verify on GitHub
- Refresh repository page
- Confirm files and commits are visible

---

## 14. Optional: GitHub Copilot Setup
- Install GitHub Copilot extension in VS Code
- Sign in with GitHub account
- Use AI suggestions carefully (understand code before committing)

---

## Hands-On Completed Successfully
You now have:
- Git installed and configured
- SSH authentication working
- Local-to-remote Git workflow
- Ability to push TDS assignments confidently

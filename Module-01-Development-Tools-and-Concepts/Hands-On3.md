## Hands-On: WSL, Linux CLI & LLM Tool Setup
### TDS Bootcamp – Session 3

This section documents the practical tasks performed during Session 3 using WSL and Ubuntu on Windows.

---

### Task 1: Verify WSL Environment
Checked that Ubuntu was running under WSL 2.

```bash
wsl --list --verbose
```

Confirmed that Ubuntu distribution was active and using WSL version 2.

---

### Task 2: Launch Ubuntu in WSL
Started the Linux environment.

```bash
wsl
```

Verified successful login into Ubuntu shell.

---

### Task 3: Basic Linux Navigation
Practiced essential Linux commands for file system navigation.

```bash
pwd
ls
cd ~
mkdir tds_session3
cd tds_session3
touch test.txt
ls
```

---

### Task 4: Understanding Paths
Verified absolute and relative paths.

```bash
pwd
cd ..
cd ./tds_session3
cd /home/username/tds_session3
```

Learned usage of `.`, `..`, and `~` for directory navigation.

---

### Task 5: Access Windows Files from Linux
Navigated Windows C drive from Ubuntu.

```bash
cd /mnt/c
ls
```

Confirmed seamless file access between Windows and Linux.

---

### Task 6: Integrate VS Code with WSL
Opened project folder in VS Code using WSL integration.

```bash
code .
```

Verified that:
- VS Code terminal was connected to Ubuntu
- Files were edited in Linux environment

---

### Task 7: Install UV Tool
Installed the UV package manager inside Ubuntu.

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Verified installation.

```bash
uv --version
```

---

### Task 8: Install LLM CLI Tool
Installed LLM tool using UV.

```bash
uv tool install llm
```

Installed Gemini plugin.

```bash
llm install llm-gemini
```

---

### Task 9: Configure API Keys

#### Gemini API Key
```bash
llm keys set gemini
```

#### OpenAI / AI-Pipe API Key
```bash
llm keys set openai
```

Configured custom endpoint.

```bash
export OPENAI_BASE_URL="https://ai-pipe.tds/token/..."
source ~/.bashrc
```

---

### Task 10: Use LLM from Terminal
Executed LLM queries directly from the Linux terminal.

```bash
llm "Explain WSL in simple terms"
llm -m gemini-1.5-flash "Explain Linux file system"
llm -m gpt-4o-mini "Write a Python script to read a CSV file"
```

Verified that responses were returned successfully in terminal.

---

### Outcome
- Successfully navigated Linux using CLI
- Installed and configured UV and LLM tools
- Connected Gemini and GPT models to terminal
- Established a production-like Linux + AI workflow

---

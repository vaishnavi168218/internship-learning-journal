# WSL, Linux CLI & LLM Tooling
## Tools in Data Science (TDS) – Session 3

**Reference Video:** https://youtu.be/sXlsRhw5X94  
**Session Focus:** Linux fundamentals in WSL, command-line navigation, and setting up UV & LLM tools to interact with Gemini and GPT models from the terminal.

---

## Session Objectives
- Understand how WSL fits into the computer boot process
- Learn Linux file system navigation and path concepts
- Compare Linux and Windows file systems
- Integrate VS Code with WSL
- Install and use modern CLI tools (UV and LLM)
- Interact with Gemini and GPT models directly from the terminal

---

## 1. WSL and Computer Boot Process

### Key Concepts
- Computer boot flow:
  - BIOS / UEFI initializes hardware
  - Bootloader loads the operating system
  - OS kernel starts system services
- WSL2 runs Linux using a lightweight virtualized kernel on Windows
- Uses Hyper-V backend for near-native performance

### Block Diagram: Boot Process with WSL
```
Power On
   |
BIOS / UEFI
   |
Windows Bootloader
   |
Windows OS
   |
Hyper-V (WSL2)
   |
Linux Kernel (Ubuntu)
   |
User Commands (CLI)
```

---

## 2. Understanding Hypervisors
- Hypervisors manage hardware resources for multiple operating systems
- WSL2 uses a Type-1 hypervisor (Hyper-V)
- More efficient than traditional virtual machines
- Enables Linux tools to run seamlessly on Windows

---

## 3. Navigating Ubuntu File System in WSL

### Basic Commands Practiced
```bash
pwd      # show current directory
ls       # list files
cd       # change directory
touch    # create file
```

- Linux environment behaves like a real server environment
- Files can be accessed from both Linux and Windows

---

## 4. Absolute vs Relative Paths

### Path Types
- **Absolute Path**: Starts from root `/`
  ```bash
  /home/username/project/file.txt
  ```
- **Relative Path**: Based on current directory
  ```bash
  project/file.txt
  ```

### Special Symbols
- `~` → Home directory
- `.` → Current directory
- `..` → Parent directory

---

## 5. Linux vs Windows File Systems

| Linux | Windows |
|------|---------|
| Single root `/` | Multiple drives (C:, D:) |
| Forward slash `/` | Backslash `\` |
| Case-sensitive | Case-insensitive |
| Everything is a file | Separate file abstractions |

### Windows Drives in WSL
```bash
/mnt/c   # Windows C drive
/mnt/d   # Windows D drive
```

---

## 6. Important Linux Directories
```text
/        → Root directory
/home    → User home directories
/mnt     → Mounted drives
/bin     → Core binaries
/usr/bin → User-installed binaries
```

---

## 7. Why Command-Line Tools Matter
- Enables automation and scripting
- Required for servers, cloud, containers, and CI/CD
- Faster and reproducible workflows
- Essential for data science, MLOps, and deployment

---

## 8. VS Code Integration with WSL
- VS Code connects directly to Ubuntu via WSL extension
- Terminal runs inside Linux environment
- Files edited in VS Code behave like native Linux files

### Block Diagram: VS Code + WSL
```
VS Code UI
   |
WSL Extension
   |
Ubuntu Terminal
   |
Linux File System
```

---

## 9. Installing UV Tool

### What is UV
- Fast Python package manager and environment tool
- Modern alternative to pip + venv
- Written in Rust for speed and reliability

### Installation
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Verify:
```bash
uv --version
```

---

## 10. Installing LLM Tool Using UV

### What is LLM
- CLI tool to interact with large language models
- Supports GPT, Gemini, Claude, and others
- Useful for coding, explanations, automation

### Installation
```bash
uv tool install llm
```

Install Gemini plugin:
```bash
llm install llm-gemini
```

---

## 11. Setting Up API Keys

### Gemini API Key
```bash
llm keys set gemini
```

- Key obtained from Google AI Studio
- Personal email recommended

### OpenAI / AI-Pipe Key
```bash
llm keys set openai
```

Set custom endpoint (AI-Pipe proxy):
```bash
export OPENAI_BASE_URL="https://ai-pipe.tds/token/..."
```

Reload config:
```bash
source ~/.bashrc
```

---

## 12. Using LLM from Terminal

### Example Commands
```bash
llm "Explain WSL"
llm -m gemini-1.5-flash "Summarize Linux file systems"
llm -m gpt-4o-mini "Write a Python script to read a CSV"
```

### Block Diagram: LLM CLI Workflow
```
Terminal Command
     |
   LLM CLI
     |
Configured API Key
     |
LLM Provider (Gemini / GPT)
     |
Response in Terminal
```

---


---

## Conclusion
Session 3 established a strong command-line foundation and introduced modern AI tooling inside a Linux environment. This setup enables faster development, automation, and intelligent workflows required throughout the TDS course and real-world data science projects.

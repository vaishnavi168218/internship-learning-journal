## Hands-On: Environment Setup & Tooling (Session 4)

### 1. Install Python Version Manager (pyenv)
```bash
brew install pyenv
brew install openssl readline sqlite3 xz zlib tcl-tk

2. Install Latest Python Version
env PYTHON_CONFIGURE_OPTS="--enable-framework" pyenv install 3.12.11

3. Set Python Version Per Project
pyenv local 3.12.11
python --version

4. Install UV (Fast Dependency & Project Manager)
curl --proto '=https' --tlsv1.2 -LsSf https://install.uv.io | sh

5. Create a New Python Project Using UV
uv init my_project
cd my_project

6. Manage Project Dependencies
uv add flask
uv remove flask

7. Initialize Git Repository
git init
git add .
git commit -m "Initial commit"

8. Install GitHub CLI
brew install gh

9. Create & Push Repository to GitHub
gh repo create username/repo-name --public --source=. --remote=origin --push

10. Install LLM Command Line Tool
llm install llm-gemini

11. Configure Gemini API Key
llm keys set gemini

12. Run LLM from Terminal
llm -m gemini-1.5-flash "What is 4+2?"

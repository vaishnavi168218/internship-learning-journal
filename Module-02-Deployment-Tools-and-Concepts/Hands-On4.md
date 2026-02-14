# Project 1 – Complete Hands-On Implementation Guide

## Objective
Build a FastAPI server that:
- Receives request from IITM server
- Validates secret
- Returns immediate 200 OK
- Processes task within 10 minutes
- Generates web app code
- Creates GitHub repo dynamically
- Pushes code
- Enables GitHub Pages
- Returns final JSON response

---

# Step 1: Project Setup

## Install Dependencies

```bash
pip install fastapi uvicorn python-dotenv requests PyGithub
```

## Project Structure

```
project/
│
├── app.py
├── requirements.txt
├── .env
├── Dockerfile
└── generated_app/
```

---

# Step 2: Store Secret Securely

## .env

```
SECRET_KEY=my_super_secret
GITHUB_TOKEN=your_github_token
```

Never commit `.env`.

---

# Step 3: Basic FastAPI Server

## app.py

```python
from fastapi import FastAPI, BackgroundTasks, HTTPException
from pydantic import BaseModel
import os
from dotenv import load_dotenv
from github import Github

load_dotenv()

app = FastAPI()

SECRET_KEY = os.getenv("SECRET_KEY")
GITHUB_TOKEN = os.getenv("GITHUB_TOKEN")

class TaskRequest(BaseModel):
    secret: str
    task: str

@app.post("/process")
async def process_task(request: TaskRequest, background_tasks: BackgroundTasks):

    # Validate secret
    if request.secret != SECRET_KEY:
        raise HTTPException(status_code=403, detail="Invalid secret")

    # Immediately return 200 OK
    background_tasks.add_task(handle_task, request.task)
    return {"status": "Processing started"}
```

---

# Step 4: Background Task Logic

```python
def handle_task(task_description: str):

    # 1. Call LLM (Pseudo Example)
    generated_code = generate_app_code(task_description)

    # 2. Create GitHub Repo
    g = Github(GITHUB_TOKEN)
    user = g.get_user()
    repo = user.create_repo("tds-generated-app", private=False)

    # 3. Push Files
    repo.create_file("index.html", "Initial commit", generated_code)

    # 4. Enable GitHub Pages
    repo.edit(has_pages=True)

    print("Deployment completed")
```

---

# Step 5: Simple LLM Mock Function

```python
def generate_app_code(task_description: str):
    return f"""
    <html>
        <head><title>Generated App</title></head>
        <body>
            <h1>Task:</h1>
            <p>{task_description}</p>
        </body>
    </html>
    """
```

Replace this with actual LLM API call (OpenAI, Gemini, etc.).

---

# Step 6: Run Locally

```bash
uvicorn app:app --reload
```

Test using curl:

```bash
curl -X POST "http://127.0.0.1:8000/process" \
-H "Content-Type: application/json" \
-d '{"secret":"my_super_secret","task":"Create a calculator app"}'
```

---

# Step 7: Dockerize for Deployment

## Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 7860

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```

---

# Step 8: Deploy to Hugging Face Spaces

1. Create new Space → Choose Docker
2. Push project files
3. Add Secrets in Settings:
   - SECRET_KEY
   - GITHUB_TOKEN
4. Ensure port = 7860

---

# Step 9: Automated Testing Script (Optional but Recommended)

Create `test.sh`:

```bash
curl -X POST https://your-space-url/process \
-H "Content-Type: application/json" \
-d '{"secret":"my_super_secret","task":"Build a todo app"}'
```

Make executable:

```bash
chmod +x test.sh
```

---

# Final Execution Flow

IITM Request
→ Validate Secret
→ Return Immediate 200 OK
→ Background Task Starts
→ Call LLM
→ Generate HTML/CSS/JS
→ Create GitHub Repo
→ Push Code
→ Enable GitHub Pages
→ Send Repo URL + Live URL

All within 10 minutes.

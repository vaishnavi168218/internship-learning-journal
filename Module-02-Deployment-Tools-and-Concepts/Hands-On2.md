# Hands-On: Podman, GitHub Pages, FastAPI, Vercel & ngrok

## Objective
- Understand Podman vs Docker basics
- Deploy a static site using GitHub Pages
- Build a REST API using FastAPI
- Deploy API to Vercel
- Expose local server using ngrok
- Configure environment variables and CORS

---

# Step 1: Install and Test Podman (WSL)

```bash
sudo apt update
sudo apt install podman -y
podman --version
```

Run a test container:

```bash
podman pull nginx
podman run -d -p 8080:80 nginx
```

Open browser:
```
http://localhost:8080
```

Stop container:
```bash
podman ps
podman stop <container_id>
podman rm <container_id>
```

---

# Step 2: Deploy Static Website Using GitHub Pages

## Create Basic Site

Create `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Site</title>
</head>
<body>
  <h1>Hello from GitHub Pages</h1>
</body>
</html>
```

## Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <repo_url>
git push -u origin main
```

## Enable GitHub Pages

1. Go to Repository → Settings → Pages  
2. Select Branch: `main`  
3. Save  

Access:
```
https://username.github.io/repository-name/
```

---

# Step 3: Build FastAPI Application

Install dependencies:

```bash
pip install fastapi uvicorn
```

Create `main.py`:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}

@app.post("/add")
async def add_numbers(a: int, b: int):
    return {"result": a + b}
```

Run locally:

```bash
uvicorn main:app --reload
```

Open:
```
http://127.0.0.1:8000/docs
```

Test GET and POST endpoints.

---

# Step 4: Deploy FastAPI to Vercel

## Install Vercel CLI

```bash
npm install -g vercel
```

## Project Structure

```
project/
 ├── api/
 │    └── index.py
 ├── requirements.txt
 └── vercel.json
```

Move FastAPI code into `api/index.py`.

## requirements.txt

```
fastapi
uvicorn
```

## vercel.json

```json
{
  "version": 2,
  "builds": [{ "src": "api/index.py", "use": "@vercel/python" }],
  "routes": [{ "src": "/(.*)", "dest": "api/index.py" }]
}
```

## Deploy

```bash
vercel
vercel --prod
```

Test deployed endpoint via generated URL.

---

# Step 5: Expose Local Server Using ngrok

Install ngrok.

Run FastAPI locally:

```bash
uvicorn main:app --reload
```

Expose port:

```bash
ngrok http 8000
```

Use generated public HTTPS URL.

---

# Step 6: Manage Environment Variables

## Local (.env file)

Install dotenv:

```bash
pip install python-dotenv
```

Create `.env`:

```
API_KEY=your_secret_key
```

Access in Python:

```python
import os
from dotenv import load_dotenv

load_dotenv()
key = os.getenv("API_KEY")
```

## Vercel

Go to:
Project → Settings → Environment Variables  
Add key-value pairs securely.

---

# Step 7: Enable CORS in FastAPI

Install CORS middleware:

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

Required when frontend and backend are hosted on different domains.


---

# Final Workflow

Container Basics → Static Deployment → API Development → Serverless Deployment → Secure Secrets → Public Exposure → Cross-Origin Configuration

Complete end-to-end modern development workflow.


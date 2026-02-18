# FastAPI & Project 1 Workflow

---

## Part 1 — Project 1 Workflow

### What You Are Building
An **API server** that can receive a task, use an LLM to generate a web application, push it to a GitHub repo, launch GitHub Pages, and report back — all automatically within 10 minutes.

### Step-by-Step Workflow

```
Step 1 → Fill the Google Form
         - Your API endpoint URL
         - Your GitHub repo URL (code for your FastAPI server)
         - Your secret key (a password only you and TDS server know)

Step 2 → TDS server sends a JSON request to your API
         - Contains: task brief + evaluation URL + round number + signature (secret)

Step 3 → Your server immediately responds with HTTP 200 OK
         - This tells TDS: "I received it and I'm alive"
         - Do NOT wait 10 min to respond — respond IMMEDIATELY

Step 4 → A 10-minute timer starts on TDS server

Step 5 → Your server does two things in the background:
         a) Calls an LLM (ChatGPT/Gemini/etc.) with the task brief
            → LLM generates JavaScript/HTML code for a web app
         b) Dynamically creates a NEW public GitHub repo
            → Pushes the generated code to that repo
            → Enables GitHub Pages on that repo

Step 6 → Within 10 minutes, your server sends a POST request BACK to TDS
         - Contains: email, task ID, repo URL, GitHub Pages URL, etc.
         - Format specified on the TDS Project 1 page

Step 7 → TDS evaluates your GitHub Pages URL
         - Checks if the app is live and working as expected
         - This is Round 1

Step 8 → Round 2 (Modification Round)
         - TDS sends a modification request (minor change to the app)
         - Same flow repeats: 200 OK → LLM update → push to same repo → callback
         - Must complete within another 10 minutes
```

### Key Rules
```
✅ Respond with 200 OK immediately — do NOT wait
✅ Create a NEW GitHub repo dynamically per task (not your existing one)
✅ GitHub Pages must be enabled and app must be accessible publicly
✅ Secret key must match what you submitted in the Google Form
✅ Callback request must reach TDS within 10 minutes
✅ Keep your FastAPI server repo public by the deadline (17th October)
✅ The app generated must run entirely on the frontend (JavaScript only)
   — GitHub Pages does not support server-side code
```

### Two Different GitHub Repos
```
Repo 1 (yours, submitted in form):
└── Your FastAPI server code
    ├── app.py
    ├── Dockerfile
    ├── requirements.txt
    └── README.md

Repo 2 (created dynamically by your server per task):
└── LLM-generated web app
    ├── index.html
    └── (any JS/CSS files)
    └── GitHub Pages enabled → live URL
```

---

## Part 2 — FastAPI Basics

### Step 1 — Setup
```bash
# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install fastapi uvicorn python-multipart
pip freeze > requirements.txt
```

### Step 2 — Create app.py
```python
from fastapi import FastAPI

app = FastAPI()
```

### Step 3 — First GET Endpoint (Root)
```python
@app.get("/")
def home():
    return {"message": "Hello from TDS"}
```

### Step 4 — Run the Server
```bash
uvicorn app:app --reload
```
```
app        → filename (app.py)
app        → variable name (app = FastAPI())
--reload   → auto-restarts on file save
```
> Default port: `http://localhost:8000`

### Step 5 — Path Parameters (GET with ID)
```python
item_db = {
    1: {"name": "Apple"},
    2: {"name": "Banana"},
    3: {"name": "Pineapple"}
}

@app.get("/item/{item_id}")
def get_item(item_id: int):
    item = item_db.get(item_id)
    if item:
        return item
    return {"error": "Not found"}
```
```
GET http://localhost:8000/item/1   → {"name": "Apple"}
GET http://localhost:8000/item/99  → {"error": "Not found"}
```

### Step 6 — Query Parameters (Search)
```python
@app.get("/search")
def search_item(q: str):
    results = []
    for item in item_db.values():
        if q.lower() in item["name"].lower():
            results.append(item)
    return results
```
```
GET http://localhost:8000/search?q=apple  → [{"name": "Apple"}]
```

### GET vs POST — Quick Difference
```
GET  → Retrieve/read data     → parameters go in the URL
POST → Send/create data       → data goes in the request body (JSON)
```

---

## Part 3 — Pydantic & Validation

### What Pydantic Does
Automatically validates incoming data types, formats, and constraints — no manual `if/else` checks needed.

### Step 1 — Define a Pydantic Model
```python
from pydantic import BaseModel, EmailStr, Field

class User(BaseModel):
    username: str = Field(min_length=3, max_length=50)
    email: EmailStr
    age: int = Field(lt=120)
```
```bash
# Install email validator for EmailStr
pip install pydantic[email]
```

### Step 2 — Use it in a POST Endpoint
```python
users_db = []

@app.post("/users")
def create_user(user: User):
    users_db.append(user)
    return {"message": "User created", "user": user.dict()}
```

### Step 3 — Response Models (Filter Output)
```python
class UserOut(BaseModel):
    username: str
    email: str
    # age is excluded — won't appear in response

@app.get("/user/{id}", response_model=UserOut)
def get_user(id: int):
    return users_db[id]
```
> Even if the data has more fields, only fields defined in `UserOut` are returned.

---

## Part 4 — File Uploads

### Single File Upload
```python
from fastapi import UploadFile, File

@app.post("/upload-file")
async def upload_file(file: UploadFile = File(...)):
    contents = await file.read()
    return {
        "filename": file.filename,
        "size": len(contents),
        "content_preview": contents[:100].decode("utf-8", errors="ignore")
    }
```

### Multiple File Upload
```python
from typing import List

@app.post("/upload-files")
async def upload_files(files: List[UploadFile] = File(...)):
    file_details = []
    for file in files:
        contents = await file.read()
        file_details.append({
            "filename": file.filename,
            "size": len(contents)
        })
    return {"files": file_details}
```

### How to Test File Upload (Postman)
```
1. Open Postman
2. Method: POST
3. URL: http://localhost:8000/upload-file
4. Body → form-data
5. Key: file  (must match parameter name in code)
6. Type: File (not Text)
7. Value: Select your file
8. Send
```

### How to Test with curl (faster)
```bash
# Single file
curl -X POST http://localhost:8000/upload-file \
  -F "file=@cars.json"

# Multiple files
curl -X POST http://localhost:8000/upload-files \
  -F "files=@cars.json" \
  -F "files=@animals.csv"
```

---

## Part 5 — Secret Keys & .env

### Why Use a .env File?
To keep sensitive data (API keys, passwords) out of your code and out of GitHub.

### Step 1 — Create .env File
```bash
touch .env
```
```env
SECRET_KEY=tds_is_a_very_good_subject
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx
GEMINI_API_KEY=AIzaxxxxxxxxxxxxxxxx
```

### Step 2 — Add .env to .gitignore
```bash
echo ".env" >> .gitignore
```
> ⚠️ Never commit your .env file to GitHub

### Step 3 — Load in Python
```bash
pip install python-dotenv
```
```python
import os
from dotenv import load_dotenv

load_dotenv()

SECRET_KEY = os.getenv("SECRET_KEY")
```

### Step 4 — Use in Endpoint
```python
@app.get("/secret")
def get_secret():
    return {"key": SECRET_KEY}
```

### Step 5 — Verify Secret in Incoming Requests
```python
@app.post("/task")
def receive_task(payload: dict):
    if payload.get("signature") != SECRET_KEY:
        return {"error": "Unauthorized"}, 401
    # Process task...
    return {"status": "ok"}, 200
```

---

## Part 6 — Deploying to Hugging Face

### Step 1 — Create requirements.txt
```bash
pip freeze > requirements.txt
```

### Step 2 — Create Dockerfile
```dockerfile
FROM python:3.11

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 7860

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```
> ⚠️ Hugging Face requires port **7860** — not 8000

### Step 3 — Create Hugging Face Space
```
1. Go to huggingface.co → New Space
2. Name: your-app-name
3. SDK: Docker
4. Hardware: CPU Basic (free)
5. Visibility: Public
6. Click Create Space
```

### Step 4 — Upload Files
```
Go to your Space → Files → Add File → Upload Files
Upload: app.py, requirements.txt, Dockerfile
Commit changes
```

### Step 5 — Add Secret Keys to Hugging Face
```
Space → Settings → Variables and Secrets → New Secret
Name: SECRET_KEY
Value: your_secret_value
Save
```
> This keeps your API keys hidden even though the Space is public

### Step 6 — Get Your Deployment URL
```
https://YOUR_USERNAME-YOUR_SPACE_NAME.hf.space
```

### Alternative: Push via Git
```bash
git clone https://huggingface.co/spaces/USERNAME/SPACE_NAME
cd SPACE_NAME
# copy your files here
git add .
git commit -m "Deploy FastAPI app"
git push
# Username: HF username
# Password: HF token (from Settings → Access Tokens)
```

### Platform Comparison (Free Tier)
| Platform | Sleep After | Boot Time | Max Size | Notes |
|---|---|---|---|---|
| Hugging Face | 48 hours | Fast | ~5 GB | Best for this project |
| Render | 15 minutes | ~60 sec | 1 GB | Good alternative |
| Vercel | N/A | Instant | Serverless | No WebSocket support |
| Railway | Varies | Fast | Varies | Limited free tier |

---

## Part 7 — Automated Testing with Bash

### Why Use a Bash Script for Testing?
Instead of manually testing every endpoint in Postman, a script tests all endpoints automatically in seconds. Saves time when redeploying.

### Step 1 — Create test script
```bash
touch script.sh
chmod +x script.sh
```

### Step 2 — Sample Test Script
```bash
#!/bin/bash

API_URL="http://localhost:8000"
PASS=0
FAIL=0

echo "=== Running API Tests ==="

# Test 1 — Root endpoint
response=$(curl -s -o /dev/null -w "%{http_code}" $API_URL/)
if [ "$response" == "200" ]; then
    echo "✅ GET /         PASSED"
    PASS=$((PASS+1))
else
    echo "❌ GET /         FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

# Test 2 — Item by ID
response=$(curl -s -o /dev/null -w "%{http_code}" $API_URL/item/1)
if [ "$response" == "200" ]; then
    echo "✅ GET /item/1   PASSED"
    PASS=$((PASS+1))
else
    echo "❌ GET /item/1   FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

# Test 3 — File upload
response=$(curl -s -o /dev/null -w "%{http_code}" \
  -X POST $API_URL/upload-file \
  -F "file=@cars.json")
if [ "$response" == "200" ]; then
    echo "✅ POST /upload  PASSED"
    PASS=$((PASS+1))
else
    echo "❌ POST /upload  FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

echo ""
echo "=== Results ==="
echo "Total: $((PASS+FAIL)) | Passed: $PASS | Failed: $FAIL"
```

### Step 3 — Run the Script
```bash
bash script.sh
```

### Step 4 — Change URL for Production Testing
```bash
# Just change this one line to test deployed version
API_URL="https://your-username-your-space.hf.space"
```

---

## Folder Structure for Project 1

```
your-fastapi-server/
├── .env                  ← secret keys (never commit)
├── .gitignore            ← includes .env, venv/
├── app.py                ← FastAPI server code
├── requirements.txt      ← dependencies
├── Dockerfile            ← for deployment
├── script.sh             ← automated test script
└── README.md             ← describe your endpoints
```


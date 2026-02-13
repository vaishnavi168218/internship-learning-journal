# Podman, GitHub Pages, FastAPI, Vercel & ngrok

## Session Overview
This session covered:
- Containers vs Virtual Machines
- Podman vs Docker
- Deploying static sites using GitHub Pages
- Building APIs using FastAPI
- Deploying APIs to Vercel
- Exposing local servers using ngrok
- Managing environment variables and CORS

---

# 1. Containers vs Virtual Machines

## Virtual Machines
- Full operating system with separate kernel
- Heavyweight
- Slower startup
- Strong isolation

## Containers (Podman / Docker)
- Share host kernel
- Lightweight
- Fast startup
- Efficient resource usage

Containers are more suitable for modern development workflows.

---

# 2. Podman vs Docker

| Feature | Podman | Docker |
|----------|--------|--------|
| Daemon | No daemon | Uses daemon |
| Rootless | Default | Traditionally root |
| Compatibility | 99% CLI compatible | Standard |

Example commands:
```bash
podman pull nginx
podman run -d -p 8080:80 nginx
```

Podman provides better security with rootless and daemonless architecture.

---

# 3. GitHub Pages

GitHub Pages provides free static website hosting directly from a repository.

## Requirements
- index.html file
OR
- Markdown rendered via Jekyll

## Steps to Enable
1. Go to Repository → Settings → Pages
2. Select branch (main or gh-pages)
3. Save

Deployment is automatic on every push.

Limitations:
- Only static content
- Jekyll configuration issues may occur

Best used for documentation, portfolios, and static sites.

---

# 4. FastAPI

FastAPI is a modern, high-performance Python web framework.

## Basic Example

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def home():
    return {"message": "Hello World"}
```

Run locally:
```bash
uvicorn main:app --reload
```

Key Features:
- Async support
- Automatic data validation
- Interactive docs at /docs
- High performance

---

# 5. HTTP Methods

| Method | Purpose |
|--------|----------|
| GET    | Retrieve data |
| POST   | Create data |
| PUT    | Update/Replace |
| DELETE | Remove data |

FastAPI decorators:
```python
@app.get()
@app.post()
@app.put()
@app.delete()
```

---

# 6. Deploying FastAPI to Vercel

Vercel is a serverless deployment platform with GitHub integration.

## Required Files
- requirements.txt
- vercel.json
- API inside api/ folder (example: api/index.py)

Example vercel.json:

```json
{
  "version": 2,
  "builds": [{ "src": "api/index.py", "use": "@vercel/python" }],
  "routes": [{ "src": "/(.*)", "dest": "api/index.py" }]
}
```

Deploy using CLI:
```bash
vercel
vercel --prod
```

## Free Tier Limitations
- 300 seconds timeout
- No persistent file storage
- No subprocess execution
- No long-running processes

Suitable for small APIs and serverless applications.

---

# 7. Testing FastAPI Endpoints

Access interactive documentation:
```
/docs
```

Allows:
- Sending GET/POST requests
- Testing JSON payloads
- Viewing response models

---

# 8. ngrok

ngrok exposes local servers to a public URL.

Example:
```bash
ngrok http 8000
```

Provides a public HTTPS link.

Use cases:
- Testing webhooks
- Demonstrating projects
- Sharing localhost applications

Free plan:
- Random URL
- One active tunnel

---

# 9. Managing Environment Variables

Never commit:
- .env files
- API keys

Local setup:
```bash
pip install python-dotenv
```

Access in Python:
```python
import os
os.getenv("API_KEY")
```

In Vercel:
Add environment variables in project settings.

---

# 10. CORS

CORS is a browser security mechanism.

Required when frontend and backend are hosted on different domains.

FastAPI configuration:

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://example.com"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

Without proper CORS configuration, browsers block requests.

---

# Key Learnings

- Differentiated containers and virtual machines
- Understood Podman and Docker architecture differences
- Deployed static sites using GitHub Pages
- Built REST APIs using FastAPI
- Learned HTTP method semantics
- Deployed serverless APIs using Vercel
- Understood Vercel free-tier constraints
- Used ngrok to expose local applications
- Managed secrets securely using environment variables
- Configured CORS for frontend-backend communication

---

# Final Understanding

Containers → API Development → Static Deployment → Serverless Deployment → Secure Secrets → Handle CORS → Public Exposure via ngrok

Complete modern development and deployment workflow.


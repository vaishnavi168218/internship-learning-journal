#  Hands-On: Containerizing Jupyter, Ollama & Flask using Podman (WSL)

##  Objective
- Run Jupyter Lab inside a container
- Run a Local LLM (Ollama) inside a container
- Connect two containers using a custom network
- Build a Flask app that communicates with the LLM
- Understand port binding, volumes, and networking

---

#  Step 1: Install Podman (Inside WSL)

```bash
sudo apt update
sudo apt install podman -y
podman --version
podman info
```

---

# Step 2: Run Jupyter Lab in Container

## Pull Jupyter Image
```bash
podman pull quay.io/jupyter/base-notebook
```

## Run Jupyter Container
```bash
podman run -d \
  --name jupyter \
  -p 8888:8888 \
  -v ./jupyter-work:/home/jovyan/work \
  quay.io/jupyter/base-notebook
```

## Access in Browser
```
http://localhost:8888
```

Learned:
- `-d` runs in background  
- `-p` exposes port  
- `-v` mounts local folder for persistence  

---

# Step 3: Run Ollama (Local LLM) in Container

## Pull Ollama Image
```bash
podman pull docker.io/ollama/ollama:alpine
```

## Create Custom Network
```bash
podman network create ai-net
```

## Run Ollama Container
```bash
podman run -d \
  --name ollama \
  -p 11434:11434 \
  --network ai-net \
  -v ./ollama:/root/.ollama \
  docker.io/ollama/ollama:alpine
```

## Enter Container
```bash
podman exec -it ollama bash
```

## Pull Small Model
```bash
ollama pull gemma3:270m
```

## Test Model
```bash
ollama run gemma3:270m
```

Type prompt → Get response ✅

---

#  Step 4: Build Flask App to Talk to Ollama

## Create Flask App (app.py)

```python
from flask import Flask, request
import requests

app = Flask(__name__)

@app.route("/")
def home():
    return "Flask + Ollama Running!"

@app.route("/chat", methods=["POST"])
def chat():
    user_input = request.json["message"]

    response = requests.post(
        "http://ollama:11434/api/chat",
        json={
            "model": "gemma3:270m",
            "messages": [{"role": "user", "content": user_input}]
        }
    )

    return response.json()

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

#  Step 5: Containerize Flask App

## Create Dockerfile

```dockerfile
FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install flask requests
CMD ["python", "app.py"]
```

## Build Image
```bash
podman build -t flask-llm .
```

## Run Flask Container (Attach to Same Network)
```bash
podman run -d \
  --name flask-app \
  -p 5000:5000 \
  --network ai-net \
  flask-llm
```

---

#  Step 6: Test Inter-Container Communication

Open browser:
```
http://localhost:5000
```

Test API using curl:
```bash
curl -X POST http://localhost:5000/chat \
-H "Content-Type: application/json" \
-d '{"message":"Hello"}'
```

 Flask container talks to Ollama container  
 Ollama returns LLM response  

---

# 🛠 Step 7: Manage Containers

```bash
podman ps
podman logs -f flask-app
podman stop flask-app
podman rm flask-app
podman network ls
```

---

#  Step 8: Fix WSL Networking (If Needed)

If localhost doesn’t work:

```bash
ip addr show eth0
```

Use:
```
http://<WSL-IP>:5000
```

---

# Learned:

- Installed and configured Podman in WSL
- Pulled images and ran containers
- Used port binding to access services
- Used volumes to persist data
- Created custom network for container communication
- Containerized Jupyter Lab
- Containerized Ollama (Local LLM)
- Built Flask app connected to LLM backend
- Debugged WSL networking issues
- Understood multi-container AI architecture

---

# Final Architecture

Browser  
↓  
Flask Container  
↓  
Ollama Container  
↓  
LLM Model  

Containerization → Networking → API Communication → Web Interface → AI Backend

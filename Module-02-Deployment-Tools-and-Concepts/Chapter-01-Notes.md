# 🐳 Containerization with Podman – Jupyter, Ollama & Flask

## Session Overview
This session covered containerization fundamentals using Podman and building a multi-container AI application including Jupyter Lab, Ollama (Local LLM), and a Flask web app. The goal was to understand how to package, run, connect, and persist AI applications using containers in WSL.

---

##  Why Containers?
- Avoid “it works on my machine” issues
- Package code + dependencies + OS-level tools together
- Ensure consistent behavior across Windows, Linux, Mac, and Cloud
- Lightweight alternative to virtual machines

---

##  Key Concepts
- **Image** → Blueprint/template for container
- **Container** → Running instance of image
- **Pull** → Download image
- **Run** → Create + start container
- **Volume (-v)** → Persist data outside container
- **Port Binding (-p)** → Expose container service
- **Network** → Enable container-to-container communication

---

## 🛠 Podman Installation (WSL)

```bash
sudo apt update
sudo apt install podman
podman --version
podman info
```

---

##  Project 1 – Jupyter Lab in Container

Pull image:
```bash
podman pull quay.io/jupyter/base-notebook
```

Run container:
```bash
podman run -d \
  --name jupyter \
  -p 8888:8888 \
  -v ./jupyter-work:/home/jovyan/work \
  quay.io/jupyter/base-notebook
```

Access:
```
http://localhost:8888
```

Key Learning:
- Used port binding for browser access
- Used volume mounting for persistent notebooks

---

## 🤖 Project 2 – Ollama (Local LLM) in Container

Pull image:
```bash
podman pull docker.io/ollama/ollama:alpine
```

Create custom network:
```bash
podman network create ai-net
```

Run Ollama:
```bash
podman run -d \
  --name ollama \
  -p 11434:11434 \
  --network ai-net \
  -v ./ollama:/root/.ollama \
  docker.io/ollama/ollama:alpine
```

Enter container:
```bash
podman exec -it ollama bash
```

Pull model:
```bash
ollama pull gemma3:270m
```

Run model:
```bash
ollama run gemma3:270m
```

---

## Project 3 – Flask + Ollama (Inter-Container Networking)

Both containers attached to:
```bash
podman network create ai-net
```

Flask calls Ollama using:
```
http://ollama:11434/api/chat
```

Container name becomes hostname inside network.

Architecture:
Browser → Flask Container → Ollama Container → LLM Model

---

## 🔌 Managing Containers

```bash
podman ps
podman ps -a
podman logs -f NAME
podman stop NAME
podman start NAME
podman rm NAME
podman network ls
```

---

## 🛠 WSL Networking Troubleshooting

If localhost fails:
```bash
ip addr show eth0
```

Use WSL IP:
```
http://<WSL-IP>:PORT
```

---

## Key Learnings

- Understood containerization fundamentals
- Installed and used Podman in WSL
- Containerized Jupyter Lab with persistent storage
- Ran a local LLM (Ollama) inside container
- Created custom networks for inter-container communication
- Built Flask web app connected to LLM backend
- Understood port binding, volumes, and container lifecycle
- Troubleshot WSL networking issues
- Learned real-world multi-container AI architecture

---

##  Final Understanding

Development → Containerization → Networking → API Communication → Web Interface → LLM Backend

This session provided hands-on experience with production-style containerized AI workflows.

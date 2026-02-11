# 🚀 FastAPI Project Workflow Learn the TDS project workflow and how to build, test, and deploy a FastAPI server, including handling requests and file uploads.

---

# 🧭 Project Workflow

```
Client → FastAPI Server → Validation → Business Logic → Response
```

### Development Lifecycle

* Design API endpoints
* Implement backend logic
* Validate requests using Pydantic
* Test endpoints
* Containerize using Docker
* Deploy to cloud platform

---

# ⚙️ FastAPI Setup

## Install Dependencies

```bash
pip install fastapi uvicorn
```

## Basic Application

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Hello World"}
```

## Run the Server

```bash
uvicorn app:app --reload
```

### Access URLs

* App: [http://127.0.0.1:8000](http://127.0.0.1:8000)
* Swagger Docs: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

# 🛣️ Path & Query Parameters

## Path Parameter (Required)

```python
@app.get("/items/{item_id}")
def get_item(item_id: int):
    return {"item_id": item_id}
```

## Query Parameter (Optional)

```python
@app.get("/items/")
def get_items(limit: int = 10):
    return {"limit": limit}
```

Example:

```
/items?limit=5
```

---

# 📦 Pydantic Models (Data Validation)

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
```

## Benefits

* Automatic request validation
* Type safety
* Auto-generated API documentation
* Cleaner and structured code

---

# 📬 POST Requests

```python
@app.post("/items/")
def create_item(item: Item):
    return item
```

### Features

* Validates JSON body automatically
* Returns 422 error for invalid input
* Integrated with Swagger UI

---

# 📁 File Upload

## Single File Upload

```python
from fastapi import File, UploadFile

@app.post("/upload/")
def upload_file(file: UploadFile = File(...)):
    return {"filename": file.filename}
```

## Multiple File Upload

```python
from typing import List

@app.post("/upload-multiple/")
def upload_files(files: List[UploadFile] = File(...)):
    return {"filenames": [file.filename for file in files]}
```

---

# 🧪 API Testing

## Using curl

```bash
curl http://127.0.0.1:8000/items/1
```

### Purpose

* Command-line testing
* Automation support
* CI/CD pipeline integration

---

# 🔐 Secret Keys & Environment Variables

## Set Environment Variable

```bash
export SECRET_KEY="mysecret"
```

## Access in Python

```python
import os
secret = os.getenv("SECRET_KEY")
```

### Best Practices

* Never hardcode secrets
* Use environment variables or `.env` files
* Keep credentials outside version control

---

# 🐳 Docker Setup

## Sample Dockerfile

```dockerfile
FROM python:3.10

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

## Build & Run Docker Container

```bash
docker build -t fastapi-app .
docker run -p 8000:8000 fastapi-app
```

---

# 🌍 Deployment (Hugging Face)

## Steps

1. Push project to GitHub repository
2. Connect repository to Hugging Face Spaces
3. Use Docker-based deployment
4. Deploy and test public API

### Outcome

* Publicly accessible API
* Production-ready backend
* Portfolio showcase project

---

# 🖥️ Bash Script for Live Testing

## Example: test.sh

```bash
#!/bin/bash

curl http://127.0.0.1:8000/
curl http://127.0.0.1:8000/items/1
```

## Run Script

```bash
bash test.sh
```

---

# 🎯 Key Takeaways

* FastAPI enables rapid API development
* Pydantic ensures strong validation
* Swagger provides interactive documentation
* Docker simplifies deployment
* Environment variables secure sensitive data
* Automation improves testing efficiency

---

# 🏁 Conclusion

This session provides a complete end-to-end understanding of building a FastAPI backend — from local development and validation to containerization and cloud deployment. It establishes a strong foundation for real-world backend engineering and production-ready API development.

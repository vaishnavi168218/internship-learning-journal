# 🧪 Prompt Experiments 
## Experiment 1 — First GET Endpoint

### What They Did
Created the most basic FastAPI server with a single root endpoint
and ran it locally using uvicorn.

### Code
```python
# app.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Hello from TDS"}
```

```bash
# Run the server
uvicorn app:app --reload
```

### How They Tested It
- Opened browser → `http://localhost:8000`
- Opened Postman → GET → `http://localhost:8000` → Send

### Expected Output
```json
{"message": "Hello from TDS"}
```
---

## Experiment 2 — Path Parameters
### Code
```python
# In-memory data store
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

### Expected URLs
- Postman → GET → `http://localhost:8000/item/1` → got Apple
- Postman → GET → `http://localhost:8000/item/2` → got Banana
- Postman → GET → `http://localhost:8000/item/5` → got Not found

### Expected Output
```json
// /item/1
{"name": "Apple"}

// /item/5
{"error": "Not found"}
```

---

## Experiment 3 — Query Parameters

### What They Did
Created a search endpoint that filters items by name using
a query parameter. Also demonstrated case-insensitive search
using `.lower()`.

### Code
```python
@app.get("/search")
def search_item(q: str):
    results = []
    for item in item_db.values():
        if q.lower() in item["name"].lower():
            results.append(item)
    return results
```

### Tested And Expected URLs
- `http://localhost:8000/search?q=apple` → returned Apple
- `http://localhost:8000/search?q=APPLE` → still returned Apple (case insensitive)
- `http://localhost:8000/search?q=an` → returned Banana and Pineapple (both contain "an")

### Expected Output
```json
// ?q=an
[{"name": "Banana"}, {"name": "Pineapple"}]
```


---

## Experiment 4 — Pydantic Response Model

### What They Did
Defined a Pydantic model with specific fields, then showed that
even if the function returns extra fields, only the fields defined
in the response model are sent to the client.

### Code
```python
from pydantic import BaseModel

# Response model — only these fields go to the client
class Item(BaseModel):
    name: str
    price: float

@app.get("/product", response_model=Item)
def get_product():
    # Returns extra_field too — but it will be stripped
    return {"name": "Mango", "price": 50.0, "extra_field": "hidden"}
```
### Expected Output
```json
// extra_field is NOT in Item model — it gets stripped
{"name": "Mango", "price": 50.0}
```

---

## Experiment 5 — POST Endpoint with Validation

### What They Did
Created a POST endpoint to register users. First showed a basic
version, then added Pydantic validation with field constraints
including minimum username length, email format, and age limit.

### Code — Basic Version
```python
users_db = []

@app.post("/users")
def create_user(user: dict):
    users_db.append(user)
    return {"message": "User created", "user": user}
```

### Code — With Pydantic Validation
```python
from pydantic import BaseModel, EmailStr, Field

class UserCreate(BaseModel):
    username: str = Field(min_length=3, max_length=50)
    email: EmailStr
    age: int = Field(lt=120)

users_tds = []

@app.post("/users/advanced")
def create_user_advanced(user: UserCreate):
    users_tds.append(user)
    return {"message": "User created", "user": user.dict()}
```

```bash
# Install email validator
pip install pydantic[email]
```

### How To Test With (Postman)
```
Method: POST
URL: http://localhost:8000/users/advanced
Body → raw → JSON:

{
  "username": "sujal",
  "email": "crab@1223.com",
  "age": 21
}
---

## Experiment 6 — Single File Upload

### Code
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

### Test Files Created
```json
// cars.json
{
  "cars": [
    {"make": "Toyota", "model": "Camry"},
    {"make": "Honda", "model": "Civic"}
  ]
}
```

```csv
// animals.csv
name,species,age
Lion,Mammal,5
Eagle,Bird,3
Shark,Fish,10
```

### How To Test With (Postman)
```
Method: POST
URL: http://localhost:8000/upload-file
Body → form-data
Key: file    ← must match parameter name exactly
Type: File   ← change from Text to File in dropdown
Value: [select cars.json from your computer]
Click Send
```

### How They Tested It (curl — faster)
```bash
curl -X POST http://localhost:8000/upload-file \
  -F "file=@cars.json"
```

### Expected Output
```json
{
  "filename": "cars.json",
  "size": 89,
  "content_preview": "{\n  \"cars\": [\n    {\"make\": \"Toyota\"..."
}

---

## Experiment 7 — Multiple File Upload
### Code
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

### How To Test With(Postman)
```
Method: POST
URL: http://localhost:8000/upload-files
Body → form-data
Key: files   Type: File   Value: cars.json
Key: files   Type: File   Value: animals.csv
(add same key "files" twice with different files)
Click Send
```

### How They Tested It (curl)
```bash
curl -X POST http://localhost:8000/upload-files \
  -F "files=@cars.json" \
  -F "files=@animals.csv"
```

### Expected Output
```json
{
  "files": [
    {"filename": "cars.json", "size": 89},
    {"filename": "animals.csv", "size": 45}
  ]
}

---

## Experiment 8 — Copilot curl Generation

### What They Did
Instead of manually constructing curl commands, they described
the endpoint to Copilot in plain English and got the curl command
generated instantly. Then saved it to a file for reuse.

### Prompt They Used in Copilot
```
There is an endpoint upload-file.
Write a curl request that will send cars.json as an attachment.
```

### What Copilot Generated
```bash
curl -X POST http://localhost:8000/upload-file \
  -F "file=@cars.json"
```

### Second Prompt for Multiple Files
```
There's an endpoint upload-files that will send cars.json
and animals.csv as attachments.
```

### What Copilot Generated
```bash
curl -X POST http://localhost:8000/upload-files \
  -F "files=@cars.json" \
  -F "files=@animals.csv"
```

### How to Save and Reuse
```bash
# Save to a file
echo 'curl -X POST http://localhost:8000/upload-file -F "file=@cars.json"' > test.txt

# Run anytime
bash test.txt
```

---

## Experiment 9 — Secret Key from .env

### What They Did
Moved a sensitive value (secret key) out of the Python code
and into a `.env` file. Loaded it at runtime and exposed it
via a GET endpoint to verify it loaded correctly.

### Files Created

**.env**
```env
SECRET_KEY=data_science_is_a_very_good_subject
```

**app.py additions**
```python
import os
from dotenv import load_dotenv

load_dotenv()

SECRET_KEY = os.getenv("SECRET_KEY")

@app.get("/secret")
def get_secret():
    return {"key": SECRET_KEY}
```

```bash
# Install dotenv
pip install python-dotenv
```

### How They Tested It
```
Browser or Postman → GET → http://localhost:8000/secret
```

### Expected Output
```json
{"key": "data_science_is_a_very_good_subject"}
```

### Then Added to Hugging Face Secrets
```
Space → Settings → Variables and Secrets → New Secret
Name:  SECRET_KEY
Value: tds_is_a_very_good_subject
Save
```

---

## Experiment 10 — Deploy to Hugging Face

### What They Did
Created a Dockerfile, uploaded all files to a Hugging Face Space,
added the secret key via Hugging Face's secrets UI, and verified
the deployed app was accessible at the public URL.

### Files They Used

**requirements.txt**
```
fastapi
uvicorn
python-multipart
python-dotenv
pydantic[email]
```

**Dockerfile**
```dockerfile
FROM python:3.11

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 7860

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```

### Steps to be Followed
```
1. huggingface.co → New Space
2. Name: fastapi-demo
3. SDK: Docker
4. Hardware: CPU Basic (free)
5. Visibility: Public
6. Create Space

7. Files → Add File → Upload Files
8. Upload: app.py, requirements.txt, Dockerfile
9. Commit changes

10. Settings → Secrets → New Secret
11. Name: SECRET_KEY  Value: tds_is_a_very_good_subject
12. Save

13. Wait for build to complete
14. Visit: https://vaishnavi-fastapi-demo.hf.space
15. Test: https://vaishnavi-fastapi-demo.hf.space/secret
```

### URL
```
They asked Copilot: "What is the deployed URL for my Hugging Face Space?"
Copilot returned: https://vaishnavi-spacename.hf.space
```

---

## Experiment 11 — Automated Bash Test Script

### What They Did
Used Copilot to generate a bash script that tests all endpoints
automatically. Ran it with one command to verify all endpoints
pass. Showed how changing one URL variable switches between
local and production testing.

### Prompt Used in Copilot
```
Create a bash file that checks all the endpoints for this
[codebase] .ssl bash file
```

### Script That Was Generated and Used
```bash
#!/bin/bash

# Change this one line to switch between local and production
API_URL="http://localhost:8000"
# API_URL="https://your-username-fastapi-demo.hf.space"

PASS=0
FAIL=0

echo "=== Running API Tests ==="

# Test root endpoint
response=$(curl -s -o /dev/null -w "%{http_code}" $API_URL/)
if [ "$response" == "200" ]; then
    echo "✅ GET /              PASSED"
    PASS=$((PASS+1))
else
    echo "❌ GET /              FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

# Test item by ID
response=$(curl -s -o /dev/null -w "%{http_code}" $API_URL/item/1)
if [ "$response" == "200" ]; then
    echo "✅ GET /item/1        PASSED"
    PASS=$((PASS+1))
else
    echo "❌ GET /item/1        FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

# Test item not found
response=$(curl -s -o /dev/null -w "%{http_code}" $API_URL/item/999)
if [ "$response" == "200" ]; then
    echo "✅ GET /item/999      PASSED"
    PASS=$((PASS+1))
else
    echo "❌ GET /item/999      FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

# Test search
response=$(curl -s -o /dev/null -w "%{http_code}" "$API_URL/search?q=apple")
if [ "$response" == "200" ]; then
    echo "✅ GET /search?q=apple PASSED"
    PASS=$((PASS+1))
else
    echo "❌ GET /search?q=apple FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

# Test secret endpoint
response=$(curl -s -o /dev/null -w "%{http_code}" $API_URL/secret)
if [ "$response" == "200" ]; then
    echo "✅ GET /secret        PASSED"
    PASS=$((PASS+1))
else
    echo "❌ GET /secret        FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

# Test file upload
response=$(curl -s -o /dev/null -w "%{http_code}" \
  -X POST $API_URL/upload-file \
  -F "file=@cars.json")
if [ "$response" == "200" ]; then
    echo "✅ POST /upload-file  PASSED"
    PASS=$((PASS+1))
else
    echo "❌ POST /upload-file  FAILED (HTTP $response)"
    FAIL=$((FAIL+1))
fi

echo ""
echo "=== Results: $((PASS+FAIL)) Total | ✅ $PASS Passed | ❌ $FAIL Failed ==="
```

### How To Run It
```bash
# Make it executable
chmod +x script.sh

# Run locally
bash script.sh

# Switch to production — just change API_URL at top
# Then run again
bash script.sh
```






---


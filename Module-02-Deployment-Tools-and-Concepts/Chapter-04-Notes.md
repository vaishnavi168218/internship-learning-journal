# FastAPI from Scratch to Deployment

## Session Goal

Understand and implement the complete workflow required for Project 1:

- Build a FastAPI server
- Receive requests from IITM evaluation server
- Validate secret key
- Process LLM task within 10 minutes
- Dynamically create a GitHub repository
- Push generated code
- Enable GitHub Pages
- Send structured JSON response back

---

# 1.Project 1 – Complete Workflow

## Evaluation Flow

IITM Evaluation Server
→ Sends JSON request + secret + task description
→ Your FastAPI Server

Your server must:

1. Immediately return `200 OK`
2. Start background processing (max 10 minutes)
3. Call LLM (GPT / Gemini / Claude / etc.)
4. Generate application code (HTML + CSS + JavaScript)
5. Create new public GitHub repository dynamically
6. Push generated code to repository
7. Enable GitHub Pages
8. Send back JSON response containing:
   - GitHub repo URL
   - GitHub Pages live URL
   - Required metadata

Two rounds:
- Round 1 → Create application
- Round 2 → Modify previously created application

---

# 2. Security Requirement (Very Important)

- A secret value is submitted via Google Form.
- Every request from IITM contains this secret.
- Your FastAPI must validate the secret.
- If secret does not match → reject request.

Secret handling:
- Store in `.env`
- Access using `os.getenv()`
- Never hardcode secrets

---

# 3. Important FastAPI Endpoints Demonstrated

| Order | Endpoint Type | Purpose | Importance |
|--------|--------------|----------|-------------|
| 1 | GET / | Basic test endpoint | Low |
| 2 | GET /item/{id} | Path parameter example | Medium |
| 3 | GET /search?q= | Query parameter example | Medium |
| 4 | POST /users | Receive JSON body + Pydantic validation | Critical |
| 5 | POST /uploadfile | Receive single file | Very Important |
| 6 | POST /uploadfiles | Receive multiple files | Very Important |
| 7 | GET /secret | Return secret from environment | Important |

---

# 4. Core Technical Concepts Learned

## JSON Validation using Pydantic

- Use `BaseModel` to validate request body.
- Automatically validates types and required fields.

## File Upload Handling

Single file:
- Use `UploadFile`
- Read using `await file.read()`

Multiple files:
- Use `List[UploadFile]`

## Secret Protection

- Store secret in `.env`
- Load using `python-dotenv`
- Compare request secret with stored value

## Testing Endpoints

- Use `curl` commands
- Generate automated bash test script
- Verify responses before deployment

---

# 5. Hugging Face Deployment Cheat-Sheet

## Dockerfile (Recommended Minimal Version)

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 7860

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "7860"]
```

## Common Ports (October 2025)

- Hugging Face Spaces → 7860
- Render → 10000
- Railway → 8080 / 3000

---

# 6. Must-Have Features for Project 1

| Requirement | Importance |
|-------------|------------|
| Receive JSON + Pydantic validation | Critical |
| Secret key validation | Critical |
| File upload handling | High |
| Fast LLM response | High |
| Create GitHub repo via API | High |
| Enable GitHub Pages | Medium |
| Send correct JSON response | Critical |
| Deploy to Hugging Face / Render | High |
| Automated curl test script | Helpful |

---

# 7. Questions You Must Be Able to Answer

- What should your server return immediately when IITM calls?
- Where should the secret value be stored?
- Which POST endpoints are most important?
- What is the maximum time allowed to finish processing?
- Which port must be exposed on Hugging Face?

---

# 8. Complete Project Pipeline

Receive Request  
→ Validate Secret  
→ Return Immediate 200 OK  
→ Process Task (≤10 minutes)  
→ Call LLM  
→ Generate Web App Code  
→ Create GitHub Repo  
→ Push Code  
→ Enable GitHub Pages  
→ Send Final JSON Response  

Full end-to-end automated deployment workflow.

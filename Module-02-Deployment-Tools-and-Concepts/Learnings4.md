# Learnings – (FastAPI to Deployment)

## 1. Project Workflow Understanding

- Understood complete IITM evaluation flow.
- Learned importance of returning immediate 200 OK response.
- Implemented background task processing (≤10 minutes limit).
- Understood two-round system: create app → modify app.

---

## 2. Security Implementation

- Learned to validate secret key in every request.
- Stored secret securely using .env file.
- Used python-dotenv to load environment variables.
- Understood why secrets must never be hardcoded.

---

## 3. FastAPI Core Concepts

- Implemented POST endpoint with Pydantic validation.
- Handled JSON request body using BaseModel.
- Implemented file upload (single & multiple).
- Used BackgroundTasks for non-blocking execution.
- Structured proper JSON response format.

---

## 4. LLM Integration Concept

- Understood how to call LLM API dynamically.
- Generated HTML/CSS/JS code from task description.
- Optimized response speed to stay within time limit.

---

## 5. GitHub Automation

- Created GitHub repository dynamically using API.
- Pushed generated code programmatically.
- Enabled GitHub Pages automatically.
- Returned repo URL and live website URL in response.

---

## 6. Deployment Knowledge

- Dockerized FastAPI application.
- Exposed correct port (7860 for Hugging Face).
- Deployed using Docker-based workflow.
- Added environment secrets in hosting platform settings.

---

## 7. Testing & Validation

- Tested endpoints using curl commands.
- Created automated bash testing script.
- Verified JSON structure before submission.

---

## 8. Overall System Architecture Learned

Receive Request
→ Validate Secret
→ Return Immediate 200 OK
→ Background Processing
→ Call LLM
→ Generate Code
→ Create Repo
→ Enable GitHub Pages
→ Send Final Response

Complete end-to-end automated deployment pipeline implemented.

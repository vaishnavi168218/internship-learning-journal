# LLM ENGINEERING SESSION 

## 1. GOALS
- API calls using HTTPX
- Chatbot with memory
- Base64 encoding/decoding (images)
- Embeddings + similarity search
- Manual vector database
- Multimodal embeddings (Jina AI)
- Function calling (structured outputs)

### PROJECTS
- Chatbot with history (ChatGPT-style)
- Product detail extractor (image → structured JSON)

--------------------------------------------------

## 2. EMBEDDINGS INTUITION
- embeddings = vector representation of meaning
- each dimension = hidden feature

### ANALOGY
- child evaluates apple using multiple factors
- assigns scores across dimensions
- selects best option
- embeddings behave similarly

### LEARNING
- semantic meaning > exact words
- similar meaning → closer vectors

--------------------------------------------------

## 3. API KEY MANAGEMENT (.bashrc)

### SETUP
nano ~/.bashrc
export OPENAI_API_KEY=your_api_key_here

### USAGE
import os
api_key = os.environ.get("OPENAI_API_KEY")

### LEARNING
- avoids hardcoding secrets
- safer for version control

--------------------------------------------------

## 4. API CALLS USING HTTPX

### REQUIREMENTS
- URL
- Headers (auth + content-type)
- JSON payload

### IMPLEMENTATION
import httpx, os

url = "https://aiproxy.sanand.workers.dev/openai/v1/chat/completions"

headers = {
    "Content-Type": "application/json",
    "Authorization": f"Bearer {os.environ.get('OPENAI_API_KEY')}"
}

data = {
    "model": "gpt-4.1-nano",
    "messages": [{"role": "user", "content": "Hello!"}]
}

response = httpx.post(url, headers=headers, json=data, timeout=10)
json_response = response.json()

reply = json_response["choices"][0]["message"]["content"]

### LEARNING
- increase timeout for LLM responses
- understand nested JSON structure

--------------------------------------------------

## 5. CHATBOT WITH MEMORY

### CONCEPT
- LLMs are stateless
- memory = full message history

### ROLES
- developer/system → behavior control
- user → input
- assistant → output

### IMPLEMENTATION
messages = [{"role": "developer", "content": "Answer within three words."}]

while True:
    user_query = input("You: ")
    if user_query == "exit":
        break

    messages.append({"role": "user", "content": user_query})
    ai_response = get_ai(messages)
    messages.append({"role": "assistant", "content": ai_response})

    print(f"AI: {ai_response}")

### LEARNING
- full conversation must be sent every time

--------------------------------------------------

## 6. BASE64 ENCODING (IMAGES)

### ENCODE
import base64

with open("image.png", "rb") as f:
    image_b64 = base64.b64encode(f.read()).decode()

### DECODE
decoded = base64.b64decode(image_b64)

with open("restored.png", "wb") as f:
    f.write(decoded)

### LEARNING
- binary → text → binary
- reversible with no data loss

--------------------------------------------------

## 7. EMBEDDINGS API

import httpx, os

url = "https://aiproxy.sanand.workers.dev/openai/v1/embeddings"

data = {
    "model": "text-embedding-3-small",
    "input": "cat",
    "encoding_format": "float"
}

response = httpx.post(url, json=data, timeout=10)
embedding = response.json()["data"][0]["embedding"]

### LEARNING
- vectors represent semantic meaning

--------------------------------------------------

## 8. SIMILARITY CALCULATIONS

### EUCLIDEAN DISTANCE
import numpy as np

def get_distance(v1, v2):
    diff = np.array(v1) - np.array(v2)
    return np.sqrt(np.dot(diff, diff))

### COSINE SIMILARITY
def get_cosine_similarity(v1, v2):
    v1, v2 = np.array(v1), np.array(v2)
    return np.dot(v1, v2) / (np.linalg.norm(v1) * np.linalg.norm(v2))

### LEARNING
- cosine similarity preferred
- measures directional similarity

--------------------------------------------------

## 9. MANUAL VECTOR DATABASE

### FLOW
- input → embedding
- compare with stored vectors
- return closest match

### LEARNING
- foundation of semantic search

--------------------------------------------------

## 10. MULTIMODAL EMBEDDINGS (JINA AI)

### CONCEPT
- text + image → same vector space
- same dimensional vectors

### LEARNING
- enables text ↔ image comparison

--------------------------------------------------

## 11. MULTIMODAL INPUT

messages = [
    {
        "role": "user",
        "content": [
            {"type": "text", "text": "Extract all info"},
            {
                "type": "image_url",
                "image_url": {
                    "url": f"data:image/png;base64,{image_b64}"
                }
            }
        ]
    }
]

### LEARNING
- clear structured prompts improve accuracy

--------------------------------------------------

## 12. FUNCTION CALLING (STRUCTURED OUTPUT)

### SCHEMA
tools = [
    {
        "type": "function",
        "function": {
            "name": "extract_product_info",
            "description": "Extract product details",
            "strict": True,
            "parameters": {
                "type": "object",
                "properties": {
                    "mfd": {"type": "number"},
                    "expiry_date": {"type": "number"},
                    "name": {"type": "string"},
                    "answer": {"type": "string"}
                },
                "required": ["mfd", "expiry_date", "name", "answer"]
            }
        }
    }
]

### EXTRACTION
result = json_response["choices"][0]["message"]["tool_calls"][0]["function"]["arguments"]

### LEARNING
- guarantees structured JSON output
- removes ambiguity

--------------------------------------------------

## 13. PROJECT 1 — CHATBOT

### FEATURES
- maintains conversation history
- contextual responses

### OUTCOME
- model recalls past inputs

--------------------------------------------------

## 14. PROJECT 2 — PRODUCT EXTRACTOR

### PIPELINE
- image → base64 encode
- send with prompt + schema
- receive structured JSON

### OUTPUT
- manufacturing date
- expiry date
- product name
- answer

### LEARNING
- stronger models give better accuracy
- small models may hallucinate

--------------------------------------------------

## 15. EXPERIMENTS

### PROMPT CLARITY
- vague → poor output
- clear → accurate output

### CONSTRAINTS
- strict instructions enforce structure

### MEMORY
- no history → stateless
- with history → contextual recall

### EMBEDDINGS
- similar meaning → closer vectors

### RAG (CONTEXT INJECTION)
- improves grounding

### CONTEXT SIZE
- too much → noise

### MULTIMODAL PROMPTING
- structured input improves extraction

### FUNCTION CALLING
- ensures all required fields

### MODEL COMPARISON
- small → fast, less accurate
- large → slower, more accurate

### COST OPTIMIZATION
- reuse embeddings
- minimize API calls

--------------------------------------------------

## FINAL INSIGHT
- LLMs are stateless engines

### PRODUCTION SYSTEMS REQUIRE
- memory handling
- embeddings + vector search
- structured outputs
- strong prompt engineering


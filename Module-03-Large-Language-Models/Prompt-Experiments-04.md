# Complete Prompt Experiments & Learnings — Embeddings, Multimodal AI & RAG

## 1. Basic vs Structured Prompting
Prompt:
"What is FastAPI?"

Learning:
- Produces generic, inconsistent answers.

Improved Prompt:
"Explain FastAPI in 3 concise bullet points for a beginner."

Learning:
- Adding structure improves clarity and consistency.

## 2. Role-Based Prompting
Prompt:
"You are a backend engineer. Explain FastAPI to a junior developer."

Learning:
- Role assignment improves relevance and practical explanation.

## 3. Step-by-Step Reasoning
Prompt:
"Explain how a request flows in FastAPI step by step."

Learning:
- Encourages logical flow and completeness.

## 4. Embedding-Based Retrieval (RAG)
Code:
from openai import OpenAI
client = OpenAI()

query = "What is vector database?"
query_embedding = client.embeddings.create(
    model="text-embedding-3-small",
    input=query
)

Learning:
- Queries are converted into vectors.
- Retrieval happens before generation.

## 5. Context Injection
Prompt:
Context:
FastAPI is a modern web framework for building APIs with Python.

Question:
What is FastAPI?

Learning:
- Model prioritizes given context over its own knowledge.

## 6. Multimodal Prompt (Text + Image)
Code:
response = client.responses.create(
    model="gpt-4.1",
    input=[{
        "role": "user",
        "content": [
            {"type": "input_text", "text": "Describe this image"},
            {
                "type": "input_image",
                "image_url": "https://example.com/image.png"
            }
        ]
    }]
)

Learning:
- Enables understanding across text and images.

## 7. Chunking Strategy
Code:
def chunk_text(text, size=200):
    words = text.split()
    for i in range(0, len(words), size):
        yield " ".join(words[i:i+size])

Learning:
- Smaller chunks improve retrieval accuracy.

## 8. Similarity Calculation
Code:
import numpy as np

def cosine_similarity(a, b):
    return np.dot(a, b) / (np.linalg.norm(a) * np.linalg.norm(b))

Learning:
- Core mechanism for finding relevant context.

## 9. Ranking + Final Prompt
Code:
top_chunks = sorted(chunks, key=lambda x: x["score"], reverse=True)[:3]
context = "\n".join([chunk["text"] for chunk in top_chunks])

Prompt:
f"""
Answer the question based only on the context below:

{context}

Question: {query}
"""

Learning:
- Top-k retrieval improves accuracy.
- Too much context can reduce quality.

## 10. JSON vs JSONL Handling
Incorrect:
import json
data = json.load(open("data.jsonl"))

Correct:
data = []
with open("data.jsonl") as f:
    for line in f:
        data.append(json.loads(line))

Learning:
- JSONL must be parsed line by line.

## 11. Async Optimization
Code:
import asyncio

async def get_embedding(text):
    return client.embeddings.create(
        model="text-embedding-3-small",
        input=text
    )

results = await asyncio.gather(*[get_embedding(t) for t in texts])

Learning:
- Async processing improves speed for large workloads.

## 12. Error Handling Awareness
Issues:
- Wrong API endpoint
- Missing API key
- Incorrect headers

Learning:
- Many failures are system-level, not prompt-level.

## 13. Hallucination Control
Prompt:
"Answer only if the information is present in the context. Otherwise, say 'I don't know'."

Learning:
- Reduces incorrect confident answers.

## 14. Combined Production Prompt
Code:
prompt = f"""
You are an AI assistant.

Rules:
- Use only provided context
- Be concise
- If unsure, say "I don't know"

Context:
{retrieved_chunks}

Question:
{user_query}
"""

Learning:
- Combining constraints + context = reliable output.


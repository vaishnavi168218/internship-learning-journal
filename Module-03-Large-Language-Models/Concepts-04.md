# Embeddings, Multimodal AI & RAG —  Concepts 

## 📌 1. Embeddings
- Numerical vector representation of data (text, images, audio)
- Exists in n-dimensional semantic space
- Dimension depends on model (e.g., 1536)
- Lower cost than LLM APIs
- Similar meaning → closer vectors

### Models
- Sentence Transformers (local)
- OpenAI: text-embedding-3-small (API)
- Nomic AI (multimodal)

---

## 📌 2. Vector Similarity
- Dot Product: np.dot(v1, v2)
- Norm: np.linalg.norm(v)
- Cosine Similarity:
  similarity = dot(v1, v2) / (||v1|| * ||v2||)
- Range: 1 (same), 0 (different)

---

## 📌 3. Multimodal Embeddings
- Maps text + images into same vector space
- Enables cross-modal comparison

### Features
- Same dimensional output
- Image ↔ Text similarity

### Providers
- Nomic AI
- Jina AI (mentioned)

---

## 📌 4. Vector Databases
- Store embeddings + metadata

### Structure
{
  "source": "file_path",
  "embedding": [...],
  "text": "content"
}

### Purpose
- Fast similarity search
- Backbone of RAG

### Options
- ChromaDB
- Pinecone
- Weaviate
- JSON (manual)

---

## 📌 5. Chunking
- Split large documents into smaller chunks

### Why
- Token limits
- Better retrieval accuracy

### Config
- Max size: 496 tokens

### Structure
{
  "id": "file_path_0",
  "content": "chunk text"
}

---

## 📌 6. JSON vs JSONL
- JSON → full structure → json.load()
- JSONL → line-by-line → json.loads(line)

---

## 📌 7. RAG (Retrieval-Augmented Generation)

### Pipeline
1. Ingest documents
2. Chunk data
3. Generate embeddings
4. Store in vector DB
5. Embed query
6. Compute similarity
7. Retrieve top-K
8. Generate response

### Retrieval
similarity = cosine(query_embedding, chunk_embedding)

### Optimization
- Embed query once

### Filtering
- Use similarity threshold

---

## 📌 8. Environment Variables
- Store API keys securely

### Temporary
export OPENAI_API_KEY="key"

### Persistent
~/.bashrc

### Python
os.environ["OPENAI_API_KEY"]

---

## 📌 9. HTTPX
- Python HTTP client

### Features
- Sync & Async
- Timeout support

### Example
httpx.post(url, json=data, timeout=30)

### Errors
- 404 → wrong URL
- Unknown provider → wrong base URL
- Missing import

---

## 📌 10. NumPy
- np.dot(v1, v2)
- np.linalg.norm(v)

---

## 📌 11. File Handling & JSON
- Write: json.dump(data, f)
- Read: json.load(f)
- JSONL: json.loads(line)

### Issue
- set {} ❌ not serializable
- list [] ✅

---

## 📌 12. Async Processing
- Parallel API calls using asyncio
- Faster for bulk embeddings

---

## 📌 13. Deployment (Vercel)
- Public repo required
- Public URL required

### Constraints
- Auth tokens expire (~1 hour)
- Requires live backend

---

## 📌 14. End-to-End Pipeline

Raw Documents
   ↓
Chunking (≤496 tokens)
   ↓
JSONL (chunks)
   ↓
Embedding Generation
   ↓
Vector Storage
   ↓
Query Embedding
   ↓
Cosine Similarity
   ↓
Top-K Retrieval
   ↓
LLM Response

---

## 📌 15. Best Practices
- Embed query once
- Normalize vectors
- Chunk large data
- Store text + embeddings
- Use async for speed
- Apply similarity threshold
- Handle JSON vs JSONL correctly

---

## 📌 16. Applications
- Semantic search
- Chatbots (RAG)
- Recommendation systems
- Multimodal search

---

## 📌 17. Project Use
- Handle text + image data
- Use multimodal embeddings
- Build RAG pipeline
- Retrieve + generate responses

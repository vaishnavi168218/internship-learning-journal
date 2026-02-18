# Module 3: topics discussion, conceptual parts, specialized API interaction, API key, proxy usage, LLMs, transformers, tokens, vector, self attention, context limitations, embeddings, models, hugging face, multimodal embeddings, topic modeling, vector databases, Chroma DB, Lance DB, retrieval augmented generation (RAG), hybrid RAG, typesense, B64 encoding, image and audio processing, vision models, video analysis, frames, function calling, travel agent example, schemas, SQL database interaction, tools, agents, LLM eval, prompt engineering, testing, YAML file, assertions, cost effectiveness, regression, commercial applications.

### 1. How LLMs Work
- LLMs are not sentient; they are mathematical models based on transformers
- Text is broken into **tokens** (sub-word units); each token ~1600-dim vector
- Internally: large matrix operations on token embeddings
- **Self-Attention**: mechanism to resolve contextual references (e.g., what does "it" refer to?)
- Output = probability distribution over next tokens → picks most likely

### 2. Context Limitations & Hallucination
- LLMs have a fixed **context window** (was ~128K tokens; now up to ~1M)
- Hallucination often stems from losing context mid-conversation
- Analogous to aphasia — words produced but lose meaningful grounding

### 3. Embeddings
- Embedding models convert text (or images/audio) to numeric vectors
- Used for semantic similarity search (not just keyword matching)
- **Multimodal embeddings**: map text + images + audio into same vector space
- Sources: HuggingFace (free, leaderboard), OpenAI embeddings API
- Use cases: anomaly detection, spam filtering, semantic search

### 4. Topic Modeling
- Use embeddings to cluster documents by meaning, not just keywords
- Enables context-aware search → finds related content even without exact keyword match
- Overcomes the core failure of traditional keyword search

### 5. Vector Databases
- Store large volumes of embeddings on disk (beyond in-memory limits)
- Supported by: DuckDB, SQLite, PostgreSQL, ChromaDB, LanceDB
- Enables efficient similarity search at scale

### 6. RAG (Retrieval Augmented Generation)
- Solves context window limitation by retrieving relevant chunks at query time
- Flow: chunk docs → embed → store → on query, retrieve top-k → inject into prompt
- Forces LLM to cite stored knowledge → reduces hallucination
- Key prompting pattern: "Answer only from these notes. Cite verbatim."

### 7. Hybrid RAG
- Combines semantic (embedding) search + keyword (exact match) search
- Tool: **Typesense** (run via Docker)
- Use case: want contextual results BUT also require specific keywords to appear
- Example: searching "Podman" commands — don't want generic Docker results

### 8. Base64 Encoding
- Converts binary data (images, audio) to text for API transmission
- 3 bytes → 4 ASCII chars; lossless encode/decode
- Required to send images/audio to LLMs via REST APIs

### 9. Vision Models
- Videos = sequence of frames → send sampled frames (e.g., every 10s) to LLM
- Use cases:
  - Exam proctoring: detect cheating patterns from screen recordings
  - Workplace safety: flag safety violations from factory footage
- LLMs handle low-quality video surprisingly well

### 10. Prompt Engineering
- Most critical factor for consistent, scalable LLM applications
- Best practices:
  - Be detailed and specific
  - Use **XML tags** to structure instructions vs examples
  - Use **Markdown** to format expected output
  - Use **JSON schemas** for structured output
  - Document all prompts + outputs (working and non-working)
  - Re-test prompts when switching models (behavior differs per model)

### 11. Sentiment Analysis
- Classify text as positive/negative/neutral
- Use cases: trading bots (analyze financial news), election monitoring, brand tracking

### 12. Text Extraction (Structured Output from Unstructured Data)
- Extract specific fields from invoices, PDFs, scanned docs → return as JSON
- Define a **JSON schema** → LLM responds in that exact structure
- Replaces expensive OCR pipelines and manual data entry
- High commercial value (e.g., Hyperbots — $100M market opportunity)

### 13. Function Calling
- Bridge between natural language input and structured backend functions
- Define function schemas (name, parameters, types, required fields)
- LLM extracts relevant args from user prompt → calls correct backend function
- Supports multi-function "tools" list
- Use cases:
  - Natural language → SQL query execution
  - Voice-driven travel booking agent
  - Any app where user speaks/types freely but backend needs structured data

### 14. Agents & Tools
- Agents = LLMs that can autonomously call tools/functions in a loop
- Tools = list of function schemas the LLM can choose from
- MCP (Model Context Protocol) = standardized version of this pattern (covered in Year 3)

### 15. LLM Evaluation & Testing (promptfoo)
- Tool: **promptfoo** — YAML-based LLM evaluation framework
- Define: prompts + providers (models) + assertions (tests)
- Assertion types: `contains-all`, `llm-rubric`, custom
- Metrics tracked: accuracy, token cost, response latency
- Key use cases:
  - Compare models (e.g., GPT-4o vs GPT-3.5) on same task
  - Catch **prompt regression** when models update
  - Ensure cost-effectiveness at scale
- Open-source model alternative: avoids vendor sunset risk

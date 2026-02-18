 ## Key Learnings ##

## 1. How LLMs Work

- LLMs are **not sentient** — they are mathematical models based on **transformer architecture**
- Text is broken into **tokens** (sub-word units); each token represented as a ~1600-dimensional vector
- Internally: large **matrix operations** on token embeddings — that's all that's happening
- **Self-Attention**: mechanism to resolve contextual references  
  _e.g. "This animal was too tired to cross the road because **it** was tired" — does "it" refer to the animal or the road?_
- Output = probability distribution over next tokens → model picks the most likely one
- LLMs make **educated guesses** based on an underlying mathematical model — not reasoning

---

## 2. Context Limitations & Hallucination

- LLMs have a fixed **context window** (was ~128K tokens; expanded to ~1M tokens recently)
- **Hallucination** often happens when the model loses context mid-conversation
- Analogous to **aphasia** — words are produced but lose meaningful grounding
- Even with 1M tokens, that's still a small window for large codebases or long-running projects
- **Key insight:** You can't fix hallucination by just using a better model — you fix it by giving better context

---

## 3. Embeddings

- Embedding models convert text (or images/audio) to **numeric vectors**
- These vectors encode **semantic meaning** — similar meanings = similar vectors (close in vector space)
- Used for semantic similarity search (not just keyword matching)
- **Multimodal embeddings**: map text + images + audio into the **same vector space**
  - This is how your phone finds all photos of "cats" — image and text mapped together
- Sources:
  - [HuggingFace](https://huggingface.co) — free models, leaderboard for comparison
  - OpenAI Embeddings API — requires API call to their servers
- Use cases: anomaly detection, spam filtering, semantic search, recommendation systems

---

## 4. Topic Modeling

- Use embeddings to cluster documents by **meaning**, not just keywords
- Enables context-aware search → finds related content even **without exact keyword match**
- Overcomes the core failure of traditional keyword search (Google before semantic era)
- Flow: embed documents → compute similarities → cluster into topics

---

## 5. Vector Databases

- Store large volumes of embeddings on disk (beyond in-memory limits)
- Supported by: **DuckDB**, **SQLite**, **PostgreSQL**, **ChromaDB**, **LanceDB**
- Enables efficient **similarity search** at scale
- When running in Docker — use volume mounts (`-v`) to **persist data** after container stops

---

## 6. RAG — Retrieval Augmented Generation

> Solves the context window limitation by retrieving relevant chunks at query time.

**Flow:**
```
Document → Chunk → Embed → Store in Vector DB
                                    ↓
User Query → Embed → Similarity Search → Retrieve Top-K Chunks → Inject into Prompt → LLM Response
```

- Forces LLM to **cite stored knowledge** → reduces hallucination dramatically (doesn't eliminate)
- Key prompting pattern:
  ```
  "Answer only from these notes. Cite verbatim from notes."
  ```
- **Chunking strategy matters** — bad chunks = bad retrieval = bad answers
- Used in production by companies to convert internal knowledge bases into AI-queryable systems

---

## 7. Hybrid RAG

- Combines **semantic (embedding) search** + **keyword (exact match) search**
- Best of both worlds: contextual relevance + keyword precision
- Tool: **[Typesense](https://typesense.org)** (run via Docker)
- Use case: searching "Podman" commands — don't want generic Docker results, but want container context
- Analogy: Google's AI overview = hybrid RAG (shows AI-generated answer + keyword-matched links)

---

## 8. Base64 Encoding

- Converts **binary data** (images, audio, video frames) to **text** for API transmission
- 3 bytes → 4 ASCII characters; **lossless** encode/decode
- Required to send images/audio to LLMs via REST APIs
- Videos = sequence of frames → sample frames (e.g., every 10s) → send as Base64
- No information is lost — the LLM decodes it back on its end

---

## 9. Vision Models

- You can send **image frames** to LLMs for visual understanding
- Videos = frames → send sampled frames at intervals (not continuous stream = cheaper)
- **Real-world use cases:**
  - 🎓 **Exam proctoring** — detect cheating from screen recording patterns (stillness → sudden activity)
  - 🏭 **Workplace safety** — query factory footage in plain English: *"Where are safety violations?"*
  - 🐱 **Smart home** — detect when your cat leaves/enters the house
- LLMs handle low-quality video **better than expected** due to ML reconstruction

---

## 10. Prompt Engineering

> Your prompt quality determines application quality — not the model.

**Best practices:**
- Be **detailed and specific** in your prompts
- Use **XML tags** to separate instructions from examples:
  ```xml
  <instruction>Do X</instruction>
  <example>Input: ... Output: ...</example>
  ```
- Use **JSON schemas** to define structured output format
- Use **Markdown** to format expected output
- **Document all prompts** — what worked, what didn't, and the outputs
- When you **switch models**, re-test everything — same prompt ≠ same behavior across models
- Store prompts per model version (e.g., GPT-4.1-nano logs ≠ GPT-4o logs)

---

## 11. Sentiment Analysis

- Classify text as positive / negative / neutral
- Use cases:
  - 📈 Trading bots — analyze financial news → buy/hold/sell signal
  - 🗳️ Election monitoring — track public sentiment on policies
  - 📱 Brand monitoring — measure Tik Tok / social media buzz at scale
- Replaces expensive human analysis pipelines with scalable automated classification

---

## 12. Text Extraction (Structured Output from Unstructured Data)

> From messy documents → clean structured JSON. This is a $100M+ problem space.

- Extract specific fields from invoices, PDFs, scanned docs → return as **JSON**
- Define a **JSON schema** → LLM responds in that exact structure
- Example schema fields for an invoice:
  ```json
  { "date": "...", "supplier_name": "...", "amount": "...", "invoice_number": "..." }
  ```
- Replaces expensive OCR pipelines and manual data entry
- Real example: Indian election PDFs from 1950s–60s → structured table in **15 seconds** vs 2 weeks manually
- Companies building entire businesses on this (e.g., **Hyperbots**)

---

## 13. Function Calling

> Bridge between messy human language and structured backend code.

**Core pattern:**
```
User says anything in natural language
    ↓
LLM extracts structured args via schema
    ↓
Your backend function is called with those args
    ↓
Result returned to user
```

**Why it matters:**
- Users can speak/type freely in any language — Hindi, Tamil, English — and your app still works
- Eliminates expensive UI development for one-off business queries
- Natural language → SQL execution without a developer

**Function schema example:**
```json
{
  "type": "function",
  "function": {
    "name": "schedule_meeting",
    "parameters": {
      "date": { "type": "string", "description": "Format: YYYY-MM-DD" },
      "time": { "type": "string", "description": "Format: HH:MM" },
      "meeting_room": { "type": "string" }
    },
    "required": ["date", "time", "meeting_room"]
  }
}
```

- **Tools** = list of function schemas the LLM can choose from
- If user gives incomplete info → workflow asks follow-up questions to fill missing args

---

## 14. Agents

- Agents = LLMs that can **autonomously call tools/functions in a loop**
- They decide which function to call, call it, get the result, and continue
- **MCP (Model Context Protocol)** = standardized version of this pattern (deeper coverage in Year 3)
- Function calling is the foundation — agents are function calling + decision loop

---

## 15. LLM Evaluation & Testing (promptfoo)

> Never ship an LLM feature without automated tests on your prompts.

**Tool: [promptfoo](https://promptfoo.dev)**  
YAML-based LLM evaluation framework

**YAML structure:**
```yaml
prompts:
  - "Summarize this: {{text}}"

providers:
  - openai:gpt-4o
  - openai:gpt-3.5-turbo

tests:
  - vars:
      text: "Some input"
    assert:
      - type: contains-all
        value: ["open source", "LLM"]
      - type: llm-rubric
        value: "Response should be concise and accurate"
```

**What it measures:**
| Metric | Why it matters |
|--------|----------------|
| ✅ Correctness | Did it pass all assertions? |
| 💰 Token cost | Cheaper model = more scalable app |
| ⚡ Latency | Faster = better user experience |
| 🔁 Regression | Did a model update break your prompts? |

**Key finding from lecture:**  
GPT-3.5 vs GPT-4o on same task → 3.5 used **1/10th the tokens** and responded in **1/4 the time** — both passed all tests. At scale, that's a massive cost difference.

**Use open-source models** (via HuggingFace / Llama) to avoid **vendor sunset risk** — if the API shuts down, your app dies.

---


## 🛠️ Tools & Libraries Referenced

| Tool | Purpose |
|------|---------|
| `sentence-transformers` | Local embedding generation |
| `ChromaDB` / `LanceDB` | Vector database storage |
| `DuckDB` / `SQLite` / `PostgreSQL` | DB with vector search support |
| `Typesense` | Hybrid RAG (keyword + semantic) |
| `promptfoo` | LLM evaluation and testing |
| `HuggingFace` | Free models + leaderboard |
| `aipipe.org` | Proxy for OpenAI/Gemini API access |
| Base64 encoding | Sending images/audio to LLMs via API |

---


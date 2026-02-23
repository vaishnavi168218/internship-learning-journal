# Learnings — API, Embeddings, Multimodal AI & Function Calling

## 1. APIs are Structured Contracts
- Every API call follows a strict structure: URL + headers + JSON body.
- Small mistakes (wrong endpoint, headers) break the entire system.
- Timeouts must be increased for LLM workloads.

## 2. Security via Environment Variables
- API keys should never be hardcoded.
- `.bashrc` ensures persistent and secure access.
- Prevents accidental leaks in version control.

## 3. LLMs are Stateless
- No memory exists between requests.
- Context must be explicitly passed every time.
- Chat history = simulated memory.

## 4. Memory = Message Accumulation
- Append both user and assistant messages.
- Full conversation is sent on each request.
- Enables contextual understanding.

## 5. Base64 is a Bridge, Not Compression
- Converts binary → text for API compatibility.
- No loss of data.
- Essential for sending images.

## 6. Embeddings Capture Meaning, Not Words
- Similar words map to nearby vectors.
- Works beyond spelling or syntax.
- Enables semantic search.

## 7. Similarity is Mathematical, Not Logical
- Cosine similarity measures direction, not distance alone.
- High similarity = similar meaning.
- Core of search and retrieval systems.

## 8. Vector Search Powers Intelligence
- Store embeddings with data.
- Compare query vector with stored vectors.
- Retrieve top matches → better answers.

## 9. Multimodal = Unified Understanding
- Text and images share the same vector space.
- Enables cross-modal reasoning.
- Required for real-world applications.

## 10. Images Must Be Converted to Text Form
- Base64 encoding enables image processing by LLMs.
- Proper formatting is required in API requests.

## 11. Function Calling Brings Structure
- Converts free-text output into strict JSON.
- Enables automation and integration.
- Critical for production systems.

## 12. Schema Design Controls Output Quality
- Strong schema → predictable output.
- Weak schema → inconsistent results.
- Validation happens at design level.

## 13. AI Pipelines Matter More Than Prompts
- Systems combine multiple steps:
  - encoding
  - embedding
  - retrieval
  - generation
- Prompt alone is not sufficient.

## 14. Debugging is Mostly Integration Work
- Errors usually come from:
  - wrong formats
  - invalid JSON
  - bad endpoints
- Reading errors carefully saves time.

## 15. Performance Requires Optimization
- Async calls improve speed.
- Avoid redundant computations.
- Optimize for cost vs accuracy.

## 16. Model Choice Impacts Output
- Smaller models → faster, cheaper, less accurate.
- Larger models → slower, expensive, more accurate.
- Select based on task complexity.

## 17. Real-World AI = System Design
- Not just using an LLM.
- Requires orchestration of multiple components.
- Reliability depends on the pipeline.

## 18. Practical Insight
- Chatbots = history management problem.
- Image understanding = encoding + multimodal + structure.
- Production AI = combining all concepts effectively.

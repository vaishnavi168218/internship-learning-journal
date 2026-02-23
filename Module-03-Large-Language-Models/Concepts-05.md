# Core Concepts — API, Embeddings, Multimodal AI & Function Calling

## 1. API Communication Fundamentals
- Every API call requires:
  - URL (endpoint)
  - Headers (authentication, content type)
  - Body (JSON payload)
- HTTP clients like `httpx` replicate `curl` behavior in code.
- Timeout handling is essential for long-running AI responses.

## 2. Environment Variable Management
- Store sensitive data (API keys) in environment variables.
- `.bashrc` ensures automatic loading on terminal startup.
- Prevents accidental exposure in source code or GitHub.

## 3. Stateless Nature of LLMs
- LLMs do not retain memory between requests.
- Memory is simulated by sending full conversation history.
- Message roles:
  - `system/developer`: behavior control
  - `user`: input
  - `assistant`: model response

## 4. Chatbot Architecture with Memory
- Maintain a list of messages.
- Append user input and assistant output continuously.
- Pass entire history on every API call.
- Enables contextual, multi-turn conversations.

## 5. Base64 Encoding (Binary ↔ Text Bridge)
- Converts binary data (images) into text format.
- Required because APIs accept text, not raw binary.
- Encoding is lossless and reversible.
- Enables image input for LLMs.

## 6. Embeddings (Semantic Representation)
- Text is converted into high-dimensional vectors.
- Each dimension represents a latent semantic feature.
- Similar meanings → similar vectors.
- Not dependent on exact word matching.

## 7. Vector Similarity Metrics
### Euclidean Distance
- Measures straight-line distance between vectors.
- Lower distance = higher similarity.

### Cosine Similarity
- Measures angle between vectors.
- Higher score = higher similarity.
- Formula:
  cos(θ) = (A · B) / (|A| × |B|)

## 8. Vector-Based Search (Manual Vector DB)
- Store embeddings with original data.
- Convert query into embedding.
- Compare with stored vectors.
- Rank based on similarity.
- Retrieve top-k results.

## 9. Multimodal Embeddings
- Text and images embedded into same vector space.
- Enables cross-modal comparison (image ↔ text).
- Useful for real-world mixed data systems.
- Requires specialized models (e.g., Jina AI).

## 10. Image Handling in AI Pipelines
- Convert image → Base64 → send in API request.
- Use structured format:
  - `type: text`
  - `type: image_url`
- Allows LLM to process visual + textual input together.

## 11. Function Calling (Structured Output)
- Converts unstructured LLM output into structured JSON.
- Defined using a schema (parameters, types, required fields).
- Ensures predictable and machine-readable responses.
- Key parameters:
  - `tools`
  - `tool_choice`

## 12. Schema Design Principles
- Use strict typing (string, number, etc.).
- Define required fields explicitly.
- Add descriptions for clarity.
- Wrap schema correctly:
  {
    "type": "function",
    "function": {...}
  }

## 13. Structured Data Extraction Pipeline
Flow:
Image → Base64 → API call → Function schema → JSON output

- Extracts:
  - Manufacturing date
  - Expiry date
  - Product name
  - Answers
- Automates data extraction from unstructured inputs.

## 14. Error Handling & Debugging
Common issues:
- Incorrect API endpoints
- Missing API keys
- JSON parsing errors
- Invalid schema structure
- Serialization errors (set vs list)

Key insight:
- Most failures are integration issues, not model issues.

## 15. Performance Optimization
- Use async requests for batch processing.
- Avoid repeated embedding generation.
- Optimize chunk sizes for retrieval.
- Balance cost vs accuracy (model selection).

## 16. Model Selection Strategy
- Lightweight models (nano):
  - Faster, cheaper
  - Lower accuracy
- Larger models:
  - Better reasoning
  - Higher cost
- Choose based on use case complexity.

## 17. Real-World System Design Insight
- AI systems are pipelines, not single models.
- Core components:
  - Input processing
  - Embedding
  - Retrieval
  - Generation
  - Output structuring
- Reliability depends on integration, not just prompts.

## 18. End-to-End Use Case Understanding
### Chatbot System
- Input → history → API → response → append → repeat

### Image Data Extraction System
- Image → encode → API → function call → structured JSON


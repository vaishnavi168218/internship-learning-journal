# Key Learnings — Embeddings, Multimodal AI & RAG

## 1. Embeddings
- Text, images, and other data can be converted into numerical vectors.
- These vectors capture semantic meaning, not just exact words.
- Similar content results in similar vectors in high-dimensional space.
- Embeddings are cheaper and faster than full LLM responses.

## 2. Similarity Measurement
- Cosine similarity is used to compare vectors.
- It measures how close two meanings are, not exact matches.
- Normalization ensures similarity scores remain consistent.
- Dot product and vector norms form the mathematical base.

## 3. Multimodal Understanding
- Text and images can be represented in the same vector space.
- This allows direct comparison between different data types.
- Useful when working with mixed datasets like forums or social platforms.

## 4. Importance of Chunking
- Large documents must be split due to token limits.
- Smaller chunks improve retrieval accuracy.
- Each chunk acts as an independent searchable unit.

## 5. Vector Storage
- Embeddings must be stored along with their original text and source.
- This enables retrieval of meaningful context later.
- Even simple JSON-based storage can simulate a vector database.

## 6. Retrieval Logic in RAG
- Convert the user query into an embedding once.
- Compare it with all stored embeddings.
- Rank results based on similarity.
- Select top relevant chunks for answering.

## 7. Efficiency Considerations
- Avoid recomputing embeddings unnecessarily.
- Sequential API calls are slow for large datasets.
- Asynchronous processing significantly improves speed.

## 8. JSON vs JSONL Handling
- JSONL requires line-by-line parsing.
- Using incorrect parsing methods leads to errors.
- Proper data format handling is critical in pipelines.

## 9. API and Environment Management
- API keys should be stored securely using environment variables.
- Incorrect endpoints or base URLs are common failure points.
- Timeout handling prevents long-running failures.

## 10. Error Handling and Debugging
- Many issues come from small mistakes (wrong URL, missing imports).
- Understanding error messages speeds up debugging.
- Data type issues (like using sets instead of lists) can break pipelines.

## 11. RAG System Design
- RAG connects retrieval systems with generation models.
- It allows LLMs to answer based on external knowledge.
- The quality of retrieval directly impacts the final answer.

## 12. Real-World Application Insight
- Systems must handle both structured and unstructured data.
- Multimodal capability is essential for modern applications.
- Proper pipeline design is more important than individual components.

## 13. Deployment Awareness
- Applications must be publicly accessible for evaluation.
- Authentication systems have time limits.
- Timing and execution strategy matter in real-world submissions.

## 14. Overall Understanding
- Building AI systems is about combining multiple components:
  chunking, embedding, storage, retrieval, and generation.
- Small implementation details can significantly impact performance.
- Optimization, structure, and correctness are equally important.

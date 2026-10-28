# prompt-caching
This video explores two primary strategies for implementing **prompt caching** in AI applications to optimize performance and reduce operational costs.

### 1. Exact Query Caching

This approach is designed for scenarios where users submit identical prompts repeatedly.

*   **Mechanism:** The system acts as a high-speed **key-value store** (similar to a hashmap). When a user sends a query, the system first checks the cache; if the exact text exists, it returns the stored response immediately, bypassing the LLM.
*   **Staleness Management:** Because responses might become outdated (e.g., changing road conditions), the speaker suggests using **time-to-live (TTL) timeouts** or **Least Recently Used (LRU)** eviction policies to remove old or irrelevant data.

### 2. Semantic Caching 

This method handles prompts that differ in wording but share the same underlying meaning (e.g., "I am going from Bangalore to Mysore" vs. "I am traveling to Mysore from Bengaluru").

*   **Mechanism:** Instead of exact text matching, queries are converted into **vector embeddings** (mathematical representations). The system performs an **approximate nearest neighbor search** to find cached queries that are semantically similar.
*   **Similarity Scoring:** A similarity threshold (e.g., **\> 0.9**) is typically set. If a stored vector matches the new query vector within this threshold, the system provides the cached response.

### Trade-offs and Considerations

Implementing these caches involves specific architectural trade-offs:

*   **Latency:** While exact caching is very fast, **semantic caching** introduces higher latency due to the complexity of vector search algorithms.
*   **Accuracy:** Semantic caching risks providing "inexact" answers. If two queries are mathematically close but contextually different (e.g., different budget requirements), the system might incorrectly return a cached response.
*   **Cost Efficiency:** Although caching requires additional engineering, it is significantly cheaper than repeatedly calling an LLM, which must process every request through its full attention blocks.

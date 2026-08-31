# 🚀 Hybrid RAG System with RRF & Ragas Evaluation

An advanced Retrieval-Augmented Generation (RAG) pipeline that combines Semantic Search and Keyword Search to deliver highly accurate context to a Groq-powered LLM. The pipeline is automatically graded for quality using the **Ragas** evaluation framework.

---

## ✨ Key Features

- **Hybrid Retrieval Mechanism:** Combines dense vector search (**ChromaDB**) with sparse keyword search (**BM25**) to find the most relevant document chunks.
- **Reciprocal Rank Fusion (RRF):** Intelligently merges and re-ranks the results from both ChromaDB and BM25 to ensure the best possible context is sent to the LLM.
- **Fast LLM Generation:** Powered by **Groq** (`ChatGroq`) for lightning-fast response generation.
- **Automated Evaluation:** Uses **Ragas** to score the pipeline across four key metrics, ensuring the LLM doesn't hallucinate and accurately relies on the provided documents.

---

## 🏗️ Architecture Flow

1. **Document Processing:** Loads a local PDF (`Static GK 2025.pdf`), splits it into chunks of 1400 characters, and hashes IDs to avoid duplication.
2. **Indexing:**
   - Embeds chunks using `all-MiniLM-L6-v2` and stores them in a persistent **ChromaDB**.
   - Tokenizes chunks and builds a **BM25** corpus for exact-match keyword search.
3. **Retrieval (RRF):** Queries both databases, limits ChromaDB by a distance threshold (1.5), and mathematically fuses the ranks together using RRF.
4. **Generation:** Passes the fused text strings to Groq to generate a final answer.
5. **Evaluation:** Packages the Query, Response, Retrieved Contexts, and Ground Truth into a HuggingFace `Dataset` and grades it using Ragas.

---

## ⚙️ Prerequisites & Setup

### 1. Install Dependencies

You will need the following Python libraries installed:

```bash
pip install langchain-community langchain-text-splitters chromadb sentence-transformers rank-bm25 datasets ragas pypdf langchain-groq python-dotenv langchain-huggingface
```

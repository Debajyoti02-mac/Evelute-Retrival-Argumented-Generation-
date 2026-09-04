# 🚀 Hybrid RAG System with RRF & Ragas Evaluation

An end-to-end Retrieval-Augmented Generation (RAG) pipeline combining dense and sparse search, powered by a local **Ollama** model (`qwen2.5:1.5b`) and graded with **Ragas**.

---

## ✨ Key Features

* **Hybrid Retrieval:** Dense vector search (**ChromaDB**) + sparse keyword search (**BM25**).
* **Reciprocal Rank Fusion (RRF):** Fuses and re-ranks top results from both retrievers.
* **Local & Lightweight:** Uses **Ollama** (`qwen2.5:1.5b`) to run fast generation locally without cloud API costs or high memory overhead.
* **Automated Evaluation:** Grades performance using **Ragas** metrics (`faithfulness`, `answer_relevancy`, `context_precision`, `context_recall`).

---

## 🏗️ Architecture Flow

1. **Indexing:** Splits local documents into 1,400-character chunks, embeds them with `all-MiniLM-L6-v2` into **ChromaDB**, and tokenizes a **BM25** corpus.
2. **Retrieval:** Queries ChromaDB and BM25 simultaneously, applies a distance threshold, and combines results via **RRF**.
3. **Generation:** Passes fused contexts to **`qwen2.5:1.5b`** via `ChatOllama` (`keep_alive="0s"`) to synthesize the answer.
4. **Evaluation:** Builds a HuggingFace `Dataset` and runs Ragas evaluation.

---

## ⚙️ Quickstart

### 1. Install Dependencies

```bash
pip install langchain-community langchain-text-splitters chromadb sentence-transformers rank-bm25 datasets ragas pypdf langchain-ollama python-dotenv langchain-huggingface

```

### 2. Pull the Local Model

```bash
ollama pull qwen2.5:1.5b

```
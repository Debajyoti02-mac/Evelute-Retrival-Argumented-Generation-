# Multi-Paradigm RAG Evaluation Suite

A comprehensive repository for building, benchmarking, and evaluating Retrieval-Augmented Generation (RAG) architectures—spanning traditional Dense RAG, Hybrid RAG, and fully autonomous Agentic RAG pipelines evaluated with **Ragas**.

---

## 📌 Repository Overview

This suite demonstrates the evolutionary steps of building modern RAG systems and systematically evaluating their performance using automated metrics:

```
rag-evaluation-suite/
│
├── 01_faiss_dense_eval/          # Stage 1: Standard Dense RAG (FAISS + Vector Search)
│   └── dense_eval.py
│
├── 02_hybrid_rrf_eval/           # Stage 2: Hybrid Retrieval RAG (ChromaDB + BM25 + RRF)
│   └── hybrid_eval.py
│
├── 03_agentic_rag_eval/          # Stage 3: Dynamic Tool-Calling Agentic RAG & Trajectory Eval
│   ├── Static GK 2025.pdf
│   └── agentic_eval.py
│
└── README.md                     # Root Documentation

```

---

## 🛠 Architectural Comparison

| Module | Retrieval Strategy | Decision Engine | Tools / Features | Main Evaluation Scope |
| --- | --- | --- | --- | --- |
| **01. FAISS Dense Eval** | Single-vector semantic lookup | Deterministic Pipeline | FAISS Vector Store | Basic retrieval recall & faithfulness |
| **02. Hybrid RRF Eval** | Dense Vector + BM25 Sparse | Reciprocal Rank Fusion | ChromaDB + `rank_bm25` | Fusion accuracy & context precision |
| **03. Agentic RAG Eval** | Dynamic Hybrid Retrieval | `ChatGroq` (`qwen/qwen3.6-27b`) | `Hybrid_Retrive` + `calculator` | Trajectory capture & end-to-end multi-tool eval |

---

## 🚀 Pipeline Modules

### 1. Dense RAG Evaluation (`01_faiss_dense_eval`)

* **Focus:** Standard baseline RAG using FAISS vector indexing.
* **Mechanism:** Converts document chunks into dense embeddings and retrieves top-$k$ documents based on cosine/L2 distance.
* **Eval Target:** Benchmark basic LLM response grounding vs. standard vector retrieval.

### 2. Hybrid RAG Evaluation (`02_hybrid_rrf_eval`)

* **Focus:** Overcoming vocabulary mismatch using sparse-dense fusion.
* **Mechanism:**
* Dense retrieval via ChromaDB (`all-MiniLM-L6-v2`).
* Sparse keyword search via `rank_bm25`.
* Context combination via **Reciprocal Rank Fusion (RRF)** ($1 / (rank + 60)$).


* **Eval Target:** Measure improvements in `ContextPrecision` and `ContextRecall` over pure dense retrieval.

### 3. Agentic RAG Evaluation (`03_agentic_rag_eval`)

* **Focus:** Multi-step reasoning and dynamic tool selection.
* **Mechanism:**
* Groq LLM binds custom tools (`Hybrid_Retrive` and `calculator`).
* Agent dynamically decides whether to search local documents or perform arithmetic computations.
* Captures intermediate execution trajectories to pass retrieved context chunks to Ragas.


* **Eval Target:** `Faithfulness`, `AnswerRelevancy`, `ContextPrecision`, and `ContextRecall` across hybrid tool executions.

---

## 📊 Evaluation Framework (Ragas Integration)

All modules are evaluated using **Ragas** with a local HuggingFace embedding model (`all-MiniLM-L6-v2`) and an evaluation LLM (`llama-3.1-8b-instant` via Groq):

* **Faithfulness:** Measures if the generation is strictly grounded in the retrieved context chunks.
* **Answer Relevancy:** Measures how directly the generated answer addresses the input query.
* **Context Precision:** Evaluates if relevant chunks are ranked at the top of the context payload.
* **Context Recall:** Verifies if all ground-truth facts were successfully retrieved by the engine.

---

## ⚙️ Installation & Setup

1. **Clone the repository:**
```bash
git clone https://github.com/your-username/rag-evaluation-suite.git
cd rag-evaluation-suite

```


2. **Set up a virtual environment:**
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

```


3. **Install required packages:**
```bash
pip install -U langchain langchain-groq langchain-community \
               chromadb faiss-cpu rank_bm25 ragas datasets \
               sentence-transformers numexpr python-dotenv pypdf

```


4. **Environment Variables:**
Create a `.env` file in the root directory:
```env
GROQ_API_KEY=your_groq_api_key_here

```



---

## 📜 License

This project is licensed under the MIT License.

---

---

# RAG Pipeline with Ragas Evaluation

An end-to-end Retrieval-Augmented Generation (RAG) system built with **LangChain**, **FAISS**, **Sentence Transformers**, and a local **Ollama** model (`qwen2.5:1.5b`). It includes automated pipeline performance grading using the **Ragas** evaluation framework.

---

## 📌 Features

* **Document Processing:** PDF loading and recursive text splitting.
* **Vector Indexing:** Dense embeddings generated via `HuggingFaceEmbeddings` (`all-MiniLM-L6-v2`) indexed with `FAISS`.
* **LLM Generation:** Fast, local context-aware responses powered by **Ollama** (`qwen2.5:1.5b`).
* **RAG Evaluation:** Benchmarks pipeline quality using **Ragas** metrics:
* *Faithfulness*
* *Answer Relevancy*
* *Context Precision*
* *Context Recall*



---

## ⚙️ Prerequisites

* Python 3.10+
* Ollama installed locally ([Download Ollama](https://ollama.com))

---

## 🚀 Getting Started

### 1. Clone & Set Up Virtual Environment

```bash
git clone <your-repository-url>
cd MultiAgentic-RAG

# Create virtual environment
python -m venv .venv2

# Activate virtual environment
# On macOS/Linux:
source .venv2/bin/activate
# On Windows:
# .venv2\Scripts\activate

```

### 2. Pull the Local Model

```bash
ollama pull qwen2.5:1.5b

```
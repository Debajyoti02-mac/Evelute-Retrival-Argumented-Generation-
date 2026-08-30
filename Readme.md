# RAG Pipeline with Ragas Evaluation

An end-to-end Retrieval-Augmented Generation (RAG) system built with **LangChain**, **FAISS**, **Sentence Transformers**, and **Groq LLM**. It includes automated pipeline performance grading using the **Ragas** evaluation framework.

---

## 📌 Features

- **Document Processing:** PDF loading and recursive text splitting.
- **Vector Indexing:** Dense embeddings generated via `SentenceTransformer` (`all-MiniLM-L6-v2`) indexed with `FAISS`.
- **LLM Generation:** Fast context-aware responses powered by Groq (`ChatGroq`).
- **RAG Evaluation:** Benchmarks pipeline quality using **Ragas** metrics:
  - _Faithfulness_
  - _Answer Relevancy_
  - _Context Precision_
  - _Context Recall_

---

## ⚙️ Prerequisites

- Python 3.10+
- A Groq API key ([Get one here](https://console.groq.com/))

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

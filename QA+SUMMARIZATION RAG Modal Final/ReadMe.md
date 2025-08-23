#  Local Retrieval-Augmented Generation (RAG) with LlamaIndex and Ollama

**Author:** Pranshu Goyal  
**Date:** August 2025  
**Python Version:** ≥ 3.10  

---

## 🔎 Overview

This repository implements a **Retrieval-Augmented Generation (RAG)** pipeline that combines:

- **[LlamaIndex](https://www.llamaindex.ai/):**  
  For document ingestion, preprocessing, chunking, embedding, and vector indexing.  
- **[Ollama](https://ollama.ai/):**  
  A local LLM runtime for efficient question answering and summarization.  

The system has been designed with **reproducibility, transparency, and resilience** in mind. It can gracefully degrade when optional components (e.g., Ollama, LlamaParse) are unavailable, while maintaining end-to-end functionality.

---

## ✨ Features

- 📂 **Document Ingestion** from multiple file types: PDF, DOCX, PPTX, MD, HTML, TXT.  
- 🧩 **Index Building** with HuggingFace embeddings + FAISS vector store.  
- ❓ **Question Answering** using retrieved context and Ollama LLM.  
- 📖 **Summarization** with broader retrieval depth and higher temperature.  
- 🖥️ **Interactive Ad-hoc Mode** for pasting raw text and querying it in real time.  
- 🔍 **Transparency Tools**:
  - Pipeline diagram (ASCII / Rich panel)  
  - Document inventory by extension  
  - Chunking estimates (size/overlap)  
  - Retrieved sources tables (with provenance)  
- ⚠️ **Lightweight PHI Detector** (heuristic-only; not HIPAA-compliant).  
- 🛡️ **Resilience**:
  - Skips Ollama-dependent demos if Ollama is not running.  
  - Falls back to `UnstructuredReader` if no LlamaParse API key is provided.  

---

## 📂 Repository Structure

```text
.
├── docs/                                           # Input documents for ingestion (user-provided)
│   └── placeholder.txt                             # Auto-created placeholder if empty
├── storage/                                        # Persisted FAISS vector index
├── logs/                                           # Query/session logs
├── notebooks/                                      # Jupyter notebooks for RAG pipeline
│   └── QA+SUMMARIZATION RAG Modal.ipynb            # Main notebook (setup, ingestion, QA, summarization)
└── README.md                                       # Project documentation
```

---

## Installation

1. Navigate into this directory:

    ```bash
    cd "QA+SUMMARIZATION RAG Modal Final"
    ```

2. (Optional) Set up a virtual environment:

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # Linux/Mac
    venv\Scripts\activate     # Windows
    ```

3. Install dependencies:

    run the notebook’s environment setup cell, which also installs conda packages if needed.

4. (Optional) Enable LlamaParse for advanced PDF parsing

Create a .env file in the root directory:

```python
LLAMA_PARSE_KEY="your-llamaparse-key"
```


# Usage

Open the notebook notebooks/rag_system.ipynb and run cells step by step.

Quickstart Workflow:

```python
# 1) Build or rebuild the index from ./docs
run_index()

# 2) Ask a question (requires Ollama running)
run_ask("What is the most common cause of oral cancer?")

# 3) Summarize a topic (requires Ollama running)
run_summarize("findings on oral cancer and ethnicity")

# 4) (Optional) Run an interactive session on pasted text
# run_interactive_process_session()
```


⸻

# Security Considerations
	•	No API keys are hardcoded.
	•	Keys such as LLAMA_PARSE_KEY are securely loaded from .env.
	•	The PHI detector is heuristic-only and does not guarantee HIPAA/GDPR compliance.

⸻

# References
	•	LlamaIndex: https://docs.llamaindex.ai
	•	Ollama: https://ollama.ai
	•	FAISS (Facebook AI Similarity Search): https://github.com/facebookresearch/faiss
	•	HuggingFace Sentence Transformers: https://www.sbert.net
	•	Unstructured: https://unstructured-io.github.io/unstructured

⸻

# Status

The system is ready-to-run:
	•	Clean, documented, and reproducible.
	•	Tested on Python 3.10 with Conda + Pip hybrid setup.

Next steps may include scaling to cloud backends, integrating evaluation benchmarks, and extending domain-specific ingestion pipelines.
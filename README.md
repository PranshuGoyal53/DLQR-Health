# Dynamic LLM Query Router (DLQR) – Healkth Case Study

Dynamic LLM Query Router for healthcare — thesis code, datasets, and benchmarks (oral-cancer biomarker case study).

DLQR-Health is the reproducible codebase for my MSc AI thesis on a Dynamic LLM Query Router (DLQR) for healthcare at University of Galway, Ireland. The system routes each incoming query to the most suitable module—structured biomarker prediction, case-based retrieval, or clinical QA—optimising for accuracy, p95 latency (<100 ms target), and ≤2 GB RAM. The repo includes training and calibration code, the routing policy head, ablations (embedding model and policy width), uncertainty/hedging logic, and an end-to-end evaluation harness (AUROC/F1, latency, throughput, cost proxy). A clinical oral-cancer biomarker scenario is provided as the primary case study, with clear hooks to swap in other domains. Research use only; not for clinical decision-making.

**Author:** Pranshu Goyal  
**Date:** August 2025  
**Environment:** Python ≥ 3.10  

## Overview

This repository provides a **production-ready, single-notebook implementation** of a **Dynamic LLM Query Router (DLQR)** for multimodal clinical decision support.  

The router dynamically dispatches user queries across three integrated modules:  

-  **Prediction** — Supervised biomarker-based disease classification (RF, XGBoost, MLP).  
-  **Case-Based Reasoning (CBR)** — Retrieval and ranking of similar clinical cases (structured + unstructured).  
-  **Retrieval-Augmented Generation (RAG)** — LLM-powered Question Answering and Summarisation.  

Key features include **temperature calibration, bandit-based exploration, circuit breakers, hedging, logging, and evaluation utilities**, making it suitable for both **academic research** and **real-world prototyping**.

---

## ⚙️ Features
- **Dynamic Query Routing** — Routes queries to Prediction, CBR, or RAG tools based on intent.  
- **LLM Intent Mixing** — Combines transformer-based classification with supervised policy nets.  
- **Resiliency** — Circuit breakers and hedging ensure graceful handling of model/tool failures.  
- **Exploration–Exploitation** — LinTS contextual bandit improves decision policies over time.  
- **Calibration** — Temperature scaling and expected calibration error (ECE) evaluation.  
- **Evaluation** — Canonical dataset splits, supervised training, and confusion matrix plots.  
- **Pretty Printing** — Rich console/UI rendering for human-friendly inspection.  

---

## 📂 Repository Structure

```text
├── data/                               # Input datasets, splits, logs, artifacts
├── reports/                            # Saved evaluation reports
├── trained_router_llm                  # Saved evaluation
├── Prediction modal Final/             # Prediction models + preprocessor artifacts
├── Case Based Reasoning Final/         # CBR artifacts (structured + text)
├── QA+SUMMARIZATION RAG Modal Final/   # RAG index & document storage
├── README.md                           # Project documentation (this file)
└── DLQR_notebook.ipynb                 # Main unified notebook implementation
```

---

## 🚀 Quick Start

### 1. Clone the repository
```bash
git clone https://github.com/PranshuGoyal53/DLQR-Health.git
```

2. Setup environment

Create a fresh environment and install dependencies:

```python
python3 -m venv dlqr_env
source dlqr_env/bin/activate   # (Linux/Mac)
dlqr_env\Scripts\activate      # (Windows)
```

Run the notebook’s environment setup cell, which also installs conda packages if needed.

3. Prepare .env file

Example .env:

```python
ROOT_DIR=.
ROUTER_DATA_DIR=./data
RANDOM_SEED=42
EMBED_MODEL=all-MiniLM-L6-v2
LLM_BACKBONE=distilbert-base-uncased
USE_LLM_INTENT=1
```

4. Run the notebook

Open in JupyterLab or VS Code, and run top-to-bottom:

jupyter lab


## Training & Evaluation

```python
# - Train Router:

train_info = load_or_train_router(
    model_dir=MODEL_DIR,
    preprocess_cfg=PREPROC,
    splits=splits,
    epochs=6
)

# - Evaluate:

eval_info = evaluate_router_model(
    preprocess_cfg=PREPROC,
    splits=splits,
    save_report_dir=REPORTS_DIR,
)

# - Visualise Confusion Matrix:

plt.imshow(eval_info["router"]["confusion_matrix"])
plt.show()
```


## Example Usage

```python
# 1. Summarisation

exc_full = execute_query(
    "SUMMARIZE the OSCC clinical context and biomarker profile into key points",
    model_dir=MODEL_DIR,
    return_full=True
)
auto_pretty(exc_full)

# 2. QA

exc_full = execute_query(
    "What are the side effects of cisplatin?",
    model_dir=MODEL_DIR,
    return_full=True
)
auto_pretty(exc_full)

# 3. Prediction

exc_full = execute_query(
    "predict", {
        "Age": 65, "Gender": "Female", "Smoking_Status": "Former",
        "Cancer_Stage": "Stage II", "IL6_Saliva": 14.5, "IL8_Saliva": 21.2,
        "TNFa_Saliva": None, "LDH_Saliva": 6.8
    },
    model_dir=MODEL_DIR,
    return_full=True
)
auto_pretty(exc_full)
```

## Citation

If you use this system in research or academic work, please cite:

@software{Goyal_DLQR-Health_Dynamic_LLM,
    author = {Goyal, Pranshu},
    title = {{DLQR-Health: Dynamic LLM Query Router for Healthcare}},
    url = {https://github.com/PranshuGoyal53/DLQR-Health/releases/tag/v1.0.0-thesis},
    version = {v1.0.0-thesis}
}

## Notes
	•	The router and helpers are self-contained; missing models or artifacts will produce warnings instead of hard errors.
	•	RAG modules may require Ollama and Sentence-Transformers models to be downloaded on first use.
	•	This system is intended as a research prototype, not a production medical device.

## License
- Code: Apache-2.0 (see `LICENSE`)
- Datasets: CC BY-NC 4.0 (see `DATA_LICENSE`)
- Model weights: CC BY-NC 4.0 (see `MODEL_LICENSE`)
- Documentation (non-code text & figures): CC BY 4.0

Note: Third-party models, datasets, and code retain their original licenses; see `THIRD_PARTY_LICENSES`.

## Legal & Safety

- **Code:** Apache-2.0 (`LICENSE`)
- **Datasets:** CC BY-NC 4.0 (`DATA_LICENSE`)
- **Model weights:** CC BY-NC 4.0 (`MODEL_LICENSE`)
- **Docs & figures:** CC BY 4.0

**Research-only; not a medical device.** See `DISCLAIMER.md` and `TERMS_OF_USE.md`.  
Third-party items remain under their original licenses (`THIRD_PARTY_LICENSES.md`).

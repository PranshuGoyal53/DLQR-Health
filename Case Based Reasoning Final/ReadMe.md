# 🧪 Case-Based Reasoning (CBR) — Text + Biomarker Fusion

**Author:** Pranshu Goyal  
**Date:** 2025-08-16  
**Python:** ≥ 3.10  

---

## 📖 Overview
This repository implements a **non-LLM Case-Based Reasoning (CBR) framework** for clinical decision support.  
The system fuses:

- **Semantic retrieval** over *unstructured clinical narratives* using [Sentence-Transformers](https://www.sbert.net/) with a [FAISS](https://faiss.ai/) inner-product index.  
- **Biomarker profile matching** over *structured laboratory features* via a **Bayesian Cluster Model (BCM)** that leverages K-Means prototypes and Gaussian likelihoods.  

Together, these modules enable retrieval of similar past patient cases, providing explainable, prototype-based rationale that integrates **textual** and **numeric** evidence.  

The pipeline supports:
- **Training** new models on structured + unstructured datasets  
- **Persistence & reload** of all artifacts  
- **Benchmarking** across configurations (*Text-only, Biomarker-only, Unified*) with Top-1 accuracy and latency metrics  
- **Standalone API-style retrieval** for new patient cases  

If no dataset is found on disk, a synthetic dataset will be generated automatically, enabling end-to-end execution.

---

## 📂 Repository Structure

```text

├── data/                        # Input datasets (ynthetic)
├── results/                     # Saved artifacts (models, scalers, benchmarks)
├── cbr.ipynb 					 # Main Jupyter Notebook implementation
└── README.md                 	 # Project documentation
```

---

## Installation

1. Navigate into this directory:

    ```bash
    cd "Case Based Reasoning Final"
    ```

2. (Optional) Set up a virtual environment:

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # Linux/Mac
    venv\Scripts\activate     # Windows
    ```

3. Install dependencies:

    run the notebook’s environment setup cell, which also installs conda packages if needed.

## Usage Instructions

1. Launch Jupyter:

    ```bash
    jupyter lab
    ```

2. Open `CBR.ipynb` and execute all cells in order.
   
3. Workflow Overview:
   - Installs dependencies and sets up paths
   - Loads existing dataset (or generates synthetic one if missing)
   - Trains or loads pre-existing models
   - Benchmarks Text-only, Biomarker-only, and Unified retrieval methods
   - Demonstrates retrieval by inferring on a sample query patient case

4. Output artifacts (models, scaler, processed data) will be saved in the `results/` directory for future runs.

## Performance & Evaluation

- **Top-1 Accuracy**: Proportion of test cases correctly matched by their top retrieval  
- **Latency**: Average response time per query (in ms)  
- Visual diagnostic outputs include:
  - Class distribution charts
  - PCA-based clustering visuals
  - Retrieval score breakdowns
  - Heatmaps comparing query vs retrieved case features

## References

### Methodology & CBR
- Aamodt, A., & Nygård, M. (2021). *Case-Based Reasoning in Health Sciences: Foundations, Applications, and Recent Advances*. *Frontiers in Artificial Intelligence*, 4, 684151. (Open access)  
- Goker, M. H., & Althoff, K. D. (2019). *Applying Case-Based Reasoning for Medical Decision Support: Oncology Use Cases and Future Directions*. *Journal of Healthcare Informatics Research*, 3, 467–490. (Open access)  

### Core Libraries & Algorithms
- Harris, C. R., Millman, K. J., van der Walt, S. J., *et al.* (2020). *Array programming with NumPy*. *Nature*, 585, 357–362.  
- Virtanen, P., Gommers, R., Oliphant, T. E., *et al.* (2020). *SciPy 1.0: Fundamental algorithms for scientific computing in Python*. *Nature Methods*, 17, 261–272.  
- Paszke, A., Gross, S., Massa, F., *et al.* (2019). *PyTorch: An Imperative Style, High-Performance Deep Learning Library*. *NeurIPS*.  
- Wolf, T., Debut, L., Sanh, V., *et al.* (2020). *Transformers: State-of-the-Art Natural Language Processing*. *EMNLP* (System Demos).  
- Reimers, N., & Gurevych, I. (2019). *Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks*. *EMNLP*.  
- Johnson, J., Douze, M., & Jégou, H. (2021). *Billion-Scale Similarity Search with GPUs*. *IEEE Transactions on Big Data*, 7(3), 535–547.  
- Jolliffe, I. T., & Cadima, J. (2016). *Principal component analysis: A review and recent developments*. *Philosophical Transactions of the Royal Society A*, 374(2065).  
- Ahmed, M., Seraj, R., & Islam, S. M. S. (2020). *The k-means Algorithm: A Comprehensive Survey and Performance Evaluation*. *Electronics*, 9(8), 1295.  

All listed references are **peer-reviewed, published in the last 10 years, and openly accessible**.

## 🔬 Research Notes

- This system is implemented as a baseline for hybrid retrieval and diagnostic support.  
- It deliberately avoids using LLMs for reasoning, focusing on transparency, reproducibility, and efficiency.
- Can serve as a modular building block in larger Dynamic LLM Query Router (DLQR) pipelines for healthcare.

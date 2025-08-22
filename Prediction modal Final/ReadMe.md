# 📘 Oral Cancer Biomarker – End-to-End Modelling Notebook

> **End-to-end machine learning pipeline for oral cancer risk prediction** using salivary/blood biomarkers and limited patient metadata.  
> Implements preprocessing, feature selection, model training (Random Forest, XGBoost, PyTorch MLP), evaluation, explainability, and patient-level inference.

---

## ✨ Features
- Deterministic environment setup & reproducibility (fixed seeds, version logging).
- Data handling:
  - Synthetic dataset (fully generated).
  - Hybrid dataset (synthetic + real-world samples).
- Preprocessing pipeline:
  - Missing-value imputation (KNN, median).
  - Log-transform for skewed biomarkers.
  - Robust scaling for outlier resistance.
  - One-hot encoding for categorical metadata.
  - Clinical ratio feature engineering (e.g., `IL6/IL8`).
- Feature selection via **Mutual Information** (top 25%).
- Model training:
  - **Random Forest**  
  - **XGBoost** (light grid search)  
  - **PyTorch MLP** (batch norm, dropout, early stopping)  
- Evaluation metrics:
  - Accuracy, Macro-F1, Macro-AUROC
  - Brier score (calibration quality)
- Explainability:
  - **SHAP (TreeExplainer)** for tree-based models
- Persistence:
  - Saves trained models, preprocessing pipeline, encoders, and feature masks.
- Inference:
  - Functions for **single-patient prediction** (both sklearn and PyTorch models).
  - Smart dispatcher automatically selects correct backend.

---

## 📂 Repository Structure

```text
.
├── data/                           # Input datasets (real or synthetic)
│   ├── Synthetic_Dataset.csv
│   └── Hybrid_Dataset.csv
├── results/                        # Saved models, encoders, pipelines, metrics
├── Prediction Modal.ipynb          # Main end-to-end notebook
├── requirements.txt                # Core dependencies
└── README.md                       # Project documentation
```

---

## Installation

1. Navigate into this directory:

    ```bash
    cd "Prediction modal Final"
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

2. Open `Prediction Modal.ipynb` and execute all cells in order.

# Outputs
	-	Trained models:
	-	random_forest_model.pkl
	-	xgboost_model.pkl
	-	mlp_model.pth
	-	Preprocessing pipeline: preprocessor.pkl
	-	Label encoder: label_encoder.pkl
	-	Feature mask: selected_features_mask.pkl
	-	Feature definitions: feature_sets.pkl
	-	Evaluation reports: printed + confusion matrices + SHAP plots
	-	Patient-level inference examples

⸻

🧪 Example Inference

```python
sample_patient = {
    "Age": 65,
    "Gender": "Male",
    "Smoking_Status": "Current",
    "Cancer_Stage": "Stage II",
    "IL6_Saliva": 14.5,
    "IL8_Saliva": 21.2,
    "TNFa_Saliva": np.nan,
    "LDH_Saliva": 6.8,
}

prediction = smart_predict_single_patient(
    patient_data=sample_patient,
    model=trained_models["XGBoost"],
    preprocessor=preprocessor_pipeline,
    feature_mask=selected_features_mask,
    label_encoder=le,
    default_categoricals={"Gender": "Male", "Smoking_Status": "Current", "Cancer_Stage": "Stage II"},
    all_feature_names=feature_sets["all_original"],
)

print(prediction)

Output:

{
  "Predicted Diagnosis": "OSCC",
  "Confidence": "92.3%",
  "Class Probabilities": { "Healthy": 0.02, "Benign": 0.05, "OSCC": 0.923 },
  "Warning": "Low model confidence."  # only if <70%
}
```


⸻

# References

Key peer-reviewed, open-access works that underpin this pipeline:
	-	Dixit S, et al. Current review of ML and deep learning in oral cancer. Cureus. 2023.
	-	Chen T, Guestrin C. XGBoost: A Scalable Tree Boosting System. KDD. 2016.
	-	Paszke A, et al. PyTorch: An Imperative Style, High-Performance Deep Learning Library. NeurIPS. 2019.
	-	Lundberg SM, Lee S-I. A Unified Approach to Interpreting Model Predictions (SHAP). NeurIPS. 2017.
	-	Guo C, et al. On Calibration of Modern Neural Networks. ICML. 2017.
	-	Collins GS, et al. TRIPOD Statement: transparent reporting of a multivariable prediction model. BMJ. 2015.
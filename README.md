# DLQR-Health
Dynamic LLM Query Router for healthcare — thesis code, datasets, and benchmarks (oral-cancer biomarker case study).

DLQR-Health is the reproducible codebase for my MSc AI thesis on a Dynamic LLM Query Router (DLQR) for healthcare at University of Galway, Ireland. The system routes each incoming query to the most suitable module—structured biomarker prediction, case-based retrieval, or clinical QA—optimising for accuracy, p95 latency (<100 ms target), and ≤2 GB RAM. The repo includes training and calibration code, the routing policy head, ablations (embedding model and policy width), uncertainty/hedging logic, and an end-to-end evaluation harness (AUROC/F1, latency, throughput, cost proxy). A clinical oral-cancer biomarker scenario is provided as the primary case study, with clear hooks to swap in other domains. Research use only; not for clinical decision-making.

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

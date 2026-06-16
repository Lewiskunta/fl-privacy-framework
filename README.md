# Federated Learning for Privacy-Preserving Fraud Detection

**Lewis Feisal Injai**  
Masters of Engineering, Data Science & Mathematics · UCLA Capstone Project 
Cathay Bank, Los Angeles · March - November 2023

[Read the paper](https://lewiskunta.github.io/fl-privacy-framework/)

---

## What this is

A federated learning system for training fraud detection models across geographically and regulatorily distinct bank branches without transmitting raw customer records. The system was developed in collaboration with Cathay Bank's data office, which provided distributional parameters and a bank-provisioned sandbox environment.

The primary contribution is not the fraud detection AUC. The contribution is the simultaneous analytical treatment of four coupled constraints within a single system:

- **Aggregation frequency**: closed-form derivation of optimal local steps τ* from the non-IID FedAvg convergence bound, eliminating grid search
- **Differential privacy**: RDP composition under full client participation, with honest accounting that declines to invoke subsampling amplification where it does not apply
- **Communication compression**: top-k gradient sparsification achieving 50x bandwidth reduction with bounded convergence penalty
- **Byzantine robustness**: variance-triggered median fallback with detection threshold grounded in sub-Gaussian tail bounds and a formally characterised adversarial hiding radius

Each of these is typically addressed in isolation in the literature. The value of this work is their joint derivation.

---

## Results

| Configuration | AUC | ε |
|---|---|---|
| Centralised (pooled data) | 98.1% | — |
| Local-only (macro-avg) | 91.4% | — |
| FedAvg τ* + top-k + DP | **96.2%** | **≈ 4.7** |

Full results table and experimental setup in the paper.

---

## Repo structure

```
├── index.html          # The paper (GitHub Pages entry point)
├── CITATION.cff        # Machine-readable citation metadata
├── CHANGELOG.md        # Version history
├── LICENSE
├── README.md
└── model/              # Hugging Face model card and weights (forthcoming in v1.1.0)
```

---

## Data

Training data was generated from distributional parameters supplied by Cathay Bank's data office — empirical feature distributions, fraud prevalence rates, and inter-branch heterogeneity statistics drawn from production records. No customer records were accessed at any stage. The same data localisation requirements the system is designed to satisfy governed the research collaboration itself.

---

## Implementation

- Local training: PyTorch
- Federated coordination: PySyft 0.5
- Privacy accounting: RDP composition (Mironov, 2017)
- Validated on a three-node distributed setup spanning two geographic regions

---

## Status

Convergence and Byzantine detection charts are currently schematic, consistent with reported terminal values. Real training logs will replace them in a subsequent revision once training code is consolidated. The Hugging Face model and interactive Colab notebook are forthcoming.

---

## Citation

If you build on this work:

```
Injai, L. F. (2023). Mathematical Foundations of Federated Learning
for Privacy-Preserving Analytics. Masters Capstone, UCLA.
https://lewiskunta.github.io/fl-privacy-framework/
```

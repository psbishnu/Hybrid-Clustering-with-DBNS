# Hybrid Clustering with DBNS

This repository provides an implementation of a **Deep Autoencoder–based Hybrid Clustering Framework** with **Dynamic Boundary Neighborhood Score (DBNS)** optimization, **outlier-aware reweighting**, and **sensitivity/ablation studies**.  

The framework integrates:
- **Autoencoder-based representation learning**
- **KMeans clustering in latent space**
- **Dynamic Mahalanobis distance thresholding (τ = μ + λσ)**
- **Reweighting mechanism to downweight potential outliers**
- **Iterative DBNS refinement loop**
- **t-SNE visualization of clusters**
- **Sensitivity analysis over τ, θ, and λ**
- **Ablation experiments (Full vs. No DBNS vs. No Reweighting)**

---

## 📂 Project Structure

When executed, the pipeline creates a dataset-specific folder inside the main results directory:

```
Hybrid Clustering with DBNS/
│
├── anemia/                         # Dataset-specific results
│   ├── learning_curves/            # Autoencoder training loss plots
│   ├── cluster_metrics/            # ARI, F1, DBNS evolution plots
│   ├── tsne/                       # t-SNE before/after DBNS clustering
│   ├── outlier/                    # Outlier distributions (histogram/boxplot)
│   ├── sensitivity/                # τ, θ, and λ sensitivity analyses
│   ├── ablation/                   # Ablation study results
│   ├── csv/                        # Metrics logs (CSV format)
│   ├── pdf/                        # Combined reports
│   └── ...
```

---

##  Requirements

- Python 3.8+
- [TensorFlow 2.x / Keras](https://www.tensorflow.org/)
- NumPy, Pandas, Matplotlib, Scikit-learn

Install dependencies with:

```bash
pip install -r requirements.txt
```

(where `requirements.txt` should include: `tensorflow`, `numpy`, `pandas`, `matplotlib`, `scikit-learn`)

---

## Usage

1. Place your dataset CSV files in the working directory.  
   - The **last column** must be the ground-truth labels.  
   - All other columns are treated as features.

2. Update the dataset path inside the configuration:

```python
file_path = "anemia.csv"
#file_path = "pima.csv"
#file_path = "heart.csv"
...
```

3. Run the main script:

```bash
python main.py
```

---

## Outputs

At the end of execution, results will include:

- **Learning Curves**: AE training/validation loss.  
- **Clustering Metrics vs Epochs**: ARI, F1, DBNS evolution.  
- **t-SNE Visualizations**: Clusters before and after DBNS refinement.  
- **Outlier Analysis**: Histogram + boxplot of Mahalanobis scores.  
- **Sensitivity Analysis**:
  - τ sweep (`mu + λσ`, varying τ)  
  - θ sweep (weight factor for outliers)  
  - λ sweep (lambda sensitivity with mean±std reporting)  

Example λ-sweep output (console and CSV):
```
[λ-sweep] Suggested λ = 1.20 (S/DB=0.487±0.000, ARI=0.007±0.000, Outlier=9.7%±0.0%)
```

- **Ablation Study**: Comparison of
  - Full method (DBNS + reweighting)
  - No DBNS
  - No Re-weighting

Results are stored as CSV and bar plots for visual comparison.

---

## Reported Metrics

- **Silhouette Score (SS)**
- **Davies–Bouldin Index (DBI)**
- **DBNS Ratio = SS/DBI**
- **Adjusted Rand Index (ARI)**
- **F1 Score (macro)**
- **Hubness Score**
- **AUC (if binary classification ground truth is available)**

---

## Example Console Output

```
Dataset: anemia.csv
Silhouette: 0.493  DBI: 0.935  DBNS: 0.528
ARI: 0.060  F1: 0.622  Hubness: 2.463
AUC (Outlier): 0.622

[Refine 1] tau=1.425, DBNS=0.482, ARI=0.055, F1=0.600, HybridLoss=1.732
[Refine 2] tau=1.398, DBNS=0.510, ARI=0.059, F1=0.618, HybridLoss=1.690

[λ-sweep] Suggested λ = 1.20 (S/DB=0.487±0.000, ARI=0.007±0.000, Outlier=9.7%±0.0%)
```

---

## Citation

If you use this framework in your research, please cite:

```
@article{DBNS2025,
  title   = {An Adaptive Hybrid Clustering Framework with Iterative Noise Filtering and a Novel DBNS Ratio Validity Measure for Outlier-
Resilient High-Dimensional Data},
  author  = {ABHISHEK, PARTHA SARATHI BISHNU, and VANDANA BHATTACHARJEE1},
  journal = {????},
  year    = {2025}
}
```

---

## Acknowledgements



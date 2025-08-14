# 🩸 IDA Detection with Reticulocyte Indices

This repository contains the Jupyter Notebook **`iron.ipynb`**, which implements an end-to-end machine learning pipeline to detect **Iron Deficiency Anemia (IDA)** from hematological data, with a specific focus on **reticulocyte maturation indices** (e.g., IRF, MRV, Ret-He).

> ⚠️ **Data Availability:** Due to medical ethics regulations and patient privacy, the original dataset **cannot be shared** in this repository. The notebook, code, and plots are provided to enable reproduction on similar datasets.

> 💡 **Quick View:** A rendered HTML export of the notebook is available as **`iron.html`**, which includes **all outputs** (figures and results) produced during the Jupyter run. You can open it directly in a web browser.

---

## 📌 Project Overview
The workflow implemented in `iron.ipynb` mirrors the study’s Methods:

- **Study design:** Retrospective cross-sectional ML study on anonymized lab records (Nov 2024 – Jan 2025).
- **Preprocessing:**
  - Missing values, duplicates, categorical inconsistencies, and outliers handled.
  - Continuous features normalized via **min–max scaling**.
  - Categorical features encoded via **one-hot encoding**.
- **Feature selection:** Multivariate analysis with removal of highly correlated features.
- **Training/validation:**
  - **Stratified** train/test split (**70/30**).
  - **SMOTE** to address class imbalance on the training set.
  - Evaluated models: **SVM**, **Random Forest**, **Naive Bayes**, **Decision Tree**, **CatBoost**.
- **Evaluation:**
  - Metrics: **Accuracy**, **Precision**, **Sensitivity**, **Specificity**, **F1-score**, **AUC-ROC**.
  - Visualizations: per-fold CV bar charts, model comparison plots.
- **Explainability:** Feature importance and **SHAP** (summary bar, beeswarm, dependence).

---

## 🗂 Repository Structure
```
IDA_Detection_with_Reticulocyte_Indices/
├── iron.ipynb         # Main end-to-end ML notebook
├── iron.html              # HTML export of the notebook with ALL outputs
├── requirements.txt       # Python dependencies
└── README.md              # This document
```

> (Optional) You may add an `outputs/` folder locally for generated figures (e.g., CV plots, feature importance, SHAP).

---

## 🛠 Requirements & Setup

### 1) Install Python packages
Make sure you have Python 3.9+. Then install the dependencies:
```bash
pip install -r requirements.txt
```

### 2) Launch the notebook
```bash
jupyter notebook notebooks/iron.ipynb
```

### 3) View all outputs without running code
Just open **`iron.html`** in your browser to see every figure and result.

If you prefer VS Code or JupyterLab, you can open `notebooks/iron.ipynb` there as well.

---

## 🔧 Reproducibility Notes
- If your dataset contains categorical fields, ensure **the same preprocessing** (imputation, one-hot, scaling) is applied.
- Apply **SMOTE only on the training split** to avoid data leakage.
- For SHAP with tree-based models, use the **post-preprocessing feature matrix** (the same features seen by the model) and consider a small background sample for stability.

---

## 📊 Outputs (examples)
`iron.ipynb` (and **iron.html**) show:
- Per-fold bar charts: **Accuracy**, **Sensitivity**, **Specificity**, **AUC-ROC**.
- Model comparison plots across metrics.
- Feature importance (tree-based).
- **SHAP** summary (bar & beeswarm) and dependence plots.

> If you save figures, consider storing them under `outputs/` (not tracked by default).

---

## 🔐 Ethics & Privacy
- The original clinical dataset is **not included** due to **medical ethics** and **patient privacy**.
- The notebook is structured so it can be run on similarly structured, anonymized data.

---

## 🧩 Tech Stack
- **Python 3.9**, **Jupyter Notebook**
- **scikit-learn**, **pandas**, **NumPy**
- **matplotlib**, **seaborn**
- **imbalanced-learn** (SMOTE)
- **SHAP**
- **CatBoost** (for gradient boosting with categorical/heterogeneous data)

---

## ❓ FAQ

**Q: Where is the dataset?**  
A: Not distributed due to ethics/privacy. Use your own anonymized dataset with similar schema.

**Q: I get a shape mismatch error with SHAP dependence plots.**  
A: Ensure you pass the **post-transform features** (after one-hot/scaling) with matching `feature_names`, or set `interaction_index=None` to avoid automatic interaction selection.

**Q: How do I install everything quickly?**  
A: Run `pip install -r requirements.txt`.

---

## 🙌 Acknowledgements
- Hormozgan University of Medical Sciences Ethics Committee (IR.HUMS.REC.1404.025).
- Clinical and lab teams contributing anonymized records and domain expertise.

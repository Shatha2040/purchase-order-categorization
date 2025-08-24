# 📦 Purchase Order Item Categorization — End-to-End Notebook

## 📖 Project Overview
This project demonstrates an **end-to-end pipeline** for categorizing purchase order (PO) items using multilingual data (Arabic + English).

It covers:
- Data cleaning & normalization
- Language detection
- Stopword removal
- Sentence embeddings
- Unsupervised clustering (HDBSCAN + KMeans)
- Cluster labeling (top words + manual overrides)
- Spend analysis & anomaly detection
- Reproducible artifact exports


---

## ✨ Key Features
- **Data Processing**: Multilingual cleaning, normalization, language detection, stopword removal, reproducible pipeline.
- **Item Categorization**: Sentence embeddings (SentenceTransformer), HDBSCAN clustering, KMeans for outliers, cluster labeling (top words + manual overrides).
- **Analysis & Insights**: Spend proportion by category, anomaly detection (count + spend/IQR), visual explanations.
- **Documentation**: WHY-focused comments, markdown walkthrough, assumptions, trade-offs, alternatives, future improvements, tool transparency.
- **Reproducibility**: Exported artifacts (CSV summaries), version notes, environment hints.

---

## 🗂 Notebook Structure
1. Data Loading & Multilingual Text Cleaning
2. Language Detection & Stopwords
3. Embeddings (SentenceTransformer)
4. Unsupervised Categorization (HDBSCAN)
5. Handling Outliers (KMeans)
6. Cluster Labeling (Top Words + Manual Overrides)
7. EDA & Visualizations (Distributions, Outliers)
8. Spend Analysis & Insights
9. Exports & Reproducibility
10. Appendix — Methodology, Assumptions, Limitations

---


## 📊 Data

- **Input File**: `purchase-order-items.xlsx` (Excel file with purchase order items)
- **Output Artifacts**:
  - `category_spend_summary.csv` — Spend by category
  - `po_items_categorized.csv` — Categorized items with clusters and descriptive names

---

## 🔍 Challenges & How I Solved Them

1. **Understanding Relationships Between Columns**
   - Initially, I struggled to understand the relationship between columns like `Unit Price`, `Quantity`, `Total`.
   - After exploring the dataset, I realized some fields were derived and partially redundant but still useful for validation.

2. **Duplicate Columns After Cleaning**
   - After preprocessing, I found that `Total Bcy` and `Sub Total Bcy` had identical values.
   - I hesitated between removing one or keeping both. In the end, I **kept both columns** as a precaution for potential differences in future data.

3. **Handling Multilingual Text (Arabic + English)**
   - Descriptions included mixed Arabic/English terms, numbers, and unit symbols.
   - Solution: I applied **text normalization, language-aware cleaning, and stopword removal** while deliberately preserving numbers/units for semantic meaning.

---

## 🧪 Methodology Highlights

- **HDBSCAN**: Detects clusters of varying density without predefining `k`, handles noise.
- **KMeans**: Applied only to HDBSCAN outliers to ensure all items are categorized.
- **Sentence Embeddings**: Multilingual representations for robust clustering (using `all-MiniLM-L6-v2`).
- **Spend Analysis**: Auto-detects spend columns or computes from `Unit Price × Quantity`.
- **Anomaly Detection**: Used **IQR** to highlight category-level spend anomalies.

---

## ⚖️ Assumptions & Trade-offs

- Item descriptions contain enough semantic signal for categorization.
- Retained decimals, numbers, and unit symbols (critical for procurement).
- Cleaning is non-destructive and language-aware.
- Pipeline tolerates missing columns and name variations.

---

## 🚀 Improvements & Future Work

- Expand stopword lists (Arabic + English).
- Apply stemming/lemmatization (Arabic light stemming).
- Experiment with **UMAP + HDBSCAN** for better cluster separation.
- Semi-supervised labeling with LLMs for human-readable cluster names.
- Productionization: pipelines, dashboards, automated monitoring.

---

## 📌 Transparency on Tools

- I used standard **open-source Python libraries**.
- I used **ChatGPT** only to assist in generating **human-readable cluster labels** after clustering.

---

## 🖥 Environment

- Python 3.8+
- Jupyter Notebook / Google Colab


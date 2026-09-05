# 🧩 Customer Segmentation Analysis

**OASIS INFOBYTE Internship - Data Analytics Track - Level 1, Task 2**

\---

## 🎯 Objective

Apply clustering to segment an e-commerce company's customer base by purchasing behaviour
(RFM: Recency, Frequency, Monetary), enabling distinct, targeted marketing strategies per
segment backed by statistical validation, not just visual grouping.

## 🗂️ Project Structure

```
Customer-Segmentation/
│
├── notebook.ipynb          # Full analysis (executed, all outputs embedded)
├── dataset/
│   └── ecommerce\_transactions.csv   # 11,000+ raw transactions, 1,000 customers
├── outputs/
│   ├── 01\_rfm\_distributions\_raw.png
│   ├── 02\_rfm\_log\_transformed.png
│   ├── 03\_elbow\_silhouette.png
│   ├── 04\_silhouette\_plot.png
│   ├── 05\_cluster\_scatterplots.png
│   ├── 06\_pca\_clusters.png
│   └── 07\_cluster\_sizes.png
└── README.md
```

## 🧰 Tech Stack

`Python` · `pandas` · `numpy` · `scipy.stats` · `scikit-learn` (StandardScaler, KMeans, PCA,
silhouette metrics) · `matplotlib` · `seaborn` · `Jupyter Notebook`

## 📁 About the Dataset

11,000+ raw, transaction-level e-commerce orders (Jan 2023 - Dec 2024) across 1,000 customers including realistic messiness (cancelled/returned orders with negative values, missing
payment mode, duplicate rows). RFM features are **engineered from these raw transactions
inside the notebook**, not handed to it pre-aggregated.

## 🔬 Method - What Was Actually Done

1. **Cleaning**: duplicates removed, nulls handled explicitly, cancelled orders separated from valid spend.
2. **RFM engineering**: Recency, Frequency, Monetary computed per customer relative to a snapshot date.
3. **Descriptive statistics**: mean/median/variance/skewness on R, F, M (covers average purchase value, purchase frequency, and a lifetime-value view).
4. **Normality testing**: D'Agostino K² test on each RFM metric all significantly non-normal, confirming the need for a log-transform.
5. **Log-transform**: applied to Frequency \& Monetary to reduce skew before distance-based clustering.
6. **Standardization**: `StandardScaler` (Z-score) applied required since K-Means uses Euclidean distance across features with very different units.
7. **K selection**: both the **Elbow Method** and **Silhouette Score** computed across K=2–10; the trade-off between statistical tightness and business-actionable granularity is explicitly discussed (see notebook Section 7).
8. **K-Means clustering** (K=5) with `n\_init=10` for stability.
9. **Visualization**: 2D scatter plots (Recency-Monetary, Frequency-Monetary) + a PCA 2D projection explaining \~98% of variance.
10. **Statistical validation**: one-way **ANOVA** confirms Recency, Frequency, and Monetary all differ significantly across clusters (p < 0.001 each) the segments are real, not algorithmic noise.
11. **Segment naming**: assigned programmatically by ranking each cluster's composite RFM score — not eyeballed.
12. **Business insights**: a recommended marketing action mapped to every segment.

## 💡 Key Results

|Segment|Recency (days)|Frequency (orders)|Monetary (Rs.)|% of Customers|
|-|-|-|-|-|
|**Champions**|\~18|\~28|\~170,600|13.8%|
|**Loyal Customers**|\~35|\~14|\~48,500|23.7%|
|**Potential Loyalists**|\~54|\~8|\~17,800|23.5%|
|**At Risk**|\~240|\~7|\~20,200|18.3%|
|**Hibernating**|\~283|\~3|\~3,300|20.7%|

*(Exact values are computed live in the notebook table above reflects the executed run.)*

* Final model: **K=5**, silhouette score ≈ 0.46.
* ANOVA confirms all three RFM metrics differ significantly across segments (p ≈ 0 for each).

## ✅ Business Recommendations

1. **Protect \& reward Champions** (13.8% of customers, disproportionate revenue) loyalty perks, early access, referral asks; avoid unnecessary discounting.
2. **Run win-back campaigns for At-Risk customers** before they slide into Hibernating this group still carries meaningful historical value and is the most cost-effective to re-engage.
3. **Nurture Potential Loyalists** with personalised offers and habit-forming incentives (e.g., subscribe-and-save) to convert them into Loyal Customers.

## ▶️ How to Run

```bash
pip install pandas numpy scipy scikit-learn matplotlib seaborn jupyter
jupyter notebook notebook.ipynb
```

All charts and statistical outputs are already executed and embedded.

\---

**Internship:** Oasis Infobyte | **Track:** Data Analytics | **Task:** Level 1 - Task 2 (Customer Segmentation Analysis)


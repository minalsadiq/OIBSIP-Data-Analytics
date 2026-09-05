# 📊 EDA on Retail Sales Data
**OASIS INFOBYTE Internship — Data Analytics Track — Level 1, Task 1**

---

## 🎯 Objective
Perform a **statistically rigorous** Exploratory Data Analysis on a retail sales dataset —
not just descriptive charts, but distribution testing, normalization, hypothesis testing,
and multicollinearity checks — to uncover patterns and evidence-backed business
recommendations.

## 🗂️ Project Structure
```
Retail-Sales-EDA/
│
├── notebook.ipynb          # Full statistical EDA (executed, all outputs embedded)
├── dataset/
│   └── retail_sales_dataset.csv     # 9,800+ transaction records (2022–2024)
├── outputs/                # Exported chart images (also embedded in the notebook)
│   ├── 01_monthly_sales_trend.png
│   ├── 02_quarterly_sales_trend.png
│   ├── 03_customer_demographics.png
│   ├── 04_top10_products.png
│   ├── 05_category_revenue.png
│   ├── 06_correlation_heatmap.png
│   ├── 07_discount_vs_revenue.png
│   ├── 08_distributions_histkde.png
│   ├── 09_qqplots.png
│   ├── 10_log_transform_revenue.png
│   └── 11_outlier_boxplots.png
├── Retail_Sales_EDA_Summary.pptx    # Presentation-ready insight summary
└── README.md
```

## 🧰 Tech Stack
`Python` · `pandas` · `numpy` · `scipy.stats` · `statsmodels` · `scikit-learn` (scalers) ·
`matplotlib` · `seaborn` · `Jupyter Notebook`

## 📁 About the Dataset
9,800+ line-item transactions (Jan 2022 – Dec 2024): order info, customer demographics
(age, gender, region, segment), product details, and revenue — with realistic messiness
(nulls, inconsistent gender casing, duplicate rows) that the notebook explicitly cleans and
documents.

## 🔬 What Makes This a *Statistical* EDA, Not Just Descriptive Charting

| Requirement | Where it's done |
|---|---|
| **Descriptive statistics** | Mean, median, mode, **variance**, std, **skewness**, **kurtosis**, IQR for every numeric field (Section 3) |
| **Normal distribution testing** | Histograms + KDE, **Q-Q plots**, **Shapiro-Wilk test**, **D'Agostino K² test** on Age, Quantity, Price, Revenue (Section 4) |
| **Normalization** | **Z-score standardisation**, **Min-Max normalisation**, and a **log-transform** applied to correct right-skewed revenue, with before/after skew comparison (Section 5) |
| **Outlier detection** | IQR-based boxplot analysis with a documented outlier report (Section 6) |
| **Mean comparison** | **Independent-samples t-test** (Male vs Female revenue) and **one-way ANOVA** (revenue across age groups, product categories, discount tiers) (Sections 8, 9, 12) |
| **Variance testing** | **Levene's test for homogeneity of variance**, run before every t-test/ANOVA to pick the correct test variant (Sections 8, 9) |
| **Multicollinearity** | **Variance Inflation Factor (VIF)** on all numeric predictors via `statsmodels` (Section 10) |
| **Independence testing** | **Chi-square test of independence** + **Cramer's V effect size** across Gender × Category, Region × Payment Mode, Segment × Category (Section 11) |
| **Correlation** | Pearson correlation heatmap + a dedicated Pearson correlation test on discount vs. quantity (Sections 10, 12) |

Every test states its **null hypothesis**, reports the **statistic and p-value**, and is
interpreted in plain language — including cases where the result is "not significant," since
that is itself a useful, honest finding (e.g., gender does *not* significantly affect order
value in this data).

## 💡 Key Statistical & Business Findings
- **None of the core numeric variables are normally distributed** (all normality tests p < 0.05); revenue is heavily right-skewed (skew ≈ 4.5), reduced to ≈ 0.16 after a log-transform.
- **VIF ≈ 1 for all predictors** — no multicollinearity risk for future modelling.
- **Gender has no statistically significant effect on order value** (t-test p ≈ 0.70) — not a useful targeting variable.
- **Product category has a highly significant effect on order value** (ANOVA p ≈ 0) — Electronics & Furniture genuinely command higher order values, not just higher volume.
- **Discount level is weakly/not correlated with quantity purchased** (r ≈ 0.01) — deep discounts are not meaningfully driving bigger baskets.
- Sales are strongly **seasonal**: a sharp, statistically consistent Q4 spike every year and a weak Q1.

## ✅ Evidence-Based Business Recommendations
1. Build Q4 inventory (Electronics & Furniture) starting in September; use the confirmed slow Q1 for clearance, not full-price campaigns.
2. Cap standard promotional discounts near 10% — the ANOVA and correlation results show deeper discounts don't significantly grow basket size.
3. Prioritise the 26-45 segment (highest transaction volume) in retention campaigns; skip gender-based targeting, since it's not statistically justified here.

## ▶️ How to Run
```bash
pip install pandas numpy scipy statsmodels scikit-learn matplotlib seaborn jupyter
jupyter notebook notebook.ipynb
```
All charts and test outputs are already executed and embedded in the notebook.

---
**Internship:** Oasis Infobyte | **Track:** Data Analytics | **Task:** Level 1 – Task 1 (EDA on Retail Sales Data)

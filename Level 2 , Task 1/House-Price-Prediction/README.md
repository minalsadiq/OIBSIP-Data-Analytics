# 🏠 Predicting House Prices with Linear Regression

**OASIS INFOBYTE Internship - Data Analytics Track - Level 2, Task 1**

\---

## 🎯 Objective

Build and evaluate a linear regression model that predicts house prices from area, location,
room counts, and age with the full statistical pipeline (assumption checks, multicollinearity,
residual diagnostics) behind the numbers, not just a fitted line and an R².

## 🗂️ Project Structure

```
House-Price-Prediction/
│
├── notebook.ipynb          # Full analysis (executed, all outputs embedded)
├── dataset/
│   └── house\_prices.csv    # 1,200+ house listings
├── outputs/
│   ├── 01\_price\_distribution.png
│   ├── 02\_correlation\_heatmap.png
│   ├── 05\_residual\_diagnostics.png
│   ├── 06\_residuals\_vs\_fitted.png
│   ├── 07\_actual\_vs\_predicted.png
│   └── 08\_coefficients.png
└── README.md
```

## 🧰 Tech Stack

`Python` · `pandas` · `numpy` · `scipy.stats` · `statsmodels` (OLS, VIF, Breusch-Pagan) ·
`scikit-learn` (LinearRegression, Ridge, Lasso, cross-validation) · `matplotlib` · `seaborn`

## 📁 About the Dataset

1,200+ house listings with `Area\_sqft`, `Bedrooms`, `Bathrooms`, `Age\_years`,
`Distance\_to\_City\_Center\_km`, `Garage\_Spaces`, `Has\_Garden`, `Location` (categorical), and the
target `Price` — including realistic messiness (missing values, a handful of duplicate rows,
and data-entry-style area outliers) that the notebook explicitly cleans and documents.

## 🔬 Method - What Was Actually Done

1. **Cleaning**: duplicates removed, missing values median-imputed (column-by-column, with counts reported), IQR-based outlier removal on `Area\_sqft` (flagged rows were implausible data-entry errors, not real mansions).
2. **Target exploration**: distribution + Q-Q plot of `Price`, tested for normality (D'Agostino K², non-normal expected and not a problem for OLS itself).
3. **Feature selection reasoning**: explicit discussion of why each predictor is a plausible driver of price, backed by a **correlation heatmap**.
4. **Encoding**: `Location` one-hot encoded (drop-first).
5. **Multicollinearity check**: **Variance Inflation Factor (VIF)** computed on the full encoded feature set all values well under the VIF > 5 warning threshold.
6. **Train/test split**: 80/20.
7. **Statistical inference**: full **OLS regression via `statsmodels`** coefficients, p-values, confidence intervals, and an overall F-test, so significance claims are backed by numbers.
8. **Predictive evaluation**: `scikit-learn` LinearRegression **MSE, RMSE, MAE, R²** on train and test sets, plus **5-fold cross-validated R²** to confirm the model isn't overfitting.
9. **Residual diagnostics**: **Shapiro-Wilk test** (residual normality) and **Breusch-Pagan test** (homoscedasticity), plus a residuals-vs-fitted plot the assumptions behind trusting the model's p-values are checked, not assumed.
10. **Actual vs. Predicted plot** and a **coefficient impact chart** (which features push price up vs. down, and by how much).
11. **Bonus**: Ridge and Lasso regularised regression compared against plain Linear Regression via cross-validated R² and test RMSE.

## 💡 Key Results

* **Test R² ≈ 0.992**, **5-fold CV R² ≈ 0.993** (mean, std ≈ 0.0008) — consistent across train/test/CV, indicating genuine generalisation rather than overfitting.
* **All VIF values low** no multicollinearity concern despite `Bedrooms`/`Bathrooms` being correlated with each other.
* **Residuals are approximately normal** (Shapiro-Wilk p ≈ 0.65) and **homoscedastic** (Breusch-Pagan p ≈ 0.90) the OLS model's coefficient p-values and confidence intervals can be trusted at face value.
* **`Area\_sqft` is the dominant driver of price** (highest correlation and largest standardised effect), followed by room counts; `Age\_years` and `Distance\_to\_City\_Center\_km` both have a statistically significant **negative** effect.
* **Location carries a real, statistically significant premium/discount** even after controlling for size and rooms (e.g. Waterfront commands a premium; Rural a discount).
* **Ridge/Lasso do not meaningfully outperform plain Linear Regression** here consistent with the low VIF values found earlier; regularisation isn't a free win when multicollinearity was never a problem.

## ✅ Business Interpretation

1. Any pricing or appraisal tool for this market should weight **square footage** most heavily — it dominates every other feature by a wide margin.
2. **Location premiums are quantifiable and statistically significant** even after controlling for size useful for flagging listings that are mispriced relative to their neighbourhood.
3. **Age and distance from the city center both depress price** — renovation and accessibility improvements are the most direct levers for closing that gap.

## ▶️ How to Run

```bash
pip install pandas numpy scipy statsmodels scikit-learn matplotlib seaborn jupyter
jupyter notebook notebook.ipynb
```

All charts and statistical outputs are already executed and embedded in the notebook.

\---

**Internship:** Oasis Infobyte | **Track:** Data Analytics | **Task:** Level 2 - Task 1 (Predicting House Prices with Linear Regression)


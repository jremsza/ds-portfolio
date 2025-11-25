---
title: "Predicting Property Values: Advanced Regression Techniques"
date: 2023-11-25
summary: "An end-to-end machine learning project predicting housing prices in Ames, Iowa. Features extensive EDA, custom feature engineering, and hyperparameter tuning of regularized regression models (Lasso, Ridge, ElasticNet)."
weight: 2

tags:
  - Predictive Modeling
  - Feature Engineering
  - Scikit-Learn
  - Python
  - Data Visualization

categories:
  - Machine Learning
  - Real Estate Analytics

# Link to your clean GitHub repo
links:
  external_link: 
    text: "View Source Code"
    icon: "fab fa-github"
    url: "https://github.com/yourusername/ames-housing-prediction"

techstack:
    - Python (Pandas, NumPy)
    - Scikit-Learn
    - Matplotlib & Seaborn
---

## 🏠 Project Overview

Accurate real estate valuation is critical for homeowners, investors, and tax assessors. This project leverages the Ames Housing dataset to build a robust predictive model for residential property prices. By moving beyond simple square footage calculations, I engineered features that capture the "age" and "quality" of a home to drive prediction accuracy.

### 🎯 The Challenge
The dataset contains 80 explanatory variables describing (almost) every aspect of residential homes. The objective was to:
1.  **Analyze** complex relationships between features and sale price.
2.  **Engineer** new features to better represent property value.
3.  **Optimize** regression models to minimize Root Mean Squared Error (RMSE).

---

## 📊 Exploratory Data Analysis (EDA)

Understanding the target variable is the first step in any regression problem. I analyzed the distribution of `SalePrice` and identified a significant right skew (Skewness: 1.88), suggesting that high-end outlier homes could bias standard linear models.

![sale-price-hist](/images/predict-housing/saleprice.png)

Figure 1: Distribution of Sale Prices. The right skew indicates a non-normal distribution, often mitigated by log-transforming the target variable.



I also examined feature correlations to identify the strongest predictors.

![correlation_heatmap](/images/predict-housing/heat-map.png)

Figure 2: Heatmap of top 20 features correlated with SalePrice.
---

## 🛠️ Feature Engineering

Raw data is rarely model-ready. I created domain-specific features to enhance model performance:
* **HouseAge:** `2023 - YearBuilt` (Captures depreciation over time)
* **YrUpdate:** `2023 - YearRemodAdd` (Accounts for renovations)
* **GarageAge:** `2023 - GarageYrBlt`
* **Living Area Ratio:** `GrLivArea / LotArea` (A proxy for property density)

This transformation pipeline also handled missing values (imputing with 0 or mode) and encoded categorical variables using `OrdinalEncoder` for ordinal data and One-Hot Encoding for nominal data.

---

## 🤖 Modeling & Optimization

I adopted an iterative approach, starting with a baseline model and progressively adding complexity and regularization.

### 1. Baseline: Linear Regression
* **Initial Performance:** R² = ~0.79
* **Issue:** Prone to overfitting due to the high dimensionality of the dataset after encoding.

### 2. Regularization: Ridge & Lasso
* **Ridge (L2):** Penalizes large coefficients. Improved stability.
* **Lasso (L1):** Performs feature selection by shrinking less important coefficients to zero.
* **Result:** Both models improved generalization on the validation set.

### 3. The Winner: ElasticNet
I utilized `GridSearchCV` to tune hyperparameters (`alpha` and `l1_ratio`) for an ElasticNet model, which combines the strengths of both Ridge and Lasso.
* **Best Parameters:** `{'alpha': 1.0, 'l1_ratio': 0.8}`
* **Performance:** Validated R² score of **0.83**.

![learning_curve](/images/predict-housing/learning-curve.png)

Figure 3: Learning curve analysis showing the convergence of training and validation error, confirming the model is not significantly overfitting.

---

## 🚀 Key Results & Interpretation

The ElasticNet model proved to be the most robust predictor.

![reg-plot](/images/predict-housing/act-v-predict.png)

Figure 4: Predicted vs. Actual Sale Prices on the validation set.

**Interpreting the Results:**
The scatter plot above illustrates the model's accuracy on unseen validation data. The red dashed line represents a perfect prediction (where Predicted Price = Actual Price). 

* **Tight Clustering:** The strong alignment of points along the diagonal confirms the model's high predictive power for the majority of housing stock (under $350k).
* **Variance at the High End:** As property values increase (>$400k), the model shows slightly higher variance. This is a common phenomenon in real estate modeling, often caused by the scarcity of luxury home data points or unique features not captured in standard columns.

---

## 💡 Key Takeaways
* **Feature Engineering Wins:** Creating "Age" features significantly improved model interpretability and performance compared to using raw "Year" columns.
* **Regularization is Crucial:** In datasets with many features (80+), unregularized linear regression tends to overfit. ElasticNet provided the best balance.
* **Data Quality:** Handling missing values (e.g., converting `NaN` in "Alley" to "No Alley") was essential for utilizing the full dataset.
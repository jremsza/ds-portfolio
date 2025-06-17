---
title: "Ames Housing Prices: Regression Modeling"
summary: "A machine learning project that predicts house prices in Ames, Iowa using Lasso, Ridge, and ElasticNet regression with cross-validation and hyperparameter tuning."
tags: ["Regression", "ElasticNet", "EDA", "Feature Engineering", "Supervised Learning"]
categories: ["Machine Learning", "Portfolio Projects"]
project types: ["Academic", "Personal"]
techstack: "Python"
---

## 🏡 Ames Housing Prices: Regression Modeling

**Category:** Supervised Learning, Regression  
**Tools:** Python, scikit-learn, pandas, seaborn  
**Skills:** EDA, regression modeling, cross-validation, feature selection, regularization

---

### 🔍 Problem Statement

The goal of this project was to predict housing prices in Ames, Iowa using a variety of regression models. The dataset contains 80 features describing different aspects of residential homes, offering a rich playground for EDA, feature engineering, and modeling.

---

### 📊 Dataset

- **Source:** Kaggle’s Ames Housing Dataset  
- **Target Variable:** `SalePrice`  
- **Features:** 80 total, including categorical and numeric types  
- **Preprocessing:**
  - Missing value imputation  
  - Categorical encoding  
  - Outlier treatment  
  - Feature scaling where needed

---

### 📈 Modeling Approach

Three types of regularized regression models were trained and compared:

- **Lasso Regression**  
- **Ridge Regression**  
- **ElasticNet Regression**

The project involved:

- Exploratory data analysis and correlation heatmaps  
- Feature selection based on domain understanding and correlation  
- Log-transformation of skewed variables  
- Cross-validation to compare model performance  
- Hyperparameter tuning (especially for ElasticNet)

---

### 🔧 Key Techniques

- Applied histogram and boxplots to inspect the target distribution  
- Identified top correlated predictors with `SalePrice`  
- Evaluated model performance with RMSE and R²  
- Used `GridSearchCV` for tuning alpha/l1 ratios in ElasticNet

---

### 📈 Results

- ElasticNet performed best after tuning, striking a balance between Lasso and Ridge  
- Achieved low RMSE and high R² values on validation data  
- Plots of predicted vs. actual prices showed strong model fit  
- Top predictors included `OverallQual`, `GrLivArea`, and `GarageCars`

---

### 📌 Reflection

This project illustrates the end-to-end process of building regression models on structured data. It highlights how EDA, thoughtful preprocessing, and regularization techniques can lead to strong predictive performance.

**Future ideas:**
- Try ensemble models like Gradient Boosted Trees or XGBoost  
- Automate preprocessing with pipelines  
- Deploy model using Flask or FastAPI

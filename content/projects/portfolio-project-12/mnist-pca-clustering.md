---
title: "MNIST Digit Recognition with PCA and Clustering"
summary: "A machine learning project that classifies handwritten digits using a Random Forest classifier and explores dimensionality reduction with PCA and K-Means clustering."
tags: ["MNIST", "PCA", "Clustering", "Random Forest", "Unsupervised Learning"]
categories: ["Machine Learning", "Portfolio Projects"]
techstack: "Python"
project types: ["Academic", "Personal"]
---

## 🔢 MNIST Digit Recognition with PCA and Clustering

**Category:** Image Classification, Dimensionality Reduction  
**Tools:** scikit-learn, pandas, matplotlib, seaborn  
**Skills:** Random Forests, PCA, clustering, visualization, model evaluation

---

### 🔍 Problem Statement

This project aimed to classify handwritten digits using the MNIST dataset. Beyond model accuracy, the goal was to investigate how dimensionality reduction (via PCA) and unsupervised learning (via K-Means) could help better understand the structure of the data.

---

### 📊 Dataset

- **Source:** [MNIST Digit Recognizer on Kaggle](https://www.kaggle.com/competitions/digit-recognizer)  
- **Samples:** 70,000 grayscale images (28x28 pixels)  
- **Classes:** 10 digits (0–9)  
- **Data Format:** Flattened pixel values in tabular format

---

### 🧠 Modeling and Techniques

1. **Random Forest Classifier**
   - Trained on full dataset (pixel values)  
   - Evaluated using accuracy on hold-out test set  
   - Predictions submitted to Kaggle for benchmark comparison

2. **Principal Component Analysis (PCA)**
   - Used to reduce dimensionality of 784-pixel input vectors  
   - Visualized variance retained to choose ideal number of components

3. **K-Means Clustering**
   - Applied on PCA-reduced data  
   - Cluster assignments compared to true digit labels  
   - Cluster quality visualized using confusion matrices and cluster centers

---

### 📈 Results

- Random Forest model achieved high accuracy (>95%) on test set  
- PCA reduced dimensionality significantly (from 784 to ~50 components) while preserving performance  
- K-Means clustering revealed natural groupings in digit space  
- t-SNE and PCA visualizations gave insight into digit similarity and cluster overlap

---

### 🔧 Key Techniques

- Feature scaling and variance thresholding  
- Evaluated model runtime and memory trade-offs with and without PCA  
- Cluster purity analysis by matching K-Means labels to digit classes  
- Visual diagnostics of misclassifications and overlapping digits

---

### 📌 Reflection

This project highlighted how dimensionality reduction can improve both model efficiency and data interpretability. It was also a chance to blend supervised and unsupervised methods for deeper insight into image data.

**Next steps:**
- Apply deep learning (e.g., CNNs) to compare performance  
- Try DBSCAN or Gaussian Mixture Models for clustering  
- Use autoencoders for learned dimensionality reduction

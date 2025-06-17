---
title: "Amazon Product Review Clustering with NLP"
summary: "An NLP project exploring text vectorization, topic modeling, and clustering on Amazon product reviews using TF-IDF, Word2Vec, LDA, and t-SNE visualizations."

tags:
  - Clustering
  - NLP
  - Text Mining
  - LDA
  - t-SNE

categories:
  - Natural Language Processing

project types: 
  - Academic
  - Personal
techstack:
    - Python
---

## 📝 Amazon Product Reviews: NLP Exploration and Sentiment Clustering

**Category:** Natural Language Processing, Unsupervised Learning  
**Tools:** Python, NLTK, scikit-learn, Gensim, t-SNE, Word2Vec, TF-IDF  
**Skills:** Text cleaning, feature extraction, topic modeling, clustering, dimensionality reduction, data visualization

---

### 🔍 Problem Statement

This project explored the application of natural language processing techniques to analyze product reviews from a subset of the Amazon dataset. The focus was on understanding how different text representations affect clustering performance and whether sentiment and topic patterns could be identified in an unsupervised manner.

---

### 📊 Dataset

- **Source:** Amazon Product Reviews (FastText-format subset)
- **Preprocessing:**
  - Text normalization (punctuation removal, lowercasing)
  - Stop word removal using NLTK
  - Comparison of stemming vs. lemmatization

---

### 🧠 NLP Techniques Explored

- **Text Representations:**
  - TF-IDF
  - Word2Vec
  - Bag-of-Words
- **Topic Modeling:**  
  - Latent Dirichlet Allocation (LDA) using Gensim
- **Dimensionality Reduction:**
  - Principal Component Analysis (PCA)
  - t-Distributed Stochastic Neighbor Embedding (t-SNE)

---

### 📈 Clustering & Evaluation

- **Clustering Methods:**
  - K-Means clustering with silhouette score evaluation
- **Label Interpretation:**
  - Visual inspection of clusters via t-SNE
  - Use of word clouds and top keywords per cluster
- **Exploratory Classification:**
  - Preliminary use of decision trees on topic-labeled data

---

### 🔧 Key Techniques

- Conducted 10 experiments across different preprocessing and vectorization strategies  
- Visualized clusters using t-SNE and PCA to validate structure  
- Integrated both unsupervised and supervised techniques to understand data structure

---

### 📌 Reflection

This project helped solidify my understanding of how choices in text preprocessing and feature engineering impact clustering performance and interpretability. Future directions include:

- Experimenting with transformer-based embeddings (e.g., BERT)  
- Applying sentiment scoring to cluster summaries  
- Building a dashboard to explore review clusters interactively

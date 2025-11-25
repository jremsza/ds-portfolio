---
title: "Unlocking Customer Sentiment: NLP & Topic Modeling on Amazon Reviews"
seo_title: "Amazon NLP Clustering Project"
summary: "Benchmarking 10 NLP techniques (TF-IDF vs. Word2Vec vs. LDA) to automatically categorize 36,000+ unstructured customer reviews into distinct product segments."
description: "A deep dive into unsupervised learning to structure the unstructured."
slug: amazon-nlp-clustering
author: "Jacob Remsza"

draft: false
date: 2025-01-15T12:00:00-05:00
lastmod: 2025-01-15T12:00:00-05:00
expiryDate: 
publishDate: 2025-01-15T12:00:00-05:00

#feature_image: "/images/amazon_review_wordcloud.png"
#feature_image_alt: "Word cloud showing frequent terms in Amazon reviews"

tags:
  - NLP
  - Unsupervised Learning
  - LDA
  - Python
  - Scikit-Learn

categories:
  - Data Science
  - Machine Learning
  - Natural Language Processing

project types: 
  - Academic
  - Personal

techstack:
  - Python
  - Gensim (LDA, Word2Vec)
  - Scikit-Learn
  - NLTK
  - Pandas
  - Matplotlib

source_url: https://github.com/jremsza/NLP_project.git
---

## 🛍️ The Business Problem
In the e-commerce sector, the volume of customer feedback is overwhelming. Manual categorization of millions of reviews is impossible, yet businesses need to understand **what** customers are talking about to route support tickets or analyze product sentiment.

**The Goal:** Develop an unsupervised machine learning pipeline capable of ingesting raw, unstructured text and automatically grouping reviews into coherent product categories without human intervention.

![Word Cloud of Amazon Reviews](/images/proj-7/word-cloud.png)
*Figure 1: Initial visualization of the raw text data. Dominated by general terms like "book", "movie", and "music", suggesting underlying categories waiting to be discovered.*

---

## 🛍️ Project Overview
**Goal:** Automate the categorization of vast amounts of unstructured customer feedback to assist in routing support tickets or analyzing product sentiment.

### 🔍 The Challenge
Raw text data is messy and high-dimensional. This project explores optimal ways to represent text numerically to discover latent topics within Amazon reviews without using pre-existing labels.

### 🛠️ Methodology
I conducted **10 iterative experiments** to determine the best feature extraction pipeline.
- **Preprocessing:** Regex cleaning, Lemmatization (NLTK), Stop-word removal.
- **Vectorization:** Tested Sparse (TF-IDF) vs. Dense (Word2Vec) embeddings.
- **Modeling:** Compared K-Means Clustering against Latent Dirichlet Allocation (LDA).

### 📊 Key Findings
The traditional TF-IDF approach struggled to separate concepts. **LDA Topic Modeling** proved superior, successfully disentangling semantic meaning where K-Means failed.

![Image](/images/proj-7/bar-chart.png)

Figure 2: Bar Chart comparing Silhouette Scores of Experiments

### 🏷️ Cluster Analysis
Using the optimal LDA model (10 topics), I projected the high-dimensional data into 2D space using t-SNE. The model successfully clustered reviews into coherent groups:

![Image: Colored t-SNE Scatterplot showing distinct clusters](/images/proj-7/t-sne-8.png)

Figure 3: A t-SNE plot generated from Experiment 8

- **Cluster 0:** Physical Media (Books)
- **Cluster 1:** Visual Media (Movies/DVDs)
- **Cluster 2:** Audio (Music/CDs)

### 💻 Tech Stack
- **Core:** Python, Pandas, Scikit-Learn
- **NLP:** Gensim (Word2Vec, LDA), NLTK
- **Viz:** Matplotlib, Seaborn, t-SNE

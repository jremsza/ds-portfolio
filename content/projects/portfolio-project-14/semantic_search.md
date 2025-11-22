---
title: Beyond Keywords - Building an End-to-End Semantic Search Engine
seo_title: Semantic Search Project
summary: A comparative analysis and engineering proof-of-concept replacing legacy TF-IDF search with SBERT embeddings and ChromaDB, achieving a 2.5x improvement in retrieval precision.
description: Portfolio Project 2 explores NLP and Vector Databases.
slug: semantic-search-engine
author: Jake Remsza

draft: false
date: 2025-11-21T12:00:00-05:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

tags:
  - NLP
  - Machine Learning
  - Docker
  - Vector DB

categories:
  - Data Science
  - Engineering
  - NLP

project types: 
  - Personal
  - Academic
techstack:
    - Python
    - ChromaDB
    - Streamlit
    - Docker
source_url: https://github.com/jremsza/semantic_search_engine
---

---

## 🔍 Project Summary

This project engineered a modern, end-to-end semantic document retrieval system to address the limitations of traditional keyword search. The project was executed in two phases:

- Part 1: System Engineering (Containerized Pipeline with SBERT & ChromaDB)
- Part 2: Comparative Evaluation (Quantitative & Qualitative Analysis vs. TF-IDF)

---

## 🧠 Background

Traditional search relies on **lexical matching** (TF-IDF). It looks for exact keywords. If the user doesn't guess the exact word the author used (e.g., searching "fix" when the doc says "repair"), the system fails.

The goal of this project was to build a "semantic" search engine that understands **user intent** and **conceptual meaning**, and to rigorously prove its superiority over a traditional baseline. The system utilizes **Transfer Learning** via the `all-MiniLM-L6-v2` model to generate dense vector embeddings, allowing for retrieval based on meaning rather than just matching text strings.

---

## 🏗️ Part 1: System Architecture

### Dual-Model Design

The system was designed as a **dual-model architecture**. This allowed for a single user query to trigger parallel retrieval processes, returning ranked results from both the Baseline (TF-IDF) and the Semantic (SBERT) models simultaneously for side-by-side comparison.

![Project Architecture Flow Diagram](/images/proj-15/architecture.png)

**Insight:** The architecture is fully containerized using Docker. This ensures reproducibility and simulates a production-grade deployment where the Vector Database (ChromaDB) runs as an isolated service, accessible via API by the Streamlit frontend.

---

## 📊 Part 2: Comparative Evaluation

### Methodology: The Golden Dataset

To scientifically benchmark the performance, I created a **Golden Dataset** consisting of 30 queries ranging from simple definitions ("what is a p-value?") to complex conceptual comparisons ("difference between random forest and gradient boosting").

The models were evaluated on two key metrics:
* **Precision@3:** On average, how many of the top 3 results were relevant? (Measures Reliability)
* **Mean Reciprocal Rank (MRR):** On average, how high up the list is the *first* correct answer? (Measures Ranking Quality)

### Quantitative Results

![Quantitative Results Bar Chart](/images/proj-15/quant_results.png)

**Insight 1: 2.5x Precision Improvement**
The baseline TF-IDF model struggled significantly, with a Precision@3 of **0.178**. This means that over 80% of the time, the keyword search failed to provide a relevant result on the "first page." The semantic model achieved a Precision@3 of **0.456**, making it **2.5 times more precise** and a far more reliable tool.

**Insight 2: Ranking Quality (MRR)**
The MRR scores reveal a stark difference in user experience. The baseline's score (0.339) translates to an average rank of ~3, meaning users have to dig for answers. The semantic model's score (0.643) translates to an average rank of ~1.55, placing the best answer at the very top.

### Qualitative Analysis

The numbers tell *what* happened, but the visual analysis explains *why*.

#### Example 1: Understanding Intent vs. Keywords

**Query:** "describe the ETL process"

![ETL Process Comparison](/images/proj-15/etl_screenshot.png)

**Insight:** The Baseline (Right) latched onto the word "process" and returned an irrelevant document about parallel processing. The Semantic Model (Left) understood that "describe" signals a request for a **definition** and returned the correct textbook explanation of Extract, Transform, Load.

#### Example 2: Handling Specific Acronyms

**Query:** "what is LSTM"

![LSTM Query Comparison](/images/proj-15/lstm_screenshot.png)

**Insight:** The Baseline got confused by the general topic of neural networks and returned a document about "Jordan networks." The Semantic model locked onto the specific entity (LSTM) and returned the correct historical context.

---

## 📌 Conclusions

- **Superior Performance:** The semantic model demonstrated clear superiority, improving retrieval precision by **250%** and ranking quality by **190%**. It successfully shifted the retrieval paradigm from keyword matching to intent understanding.

- **Engineering Viability:** This project serves as an engineering proof-of-concept. By leveraging **Docker**, **ChromaDB**, and **Streamlit**, I demonstrated that a robust, deployable semantic search engine can be built using open-source tools, moving beyond simple local scripts to a stable application architecture.

- **Strategic Advantage:** The analysis proves that for internal knowledge bases, semantic search provides the "high ground." It eliminates the friction of exact-match requirements, allowing users to query naturally and find accurate information faster.

---

## 🧰 Tools Used

- **Python** (Pandas, NumPy)
- **NLP & AI:** `sentence-transformers` (SBERT), Hugging Face, Scikit-learn (TF-IDF)
- **Database:** **ChromaDB** (Vector Store)
- **DevOps:** **Docker** & Docker Compose for containerization
- **Frontend:** **Streamlit** for the interactive UI and side-by-side comparison
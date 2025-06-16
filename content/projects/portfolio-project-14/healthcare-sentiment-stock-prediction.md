
---
title: "Predicting Healthcare Sector Stock Performance with News Sentiment"
course: Knowledge Engineering
summary: "A full-stack data science project that integrates NLP, knowledge graphs, and machine learning to analyze how healthcare-related news sentiment impacts stock market movements."
tags: ["NLP", "Sentiment Analysis", "XGBoost", "Healthcare", "Knowledge Graph", "Stock Prediction"]
categories: ["End-to-End Projects", "Portfolio Projects"]
---

## 🧬 Predicting Healthcare Stock Performance with News Sentiment

**Category:** NLP, Financial Prediction, Knowledge Graphs  
**Tools:** Python, BERT, spaCy, Scrapy, yfinance, Gel (Graph DB)  
**Skills:** NLP, data engineering, API integration, web crawling, graph databases, ML modeling

---

### 🔍 Overview

This project analyzes the relationship between healthcare market sector sentiment and stock performance by integrating data engineering, NLP, and machine learning techniques. It demonstrates an end-to-end approach—from data ingestion and graph construction to sentiment modeling and return prediction.

---

### 🎯 Project Goals

- Analyze sentiment in healthcare-related news articles from CNBC, NewsAPI, and Investopedia  
- Build a **knowledge graph** linking companies, events, and market behavior  
- Predict stock price movements using **XGBoost** and sentiment-driven features  
- Store and analyze these relationships using a graph database schema

---

### 🧱 Methods

#### 📰 Data Collection
- Web crawlers (Scrapy) + API integrations to collect healthcare news  
- Used `yfinance` to fetch historical stock prices for top healthcare firms  
- Linked articles with companies through keyword/entity matching

#### 🔎 Sentiment Analysis
- Fine-tuned BERT-based sentiment classifier  
- Produced binary sentiment scores (0/1) for each article  

#### 🧠 Knowledge Graph Construction
- Built graph schema using **Gel**  
- Modeled relationships: `.about`, `.mentions`, `.sentiment_score`, `.date`  
- Applied spaCy NER to extract entities (companies, drugs, CEOs) and link them to articles  

#### ⚙️ Data Processing Pipeline
- Python automation scripts to clean, merge, and sync all data sources  
- Combined news and stock data to create model-ready features:  
  - Moving averages, lagged returns, rolling sentiment ratios

#### 🤖 ML Modeling
- Trained an **XGBoost regressor** to predict next-day returns  
- Features included:  
  - Past returns (lagged)  
  - 3-day moving sentiment ratios  
  - 5-day stock return averages

---

### 📈 Results

- Built a real-time knowledge graph of healthcare news events and company links  
- Generated sentiment scores across multiple media sources  
- Developed a predictive model with high correlation between predicted and actual returns  
- Demonstrated how media tone can enhance financial forecasting for healthcare markets

---

### 📌 Reflection

This project combined a wide range of advanced data science skills including BERT-based NLP, web scraping, graph database design, and predictive modeling. It also emphasized the importance of building **structured knowledge** from unstructured web sources.

---

### 🧰 Key Technologies

- **Python** – Core scripting and analysis  
- **BERT** – Sentiment modeling  
- **spaCy** – NER for entity linking  
- **Scrapy + APIs** – Data ingestion  
- **Gel** – Graph database schema and querying  
- **XGBoost** – Predictive modeling  
- **yfinance** – Stock data

---

### 🔗 GitHub Repository 


```markdown
[View the full code and pipeline on GitHub](https://github.com/your-username/healthcare-sentiment-graph)
```

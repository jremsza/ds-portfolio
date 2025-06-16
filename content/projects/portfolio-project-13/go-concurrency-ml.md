
---
title: "Benchmarking Linear Regression with Concurrency in Go"
course: Data Engineering with Go
summary: "A systems-level machine learning project comparing serial and concurrent linear regression implementations in Go using the Boston Housing dataset."
tags: ["Go", "Concurrency", "Benchmarking", "Linear Regression", "Performance"]
categories: ["Systems Projects", "Portfolio Projects"]
---

## ⚙️ Benchmarking Linear Regression with Concurrency in Go

**Category:** Systems Programming, Performance Engineering  
**Tools:** Go, Gonum, CSV, sync.WaitGroup, benchmarking utilities  
**Skills:** Concurrency, matrix algebra, linear regression, benchmarking, CLI programming

---

### 🔍 Problem Statement

This project explores how concurrency can accelerate machine learning workflows by comparing a traditional serial linear regression implementation against a concurrent version written in Go. The comparison focuses on model performance and execution time using the Boston Housing dataset.

---

### 🧱 Technical Overview

- **Language:** Go  
- **ML Technique:** Least Squares Linear Regression  
- **Libraries:** Gonum for matrix operations  
- **Concurrency Tools:** `goroutines`, `channels`, and `sync.WaitGroup`

Two programs were built:

- `noConcur`: A baseline implementation of linear regression without concurrency  
- `withConcur`: An enhanced version with concurrent prediction execution using goroutines

---

### 📊 Dataset

- **Source:** Boston Housing Dataset (CSV format)  
- **Features:** Subset of numeric predictors  
- **Preprocessing:**
  - CSV parsing into slices and `mat.Dense` matrices  
  - Train/test split using randomized index permutation

---

### 🧠 Model Building

- Implemented linear regression manually using:
  - \( \theta = (X^T X)^{-1} X^T y \)  
- Model predictions computed using matrix multiplication  
- Evaluation metrics included:
  - Mean Squared Error (MSE)  
  - Akaike Information Criterion (AIC)

---

### 🚀 Concurrency in Practice

The `withConcur` program uses Go's native concurrency features to execute predictions in a separate goroutine:

- Matrix multiplication (`X * θ`) happens inside a goroutine  
- A `sync.WaitGroup` ensures safe synchronization  
- Results returned over a channel to the main thread

---

### 📈 Results

- Benchmarked over 100 trials  
- The concurrent version consistently outperformed the serial version in execution time  
- Benchmark output saved and compared in separate logs for transparency

---

### 📌 Reflection

This project demonstrated Go's viability as a performant language for lightweight ML tasks. Concurrency added measurable speed benefits, particularly during prediction phases.

**Takeaway for Engineering Teams:** While concurrency improves runtime, it comes at the cost of additional code complexity. Future work could include:
- Further parallelizing matrix operations  
- Comparing Go’s performance to Python’s NumPy-based solutions  
- Building reusable Go packages for regression modeling

---

### 🔗 GitHub Repository

[👉 View Source Code and Benchmarks on GitHub](https://github.com/jremsza/goMLproject.git)

---

### 📷 Visuals & Benchmark Plots 


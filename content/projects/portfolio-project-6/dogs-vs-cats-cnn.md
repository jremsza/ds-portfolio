---
title: "Iterative CNN Design: Engineering High-Performance Vision Models on Prototype Hardware"
seo_title: "Building Custom CNNs on NVIDIA RTX 5070 Ti"
summary: "A methodological approach to Computer Vision. I benchmarked three custom CNN architectures on the unreleased RTX 5070 Ti, optimizing data pipelines to achieve 92% accuracy without transfer learning."
description: "From 62% to 92%: An engineering journey through CNN architecture and hardware optimization."
slug: iterative-cnn-design-rtx50
author: Jake Remsza
date: 2025-11-24
draft: false

#feature_image: /images/dogs-vs-cats/model_comparison_chart.png
#feature_image_alt: "Bar chart showing accuracy progression from Model 1 to Model 3"

tags:
  - Computer Vision
  - TensorFlow Nightly
  - Model Architecture
  - GPU Optimization
  - WSL2

categories:
  - Machine Learning Engineering
  - Data Science
  - Infrastructure

project_types:
  - Experimental
  - Engineering

techstack:
  - Python 3.10
  - TensorFlow Nightly (v2.16+)
  - NVIDIA CUDA 12.x (WSL2)
  - Scikit-Learn
  - Matplotlib
source_url: https://github.com/jremsza/YOUR_REPO_NAME
---

---

## 🎯 Project Objective

The goal of this project was to engineer a robust binary image classifier (Dogs vs. Cats) from scratch, strictly avoiding pre-trained weights (Transfer Learning) to demonstrate mastery of CNN fundamentals.

This project also served as an infrastructure stress test. Running on the newly released **NVIDIA RTX 5070 Ti**, I faced significant driver and JIT compilation challenges, requiring a custom **WSL2 + TensorFlow Nightly** environment to bypass "Compute Capability 12.0" incompatibilities.

---

## 🏗️ The Engineering Approach (Iterative Design)

Rather than guessing hyperparameters, I adopted a scientific approach, designing and benchmarking three distinct architectures to isolate performance drivers.

### 🧪 Experiment 1: The Baseline
* **Architecture:** Shallow network (2 Conv Blocks), `Softmax` output.
* **Hypothesis:** A simple model can capture basic shapes.
* **Result:** **Underfitting (62% Accuracy)**. The model lacked the capacity to distinguish subtle features like snout length or ear texture.

### 🧪 Experiment 2: The "Deep" Model
* **Architecture:** Deep network (4 Conv Blocks, up to 256 filters), heavy Dropout.
* **Hypothesis:** More parameters = better feature extraction.
* **Result:** **Overfitting (76% Accuracy)**. The model memorized training noise. Validation loss spiked while training accuracy hit 99%, a classic variance error.

### 🏆 Experiment 3: The Optimized "Binary Brain"
* **Architecture:** Balanced depth (3 Conv Blocks), Aggressive Augmentation, **Binary Logic**.
* **Key Innovation:** Switched from `Categorical Crossentropy` (Softmax) to `Binary Crossentropy` (Sigmoid). This fundamental change in loss function stabilized gradients and solved mode collapse.
* **Result:** **92% Accuracy**. The champion model.

---

## ⚙️ Final System Architecture (Model 3)

The winning architecture was a custom Sequential CNN optimized for the RTX 5070 Ti's memory bandwidth.

**1. The Data Pipeline (`tf.data`)**
To prevent CPU bottlenecks, I built an asynchronous pipeline:
* **Dynamic Normalization:** `x / 255.0` applied in parallel threads.
* **Augmentation:** Random Rotations (10%), Flips, and Zooms to force invariant feature learning.
* **Prefetching:** `AUTOTUNE` enabled to keep the GPU utilization >90%.

**2. The Model Specs**
| Layer Type | Parameters | Purpose |
| :--- | :--- | :--- |
| **Input** | 180x180x3 | RGB Image Tensor |
| **Conv2D Block 1** | 32 filters, 3x3 | Edge/Color detection |
| **Conv2D Block 2** | 64 filters, 3x3 | Texture/Pattern detection |
| **Conv2D Block 3** | 128 filters, 3x3 | High-level shape (Ears/Nose) |
| **Dropout** | 0.5 Rate | Prevent neuron co-adaptation |
| **Dense Output** | **1 Unit (Sigmoid)** | Binary Probability Score |

---

## 📊 Performance Analysis

### 1. Architecture Comparison
The iterative process yielded a clear "Step Function" in performance. Moving to binary logic in Model 3 provided the massive jump to >90%.

![Model Comparison Chart](/images/proj-6/model_comparison_chart.png)
*Figure 1: Validation Accuracy comparison. Model 3 outperforms the baseline by 30 percentage points.*

### 2. ROC Curve Analysis
To prove the model wasn't just guessing the majority class, I plotted the Receiver Operating Characteristic (ROC). The curves show the distinct improvement in class separability.

![ROC Curve Comparison](/images/proj-6/roc_curve_compare.png)
*Figure 2: ROC Curves for all three experiments. Model 3 (Orange) hugs the top-left corner with an **AUC of 0.96**, indicating near-perfect separation capability.*

### 3. Confusion Matrix (Balanced)
Tested on a strictly isolated, balanced validation set (2,500 Cats / 2,500 Dogs).

![Confusion Matrix](/images/proj-6/confusion_matrix.png)
*Figure 3: Final Confusion Matrix for Model 3. The model predicts both classes with high precision (~92%), showing negligible bias toward either animal.*

---

## 📌 Key Takeaways

1.  **Logic Matters More Than Depth:** Switching from Categorical (2 output units) to Binary (1 output unit) had a bigger impact than adding more convolutional layers.
2.  **Infrastructure is a Feature:** Optimizing the `tf.data` pipeline for the RTX 5070 Ti reduced epoch time by 40%, allowing for faster iteration cycles.
3.  **Data Integrity:** Identifying and fixing the "Alphabet Trap" (where validation data sorted by filename biased evaluation) was critical to getting honest metrics.

---

## 🧰 Tools Used
* **Hardware:** NVIDIA RTX 5070 Ti (Prototype Drivers)
* **Environment:** WSL2 Ubuntu / TensorFlow Nightly
* **Libraries:** Keras, Pandas, Scikit-Learn
---
title: "Paw-sitive Predictions: Binary Image Classification with CNNs"
seo_title: Dogs vs Cats CNN Project
summary: "A custom Convolutional Neural Network (CNN) built with TensorFlow/Keras to classify images of dogs and cats with 76% accuracy, featuring data augmentation and real-time training visualization."
description: "Portfolio Project 3 exploring Computer Vision."
slug: dogs-vs-cats-cnn
author: Jake Remsza

draft: false
date: 2025-11-22T12:00:00-05:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

tags:
  - Computer Vision
  - TensorFlow
  - Deep Learning
  - Python

categories:
  - Data Science
  - Engineering
  - Computer Vision

project types: 
  - Personal
  - Academic
techstack:
    - TensorFlow
    - Keras
    - Python
    - Matplotlib
source_url: https://github.com/jremsza/YOUR_REPO_NAME
---

---

## 🔍 Project Summary

This project tackles a classic Computer Vision problem: binary classification of images. Using the "Dogs vs. Cats" dataset, I engineered a custom Convolutional Neural Network (CNN) capable of distinguishing between the two species. The project focuses on:

- **Pipeline Engineering:** Building robust `ImageDataGenerators` for real-time data augmentation.
- **Model Architecture:** Designing a custom 3-layer CNN from scratch.
- **Evaluation:** Analyzing training curves and confusion matrices to diagnose model performance.

---

## 🏗️ Part 1: System Architecture

### The Pipeline
To prevent overfitting on the training data, I implemented a robust preprocessing pipeline using Keras `ImageDataGenerator`. Instead of feeding static images, the generator applies random transformations during training, effectively creating a diverse, infinite dataset.

**Augmentation Techniques Used:**
* **Rescaling:** Normalizing pixel values (1./255) for faster convergence.
* **Shear & Zoom:** Random geometric distortions to force the model to learn invariant features.
* **Horizontal Flips:** Mirroring images to ensure orientation doesn't bias predictions.

### The Custom CNN Model
I eschewed pre-trained models (like ResNet) to build a custom architecture from the ground up, allowing for deeper understanding of feature extraction.

* **Input Layer:** 64x64x3 (RGB Images)
* **Feature Extraction:** 3 distinct blocks of `Conv2D` (32 filters) + `MaxPooling2D` (2x2).
* **Classification Head:** A `Flatten` layer feeding into a fully connected `Dense` layer (64 units) and a final `Sigmoid` output unit for binary probability.

---

## 📊 Part 2: Performance & Evaluation

### Training Dynamics
The model was trained for **25 epochs** with a batch size of 32.

![Training History Accuracy and Loss](/images/dogs-vs-cats/training_curves.png)
*Figure 1: The training curves (Blue) vs. Validation curves (Orange). The convergence of accuracy and the stabilization of loss indicate the model learned effectively without significant overfitting.*

### Quantitative Results
The model achieved a final evaluation accuracy of **76.4%** on the unseen test set.

| Metric | Score | Notes |
| :--- | :--- | :--- |
| **Test Accuracy** | **76.41%** | Strong baseline for a custom-built model. |
| **Test Loss** | **0.678** | Indicates good probabilistic confidence. |

### Visualizing Predictions
To verify the model qualitatively, I visualized a batch of predictions.

![Sample Predictions Grid](/images/dogs-vs-cats/predictions.png)
*Figure 2: A grid of test images with their predicted labels. The model successfully distinguishes distinct features like ear shape and snout length.*

### Confusion Matrix Analysis
![Confusion Matrix](/images/dogs-vs-cats/confusion_matrix.png)
*Figure 3: The Confusion Matrix reveals the model's specific biases. It shows a balanced performance between classes, with similar rates of False Positives (predicting Dog when it's a Cat) and False Negatives.*

---

## 📌 Conclusions & Future Work

- **Engineering Success:** Successfully built an end-to-end vision pipeline that handles raw image data, augments it in real-time, and trains a stable neural network.
- **Architectural Insights:** The 3-layer convolutional design proved sufficient for capturing high-level features (edges, textures) required for species differentiation.
- **Future Roadmap:**
    - **Transfer Learning:** Implementing VGG16 or MobileNet to boost accuracy from 76% to 95%+.
    - **Hyperparameter Tuning:** Experimenting with dropout rates and kernel sizes to further reduce validation loss.

---

## 🧰 Tools Used

- **TensorFlow / Keras** (Model Building)
- **Python** (Pandas, NumPy)
- **Matplotlib / Seaborn** (Visualization)
- **Jupyter Notebook** (Development Environment)
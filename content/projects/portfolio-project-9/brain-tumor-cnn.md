---
title: "Brain Tumor Detection with CNNs"
course: "Artificial Intelligence and Deep Learning"
summary: "A healthcare-focused image classification project using Convolutional Neural Networks to detect brain tumors from MRI scans. Includes image preprocessing, CNN modeling, and accuracy evaluation."
tags: ["Computer Vision", "Deep Learning", "Healthcare", "CNN", "Medical Imaging"]
categories: ["Machine Learning", "Portfolio Projects"]
techstack: "Python"
---

## 🧠 Brain Tumor Detection with CNNs

**Category:** Computer Vision, Healthcare AI  
**Tools:** Python, TensorFlow/Keras, OpenCV  
**Skills:** Image preprocessing, CNN modeling, binary classification, model tuning, healthcare dataset application

---

### 🔍 Problem Statement

The objective of this project was to classify brain MRI scans as either showing the presence or absence of a tumor. This binary classification task is essential in medical imaging, where early detection can significantly impact patient outcomes.

---

### 📊 Dataset

- **Source:** Brain Tumor MRI Dataset (via Kaggle)
- **Structure:** Two classes – `yes` (tumor present), `no` (tumor absent)
- **Preprocessing:**
  - Grayscale image conversion and resizing
  - Histogram equalization using OpenCV
  - Normalization and reshaping for CNN input

---

### 🧠 CNN Model Architecture

The project involved building and tuning a Convolutional Neural Network using TensorFlow/Keras. Key layers included:

- **Convolutional Layers** with ReLU activation  
- **MaxPooling Layers** to reduce dimensionality  
- **Flatten + Dense Layers** for classification  
- **Dropout** to prevent overfitting  
- **Sigmoid Output Layer** for binary classification

Model performance was monitored using loss and accuracy curves across multiple training runs and experiments.

---

### 📈 Results

- Achieved high validation accuracy (>90%)  
- Showed stable training/validation curves after tuning  
- Successfully differentiated between MRI images with and without tumors  
- Included clear visualizations of data samples and model predictions

---

### 🔧 Key Techniques

- OpenCV image enhancement techniques for medical data  
- CNN model building and experimentation  
- Cross-validation and tuning for reliable results  
- Evaluation using binary classification metrics (accuracy, loss)

---

### 📌 Reflection

This project demonstrated how deep learning can assist in medical image diagnosis. The experiments highlighted the importance of preprocessing in medical datasets and how model tuning affects real-world classification outcomes.

**Future directions:**
- Incorporate transfer learning with pretrained CNNs (e.g., VGG, ResNet)  
- Use Grad-CAM to visualize what parts of the brain the model focuses on  
- Explore deployment options for clinical decision support

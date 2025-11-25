---
title: "Brain Tumor Classification: A Transfer Learning Comparative Study"
summary: "A comparative study evaluating Custom CNNs against Transfer Learning architectures (VGG16, ResNet50) for the multi-class classification of brain tumors from MRI scans."

tags:
  - Computer Vision
  - Transfer Learning
  - VGG16
  - ResNet50
  - TensorFlow
  - Medical Imaging

categories:
  - Deep Learning

project types: 
  - Academic
  - Research

techstack:
    - Python
    - TensorFlow/Keras
    - OpenCV
    - Scikit-Learn

source_url: https://github.com/jremsza/computer-vision_brain-scans.git
---

## 🧠 Brain Tumor Classification: Transfer Learning Comparative Study

**Category:** Computer Vision, Healthcare AI  
**Tools:** Python, TensorFlow/Keras, OpenCV, Scikit-Learn  
**Skills:** Multi-class Classification, Transfer Learning, Model Benchmarking, Data Augmentation, Overfitting Mitigation

---

### 🔍 Problem Statement

Classifying brain tumors is a complex challenge that goes beyond simple detection. This project focused on the multi-class classification of MRI scans into four distinct categories: **Glioma**, **Meningioma**, **Pituitary**, and **Healthy**.

The objective was not just to build a model that works, but to determine the optimal architecture for distinguishing between subtle anatomical differences in medical imagery.

![img-grid](/images/brain-cnn/img-grid.png) <br>

*Figure 1: Samples from the dataset showing the visual variability between the four classes.*

---

### 🧪 Experimental Approach

Instead of relying on a single architecture, I conducted a comparative study to maximize classification accuracy. The experiment tested three distinct approaches:

1.  **Baseline Custom CNN:** A standard 4-layer Convolutional Neural Network to establish a performance floor.
2.  **Transfer Learning (Feature Extraction):** Leveraged **ResNet50** and **VGG16** (pretrained on ImageNet) to utilize their advanced feature extraction capabilities.
3.  **Optimization Strategy:** Applied **Data Augmentation** (rotation, flips, contrast adjustments) specifically to the VGG16 model to combat overfitting observed in early trials.

---

### 📊 Results & Evaluation

To determine the optimal architecture, I conducted 10 distinct experiments, benchmarking a custom CNN against industry-standard Transfer Learning models (ResNet50, VGG16).

**Key Findings:**
* **VGG-16** consistently outperformed ResNet50 and the Custom CNN.
* **ResNet50** struggled with this specific dataset, likely due to the small image size or insufficient training data for its depth.
* **Model 10 (VGG-16 with Data Augmentation)** achieved the highest robustness (Test Acc: 96.3%), though at the cost of significantly longer training time (513s vs 42s for baseline).

#### 🏆 Model Performance Summary

| Experiment | Train Loss | Val Acc | Test Acc | Epochs | Duration (s) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Model 1: Baseline CNN** | 1.000 | 92.5% | 94.5% | 15 | 47s |
| **Model 2: CNN - Added Complexity** | 0.266 | 92.5% | 93.5% | 20 | 76s |
| **Model 3: CNN - Refine** | 0.249 | 94.4% | 94.7% | 22 | 73s |
| **Model 4: Baseline ResNet50** | 0.507 | 78.3% | 78.0% | 25 | 122s |
| **Model 5: ResNet50 - Complexity** | 0.733 | 78.3% | 75.7% | 15 | 90s |
| **Model 6: ResNet50 - Augment** | 0.673 | 75.6% | 75.0% | 9 | 57s |
| **Model 7: Baseline VGG-16** | 0.047 | 95.3% | 95.6% | 5 | 43s |
| **Model 8: VGG-16 Complexity** | 0.356 | 91.7% | 95.0% | 25 | 127s |
| **Model 9: VGG-16 - Refine** | 0.330 | 95.5% | **96.7%** | 20 | 94s |
| **Model 10: VGG-16 Data Augment** | 0.520 | **95.9%** | 96.3% | 100 | 514s |

![Model Performance Comparison Chart](/images/brain-cnn/bar_chart.png)
*Figure 2: VGG-16 variants (Models 7-10) demonstrated superior accuracy compared to ResNet50 and the Custom CNN.*

#### Error Analysis
To understand *where* the model failed, I analyzed the Confusion Matrix. The model achieved near-perfect precision on "Healthy" scans (class 2) However, slight confusion persisted between **Meningioma** (class 1) and **Glioma** (class 0) classes, likely due to their similar positioning within the brain structure.

![Insert Confusion Matrix Heatmap from the VGG16 Model](/images/brain-cnn/conf-matrix.png)
*Figure 3: Confusion matrix highlighting the model's predictive performance across all four classes.*

---

### 🔧 Key Technical Challenges

* **Handling Overfitting:** Early models showed a large gap between training and validation accuracy. I resolved this by implementing image augmentation (rotation, zoom, shear) to artificially expand the training dataset diversity.
* **Input Preprocessing:** Adapted raw MRI images to fit the specific input requirements of pre-trained networks (e.g., resizing to 224x224, RGB conversion).

---

### 📌 Reflection & Future Scope

This project demonstrated the power of **Transfer Learning** in medical imaging where labeled data is often scarce. While the Custom CNN provided a learning opportunity, the pre-trained VGG16 model illustrated how leveraging existing weights can drastically reduce training time and improve accuracy.

**Future directions:**
* **Explainability:** Implement **Grad-CAM** to visualize exactly which regions of the MRI scan the CNN is focusing on to make its prediction.
* **Deployment:** Wrap the model in a Flask/Streamlit API to allow clinicians to upload scans for real-time inference.
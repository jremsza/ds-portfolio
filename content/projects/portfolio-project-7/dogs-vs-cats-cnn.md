---
title: "Dogs vs Cats Image Classification"
summary: "A computer vision project using CNNs to classify images of cats and dogs from the Kaggle dataset. Includes image preprocessing, data augmentation, and CNN model design using TensorFlow/Keras."
tags: ["Computer Vision", "CNN", "TensorFlow", "Deep Learning", "Image Classification"]
categories: ["Machine Learning", "Portfolio Projects"]
project types: ["Academic", "Personal"]
techstack: "Python"
---

## 🐶🐱 Dogs vs Cats: Image Classification with CNNs

**Category:** Computer Vision, Deep Learning  
**Tools:** Python, TensorFlow/Keras, Matplotlib, Seaborn  
**Skills:** CNN architecture, image preprocessing, EDA, class balancing, data augmentation, performance evaluation

---

### 🔍 Problem Statement

The goal of this project was to build a convolutional neural network (CNN) that accurately classifies images of cats and dogs. This binary classification task is a popular computer vision benchmark and is great for hands on deep learning for image recognition.

---

### 📊 Dataset

- **Source:** Kaggle Dogs vs. Cats Redux
- **Size:** 25,000 labeled images of cats and dogs
- **Preprocessing:**
  - File parsing to assign labels from filenames
  - Sampled a 5% subset for quicker experimentation
  - Image resizing, normalization, and augmentation

---

### 🧠 Modeling Approach

A custom CNN was built using TensorFlow and Keras:

- **Convolutional Layers** with ReLU activation  
- **MaxPooling Layers** to reduce spatial dimensions  
- **Dropout** for regularization  
- **Dense Output Layer** with sigmoid activation

Data augmentation was applied using `ImageDataGenerator` to improve generalization. The data was split into training and validation sets, and performance was evaluated using accuracy and loss curves.

---

### 📈 Results

- The model achieved **strong validation accuracy** on the subset dataset.
- The class balance was well maintained between cats and dogs.
- Visualizations include:
  - Sample training images  
  - Distribution of class labels  
  - Training vs. validation loss and accuracy curves

---

### 🔧 Key Techniques

- Subsetting large datasets for rapid iteration  
- Real-time image augmentation for robustness  
- Custom CNN architecture design  
- Use of dropout and pooling to mitigate overfitting  
- Data pipeline optimization with Keras generators

---

### 📌 Reflection

This project deepened my understanding of image preprocessing and convolutional network design. Future work could include:
- Using transfer learning with a pretrained model (e.g., VGG16, ResNet)  
- Hyperparameter tuning  
- Deploying the model as a web app

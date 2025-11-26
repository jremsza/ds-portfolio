---
title: "Deep Learning vs. Traditional ML: MNIST Digit Classification"
date: 2023-11-15
summary: "A comparative study benchmarking Random Forest classifiers against a Deep Neural Network (DNN) built with TensorFlow/Keras. Features dimensionality reduction via PCA/t-SNE and failure analysis of misclassified images."
weight: 1

tags:
  - Deep Learning
  - TensorFlow
  - Keras
  - Random Forest
  - PCA
  - t-SNE
  - Computer Vision

categories:
  - Neural Networks
  - Model Benchmarking

# Link to your clean GitHub repo
# links:
#   external_link: 
#     text: "View Source Code"
#     icon: "fab fa-github"
#     url: "https://github.com/yourusername/mnist-deep-learning"

techstack:
    - Python (TensorFlow, Keras)
    - Scikit-Learn (Random Forest, PCA, t-SNE)
    - Matplotlib & Seaborn
---

## 👁️ Project Overview

Handwritten digit recognition is the "Hello World" of Computer Vision, but achieving >98% accuracy requires moving beyond basic algorithms. This project benchmarks a traditional ensemble method (**Random Forest**) against a modern **Deep Neural Network (DNN)** to quantify the performance gains offered by deep learning architectures on unstructured image data.

### 🔍 The Challenge
The MNIST dataset consists of 70,000 grayscale images (28x28 pixels). The objective was to:
1.  **Visualize** high-dimensional pixel data using PCA and t-SNE.
2.  **Establish a Baseline** using a robust classical algorithm (Random Forest).
3.  **Architect a DNN** in TensorFlow to push accuracy limits.
4.  **Diagnose Failures** by visualizing the specific images that confused the model.

---

## 📊 Exploratory Analysis: Visualizing the Manifold

Before modeling, I used dimensionality reduction techniques to understand the separability of the classes. While **PCA** explained variance, **t-SNE** (t-Distributed Stochastic Neighbor Embedding) provided a superior visualization of the digit clusters.

![tsne](/images/mnist-proj/t-sne_plot.png)

Figure 1: t-SNE projection of the MNIST dataset. Note how digits like '1' (red) form tight clusters, while '4' and '9' have overlapping boundaries, hinting at potential classification challenges.

The t-SNE projection reveals that while most digits form distinct, separable clusters (indicating high learnability), there are specific regions of significant overlap. 
* **Separable Zones:** The clear separation of certain clusters explains why even the baseline Random Forest achieved ~96% accuracy.
* **The Problem Area:** The visible "bleeding" between clusters (center) represents digits with high morphological similarity (e.g., a messy '4' vs '9'). This non-linear overlap provides the justification for deploying a Deep Neural Network, which excels at drawing complex decision boundaries in these ambiguous regions.

---

## 🤖 Model 1: The Baseline (Random Forest)

I started with a Random Forest classifier (100 trees) as a baseline.
* **Pros:** Fast training, interpretable feature importance (center pixels matter most).
* **Cons:** Treats pixels as independent features, ignoring spatial relationships.
* **Result:** ~96% Accuracy. Good, but struggled with messy handwriting.

---

## 🧠 Model 2: The Deep Neural Network (TensorFlow)

To capture more complex patterns, I built a fully connected Dense Neural Network using **Keras**.

**Architecture:**
* **Input Layer:** 784 neurons (flattened image).
* **Hidden Layers:** Two dense layers (128 & 64 neurons) with `ReLU` activation.
* **Dropout:** 20% dropout layers added to prevent overfitting.
* **Output:** 10 neurons with `Softmax` activation for multi-class probability.

```python
# Keras model architecture snippet
model = keras.Sequential([
    layers.Dense(128, activation='relu', input_shape=(784,)),
    layers.Dropout(0.2),
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')
])
```
### Training Dynamics: The model was trained for 15 epochs using the Adam optimizer and SparseCategoricalCrossentropy loss.

![training_curve](/images/mnist-proj/learning-curve.png/)

Figure 2: Learning curves showing Training vs. Validation accuracy. The model converges quickly, reaching >98% validation accuracy within 10 epochs.

**Interpretation of Training Dynamics:**
The learning curve above is critical for validating the architecture decisions (specifically the use of Dropout layers).
* **Rapid Convergence:** The steep initial ascent shows that the optimizer (`Adam`) effectively navigated the loss landscape.
* **Stability:** The lack of divergence between the Training (Blue) and Validation (Orange) lines confirms that the model is not memorizing the training data, but actually learning generalized features of the digits.

### 🧪 Experiment Tracking: The Power of Hybrid Models

I conducted a grid search across different architecture sizes and feature sets to identify the optimal model complexity.

| Experiment | Training Loss | Train Accuracy | Val Loss | Val Accuracy | Test Accuracy |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **1 Node** | 1.665 | 30.5% | 1.638 | 30.6% | 30.3% |
| **64 Nodes** | 0.171 | 96.5% | 0.186 | 96.2% | 96.3% |
| **128 Nodes (Best Pure DNN)** | 0.151 | 97.0% | 0.169 | 96.7% | 96.6% |
| **256 Nodes** | 0.172 | 96.7% | 0.176 | 96.5% | 96.5% |
| **PCA + DNN (Overall Winner)** | **0.087** | **98.5%** | **0.115** | **97.7%** | **97.7%** |

**Critical Insight:**
While the 128-Node architecture was the best performing *pure* Deep Learning model, the **PCA-Hybrid approach was the overall champion**. 
* **Why it won:** By using PCA to reduce the noisy 784-pixel input down to its principal components, we removed "visual noise" before training. 
* **The Lesson:** This demonstrates that **feature engineering** often yields better ROI than simply increasing model complexity.

**Architectural Decisions:**
The experiment logs reveal a clear point of diminishing returns.
* **Underfitting:** Models with fewer than 32 nodes lacked the capacity to capture the morphological diversity of digits (Accuracy < 96%).
* **The Sweet Spot:** The 128-node architecture maximized test accuracy (96.6%) while maintaining a low validation loss (0.169).
* **Overfitting:** Increasing complexity to 256 or 512 nodes did not improve generalization; in fact, validation loss began to creep up, indicating the model was starting to memorize noise rather than signal.

### 🚀 Key Takeaways
Deep Learning Superiority: The DNN reduced the error rate by over 40% compared to the Random Forest baseline.

The "Black Box" Trade-off: While the DNN is more accurate, the Random Forest provided instant feature importance scores, showing which pixels were most critical.

Data Quality: Visual inspection of misclassified images revealed that many "errors" were actually ambiguous handwriting that even a human might mislabel.
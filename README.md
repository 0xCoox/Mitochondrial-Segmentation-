# 🔬 FIB/SEM Organelle & Mitochondria Classification

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=flat&logo=PyTorch&logoColor=white)](https://pytorch.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1YAB6wLmHx2t8WpbgldcQNXFBrOkCnu9F)

## 📌 Project Overview
This project falls within the field of **Cellular Imaging and Healthcare AI**. The objective is to automatically recognize and identify various cellular organelles (such as mitochondria) from FIB/SEM electron microscopy images. 

Although FIB/SEM images are initially large 3D volumes, the problem was approached as a **supervised 2D image classification task**: the model analyzes image patches extracted around annotated pixels to predict the class of the central pixel.

## 🧠 Data Strategy and Processing
The initial dataset contains **14,000 grayscale images (257x257 pixels)** distributed across 5 organelle classes. 

To optimize training and ensure model robustness, the following strategy was adopted:
* **Stratified Splitting:** The data was split into 95% for training (13,300 images) and 5% for validation (700 images) while preserving the original class distribution.
* **Handling Class Imbalance:** Since the classes are highly imbalanced (the majority class represents 48% of the data, while the minority represents only 5%), an inverse weighting was applied to the loss function (`CrossEntropyLoss(weight=weights_tensor)`) to heavily penalize errors on rare classes.

## ⚙️ Architecture and Training (PyTorch)
A Convolutional Neural Network (CNN) was developed and trained from scratch.
* **Framework:** PyTorch (executed on an NVIDIA Tesla T4 GPU).
* **Optimizer:** Adam (`lr=5e-4`) paired with a `ReduceLROnPlateau` scheduler to dynamically adjust the learning rate.
* **Overfitting Prevention:** Implementation of *Early Stopping* with a patience of 8 epochs to save the best model weights.

## 📊 Results and Performance
The model achieved a **Validation Accuracy of 88%** on complex cellular data. 

### Learning Curves
*Evolution of the loss function and accuracy over the epochs:*

![Loss/Accuracy Learning Curves]([INSERT: LINK TO YOUR CURVES IMAGE])

### Prediction Examples
*Comparison between raw microscopy images and the model's predictions:*

![Examples of mitochondria predictions]([INSERT: LINK TO AN IMAGE SHOWING PATCHES WITH PREDICTED LABELS])

## 🚀 Usage
The complete code, from data preparation to evaluation, is available and documented step-by-step in the `mitochondrial_segmentation.ipynb` notebook. 

You can test it directly in your browser without any installation via Google Colab by clicking the badge at the top of the page.

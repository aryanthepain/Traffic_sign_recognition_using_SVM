# Traffic Sign Recognition Based on HOG Feature and SVM 🚦

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-Latest-orange.svg)](https://scikit-learn.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Latest-green.svg)](https://opencv.org/)

## 📌 Overview
This repository implements a traditional computer vision pipeline inspired by research on *"Traffic Sign Recognition Based on HOG Feature and SVM"*. The primary goal of this project is to achieve intelligent detection and automatic recognition of multi-category natural road traffic signs, which serves as an essential technology for autonomous driving systems. By leveraging classical computer vision techniques, the pipeline handles image enhancement, spatial localization, feature extraction, and machine learning classification.

## 📂 Dataset
* The primary dataset used for training and testing is the **GTSRB (German Traffic Sign Recognition Benchmark)** dataset.
* To balance the class distribution and improve model robustness, the dataset is augmented using translation, rotation, and affine transformations.
* The dataset spans **43 distinct classes** of traffic signs—including indicator, prohibition, speed limit, and warning signs—alongside negative background samples that do not contain traffic signs.

## 🧠 Pipeline & Methodology

### 1. Preprocessing and Image Enhancement
* The original input image is converted into the YUV color space.
* To resolve issues with blurriness and low brightness, adaptive histogram equalization is applied specifically to the Y-channel.
* The image is independently converted into the HSV color space, where image mask technology is applied to the H component to segment the critical traffic sign colors: blue, yellow, and red.

### 2. Traffic Sign Localization
* For circular traffic signs, the Hough transformation is utilized to detect and extract the complex curve and circle shapes from the image space.
* For triangular and rectangular signs, the system extracts contours and applies polygon fitting. 
* A contour containing exactly 3 vertices is identified as a triangle, while a contour with 4 vertices is classified as a rectangle.

### 3. Feature Extraction (HOG)
* Traffic sign candidate images are resized to a standard dimension of 64x64 pixels.
* The system extracts Histogram of Oriented Gradients (HOG) features to accurately represent the edge and outline information of the traffic signs.
* The HOG parameters are meticulously configured: images are divided into 8x8 pixel cells, blocks are formed using 4 adjacent cells (2x2), and gradients are calculated across 9 directions.
* This specific configuration yields a highly descriptive final HOG feature vector of 1764 dimensions.

### 4. Classification (SVM)
* A Support Vector Machine (SVM) is employed to map the extracted HOG features into a high-dimensional space to find the optimal classification hyperplane.
* The Radial Basis Function (RBF) kernel is utilized for the classifier to handle non-linear relationships.
* The SVM penalty factor (C) is optimized to maximize classification accuracy across all 43 classes while maintaining generalization.

## 📈 Results & Performance
* The finalized SVM model, utilizing the RBF kernel, achieves a robust **test accuracy of 95.2%** across all 43 classes of the GTSRB dataset.
* The recognition system demonstrates reliable performance across varying environmental conditions, successfully identifying traffic signs in sunny, rainy, and foggy weather scenarios.
* The model retains the ability to accurately identify signs under minor partial occlusion, such as a sign partially covered by a tree branch or shadow.

## ⚠️ Limitations & Challenges
* The reliability of the detection results can be negatively impacted by extremely small target areas, severe motion blurring, and interference from background objects sharing the exact color and shape of legitimate traffic signs.
* Traffic signs that contain a high density of detailed information (e.g., specific numeric speed limits like 30 vs. 50 vs. 80) across the 43 classes are more prone to recognition errors when subjected to heavy partial occlusion or low resolution.

## 🚀 Extensions & Future Work
While this repository establishes a highly accurate baseline utilizing traditional Computer Vision (HOG + SVM), future iterations will explore replacing the feature extraction and classification steps with Deep Learning architectures. Transitioning from SVMs to advanced frameworks like Convolutional Neural Networks (CNNs), Vision Transformers (ViT), or Hybrid CNN-Transformer models could further improve predictive capabilities on heavily occluded, small, or detail-dense traffic signs in complex environments.

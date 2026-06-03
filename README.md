# Traffic Sign Recognition Based on HOG Feature and SVM 🚦

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-Latest-orange.svg)](https://scikit-learn.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Latest-green.svg)](https://opencv.org/)

## 📌 Overview
This repository implements the methodology described in the research paper *"Traffic Sign Recognition Based on HOG Feature and SVM"*[cite: 1]. The primary goal of this project is to achieve intelligent detection and automatic recognition of multi-category natural road traffic signs, which serves as an essential technology for unmanned driver systems[cite: 1]. By leveraging traditional computer vision techniques, the pipeline handles image enhancement, spatial localization, feature extraction, and machine learning classification.

## 📂 Dataset
* The primary dataset used for training and testing is the TT100K traffic sign dataset[cite: 1].
* To balance the class distribution, the dataset is augmented using translation, rotation, and affine transformations[cite: 1].
* The curated training set consists of 22 common positive samples—spanning indicator, prohibition, and warning signs—alongside negative background samples that do not contain traffic signs[cite: 1].
* Additional testing and validation are performed using select images from the CCTSDB dataset[cite: 1].

## 🧠 Pipeline & Methodology

### 1. Preprocessing and Image Enhancement
* The original input image is converted into the YUV color space[cite: 1].
* To resolve issues with blurriness and low brightness, adaptive histogram equalization is applied specifically to the Y-channel[cite: 1].
* The image is independently converted into the HSV color space, where image mask technology is applied to the H component to segment the colors blue, yellow, and red[cite: 1].

### 2. Traffic Sign Localization
* For circular traffic signs, the Hough transformation is utilized to detect and extract the complex curve and circle shapes from the image space[cite: 1].
* For triangular and rectangular signs, the system extracts contours and applies polygon fitting[cite: 1]. 
* A contour containing exactly 3 vertices is identified as a triangle, while a contour with 4 vertices is classified as a rectangle[cite: 1].

### 3. Feature Extraction (HOG)
* Traffic sign candidate images are resized to a standard dimension of 64x64 pixels[cite: 1].
* The system extracts Histogram of Oriented Gradients (HOG) features to accurately represent the edge and outline information of the traffic signs[cite: 1].
* The HOG parameters are meticulously configured: images are divided into 8x8 pixel cells, blocks are formed using 4 adjacent cells, and gradients are calculated across 9 directions[cite: 1].
* This specific configuration yields a final HOG feature dimension of 1764[cite: 1].

### 4. Classification (SVM)
* A Support Vector Machine (SVM) is employed to map the extracted HOG features into a high-dimensional space to find the optimal classification hyperplane[cite: 1].
* The Radical Basis Function (RBF) kernel is utilized for the classifier[cite: 1].
* The SVM penalty factor (C) is optimized and set to 60 to maximize classification accuracy while maintaining generalization[cite: 1].

## 📈 Results & Performance
* The finalized SVM model, utilizing the RBF kernel and a penalty factor of 60, achieves a test accuracy of 97.458%[cite: 1].
* Comparative testing of other kernel functions yielded accuracies of 97.233% for the Linear kernel, 97.110% for the Sigmoid kernel, and 20.578% for the Polynomial kernel[cite: 1].
* The recognition system demonstrates robust performance across varying environmental conditions, successfully identifying traffic signs in sunny, rainy, and foggy weather[cite: 1].
* The model also retains the ability to accurately identify signs under minor partial occlusion, such as a stop sign partially covered by a tree branch[cite: 1].

## ⚠️ Limitations & Challenges
* The reliability of the detection results can be negatively impacted by extremely small target areas, severe motion blurring, and interference from background objects sharing the exact color and shape of legitimate traffic signs[cite: 1].
* Traffic signs that contain a high density of detailed information (e.g., specific numeric speed limits) are more prone to recognition errors when subjected to partial occlusion[cite: 1].

## 🚀 Extensions & Future Work
While this repository establishes a highly accurate baseline utilizing traditional Computer Vision (HOG + SVM), future iterations will explore replacing the feature extraction and classification steps with Deep Learning architectures. Transitioning from SVMs to advanced frameworks like Convolutional Neural Networks (CNNs), Vision Transformers (ViT), or Hybrid CNN-Transformer models could further improve predictive capabilities on heavily occluded, small, or detail-dense traffic signs in complex environments.

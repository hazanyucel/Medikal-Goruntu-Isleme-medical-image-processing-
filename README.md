# 🫀 Automated Cardiac Diagnosis Challenge (ACDC) - Segmentation Project

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)
![License](https://img.shields.io/badge/License-MIT-green)

## 📌 Project Overview
This project focuses on the **semantic segmentation of cardiac MRI images** using the ACDC (Automated Cardiac Diagnosis Challenge) dataset. The goal is to automatically segment three key structures of the heart to assist in the diagnosis of cardiac pathologies.

We implementing and comparing **5 different deep learning architectures** to determine the best performing model for this medical imaging task.

### 🎯 Segmentation Classes
The models are trained to segment 4 classes:
0. **Background**
1. **Right Ventricle (RV)**
2. **Myocardium (Myo)**
3. **Left Ventricle (LV)**

---

## 🏗️ Methodology

### 1. Dataset & Preprocessing
The dataset consists of 3D NIfTI/H5 volumes. The following preprocessing steps were applied:
* **Slicing:** 3D volumes were sliced into 2D images.
* **Filtering:** Empty masks were removed to optimize training.
* **Resizing:** Images resized to `128x128` (can be adjusted).
* **Normalization:** Pixel intensities scaled to [0, 1] range.
* **One-Hot Encoding:** Masks converted to categorical format.

### 2. Architectures Implemented
We utilized the `segmentation-models` library with **ResNet34** as the backbone (Pre-trained on ImageNet) for all models to ensure a fair comparison:

1.  **U-Net:** The gold standard for medical image segmentation.
2.  **U-Net++ (Nested U-Net):** An architecture with dense skip connections to capture fine details.
3.  **FPN (Feature Pyramid Network):** Good for detecting objects at different scales.
4.  **LinkNet:** Efficient and fast architecture.
5.  **PSPNet:** Pyramid Scene Parsing Network for global context embedding.

### 3. Loss Function & Metrics
* **Loss:** `Dice Loss` + `Categorical Focal Loss` (To handle class imbalance).
* **Metrics:** IoU (Intersection over Union), Dice Coefficient, F1-Score, Accuracy.

---

## 📊 Comparative Results

After training the models for 30 epochs, the following results were obtained on the test set:

| Model Architecture | Backbone | Dice Score | IoU Score |
|--------------------|----------|------------|-----------|
| **U-Net** | ResNet34 | 0.9946  | 0.8823  |
| **U-Net++** | ResNet34 | 0.9943 | 0.8775 |

*(Note: U-Net++ demonstrated superior performance in capturing boundary details, specifically for the Myocardium.)*

---

## 🖼️ Visualizations

Here are some qualitative results comparing the **Ground Truth** (Radiologist's annotation) vs. **Model Prediction**:

### U-Net++ Predictions
![U-Net++ Result](https://github.com/hazanyucel/Medikal-Goruntu-Isleme-medical-image-processing-/blob/main/images/ornek_resim_1.png)
*Figure 1: Successful segmentation of RV, Myo, and LV.*

### Comparative View
![Comparison](https://github.com/hazanyucel/Medikal-Goruntu-Isleme-medical-image-processing-/blob/main/images/ornek_resim_2.png)
*Figure 2: Comparison of difficult slices.*

---

## 🚀 Installation & Usage

### Prerequisites
```bash
pip install tensorflow segmentation-models nibabel matplotlib opencv-python h5py

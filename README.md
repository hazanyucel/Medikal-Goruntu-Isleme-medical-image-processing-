#  Otomatik Kardiyak Teşhisi (ACDC) - Segmentasyon Projesi

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)


##  Proje Özeti
Bu proje, ACDC (Automated Cardiac Diagnosis Challenge) veri setini kullanarak **kardiyak MR görüntülerinin anlamsal segmentasyonuna** odaklanmaktadır. Amaç, kalp patolojilerinin teşhisine yardımcı olmak için kalbin üç temel yapısını otomatik olarak bölümlemektir (segmentasyon).

Bu medikal görüntüleme görevi için en iyi performansı gösteren modeli belirlemek amacıyla **5 farklı derin öğrenme mimarisi** uygulanacak ve karşılaştırılacaktır.

###  Segmentasyon Sınıfları
Modeller aşağıdaki 4 sınıfı ayırt etmek üzere eğitilmiştir:
0. **Arka Plan (Background)**
1. **Sağ Ventrikül (RV)**
2. **Miyokard - Kalp Kası (Myo)**
3. **Sol Ventrikül (LV)**

---

##  Metodoloji

### 1. Veri Seti ve Ön İşleme
Veri seti 3 boyutlu NIfTI/H5 hacimlerinden oluşmaktadır. Aşağıdaki ön işleme adımları uygulanmıştır:
* **Dilimleme (Slicing):** 3D hacimler 2D görüntülere ayrıldı.
* **Filtreleme:** Eğitimi optimize etmek için boş maskeler veri setinden çıkarıldı.
* **Yeniden Boyutlandırma:** Görüntüler `128x128` boyutuna getirildi (değiştirilebilir).
* **Normalizasyon:** Piksel yoğunlukları [0, 1] aralığına ölçeklendi.
* **One-Hot Encoding:** Maskeler kategorik formata dönüştürüldü.

### 2. Uygulanan Mimariler
Adil bir karşılaştırma sağlamak için tüm modellerde `segmentation-models` kütüphanesi kullanılmış ve omurga (backbone) olarak **ResNet34** (ImageNet üzerinde ön eğitimli) seçilmiştir:

1.  **U-Net** 
2.  **U-Net++ (Nested U-Net)** 
3.  **TransUNet** 
4.  **AttentionUNet** 
5.  **ResUNet** 
### 3. Kayıp Fonksiyonu ve Metrikler
* **Kayıp Fonksiyonu (Loss):** `Dice Loss` + `Categorical Focal Loss` (Sınıf dengesizliğini yönetmek için).
*  Dice Katsayısı.

---

##  Karşılaştırmalı Sonuçlar

Modellerin 30 epoch boyunca eğitilmesinin ardından test setinde elde edilen sonuçlar:

| Model Mimarisi | Omurga (Backbone) | Dice Skoru | IoU Skoru |
|----------------|-------------------|------------|-----------|
| **U-Net** | ResNet34 | 0.9353  | 0.8823  |
| **U-Net++** | ResNet34 | 0.9324 | 0.8775 |
| **TransU-Net** | ResNet34 | 0.9146 |  |
| **AttentionUNet** | ResNet34 | 0.9182 |  |
| **ResUNEt** | ResNet34 | 0.8922 |  |


*(Not: U-Net++, özellikle miyokard sınır detaylarını yakalamada üstün performans göstermiştir.)*



#  Automated Cardiac Diagnosis Challenge (ACDC) - Segmentation Project

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)


##  Project Overview
This project focuses on the **semantic segmentation of cardiac MRI images** using the ACDC (Automated Cardiac Diagnosis Challenge) dataset. The goal is to automatically segment three key structures of the heart to assist in the diagnosis of cardiac pathologies.

We implementing and comparing **5 different deep learning architectures** to determine the best performing model for this medical imaging task.

###  Segmentation Classes
The models are trained to segment 4 classes:
##
0. **Background**
1. **Right Ventricle (RV)**
2. **Myocardium (Myo)**
3. **Left Ventricle (LV)**

---

##  Methodology

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

##  Comparative Results

After training the models for 30 epochs, the following results were obtained on the test set:

| Model Architecture | Backbone | Dice Score | IoU Score |
|--------------------|----------|------------|-----------|
| **U-Net** | ResNet34 | 0.9353  | 0.8823  |
| **U-Net++** | ResNet34 | 0.9324 | 0.8775 |
| **TransU-Net** | ResNet34 | 0.9146 |  |
| **AttentionUNet** | ResNet34 | 0.9182 |  |
| **ResUNEt** | ResNet34 | 0.8922 |  |
|

*(Note: U-Net++ demonstrated superior performance in capturing boundary details, specifically for the Myocardium.)*


##  Installation & Usage

### Prerequisites
```bash
pip install tensorflow segmentation-models nibabel matplotlib opencv-python h5py

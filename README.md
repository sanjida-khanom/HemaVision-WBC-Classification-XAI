# HemaVision-WBC-Classification-XAI
<div align="center">

# 🩸 HemaVision

**Explainable Computer Vision (XAI) for Morphological White Blood Cell Classification**

[![IEEE CSDE 2026](https://img.shields.io/badge/Accepted-IEEE%20CSDE%202026-00629B?style=flat-square)](#-publication)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Dataset](https://img.shields.io/badge/Dataset-Raabin--WBC-20BEFF?style=flat-square&logo=kaggle&logoColor=white)](https://www.kaggle.com/datasets/raabindata/raabin-wbc)

</div>

## 📢 Publication

Official code for the paper **"HemaVision: EfficientNetV2 and CBAM-Based Explainable AI for Morphological White Blood Cell Classification and Clinical Decision Support"**, accepted at the **IEEE Asia-Pacific Conference on Computer Science and Data Engineering (IEEE CSDE 2026)**.
<p align="center"><img src="Paper%20Acceptance%20Mail.png" width="95%"></p>

**Authors:**
- Sanjida Khanom
- Md. Ashiqur Rahman
- Mohammod Ashikur Rahman
- Muhammad Aminur Rahaman
- Md. Ahsan Habib
- Md Shafiqul Islam

## 📌 Overview

HemaVision classifies five types of white blood cells from blood smear images and explains every prediction.

- **EfficientNetV2-B0** backbone for efficient feature extraction
- **CBAM attention** to focus on the cell and suppress background noise
- **Grad-CAM** heatmaps showing which regions drove each prediction
- **Clinical Decision Report** combining the prediction, confidence, heatmap and cell information

<p align="center"><img src="Clinical%20decision%20report.png" width="95%"></p>

## 📂 Dataset

[Raabin-WBC](https://www.kaggle.com/datasets/raabindata/raabin-wbc): 16,633 images across 5 classes (Basophil, Eosinophil, Lymphocyte, Monocyte, Neutrophil), split 70/15/15 with stratification. The data is highly imbalanced, so a WeightedRandomSampler and label smoothing are used during training.

<p align="center"><img src="Class%20Distribution.png" width="85%"></p>

## 📊 Results

| Metric | Score |
|:--|:--:|
| Validation Accuracy | **99.04%** |
| Test Accuracy | **98.60%** |
| Weighted F1-Score | 0.9859 |
| Macro-AUC | **0.9976** |

| Class | Precision | Recall | F1-Score |
|:--|:--:|:--:|:--:|
| Basophil | 0.978 | 1.000 | 0.989 |
| Eosinophil | 0.981 | 0.963 | 0.972 |
| Lymphocyte | 0.976 | 0.983 | 0.980 |
| Monocyte | 0.948 | 0.916 | 0.932 |
| Neutrophil | 0.993 | 0.994 | 0.993 |

<p align="center"><img src="Loss%20curve%20and%20accuracy%20curve.png" width="90%"></p>
<p align="center"><img src="Confusion%20Matrix.png" width="90%"></p>
<p align="center"><img src="Roc%20and%20Precision-recall%20curve.png" width="90%"></p>

## 🔍 Explainability

Grad-CAM confirms that the model focuses on the nucleus and cytoplasm instead of surrounding red blood cells. The t-SNE plot shows clearly separated feature clusters for each class.

<p align="center"><img src="Grad-Cam%20visualisation.png" width="80%"></p>
<p align="center"><img src="t-sne%20feature%20visualisation.png" width="65%"></p>

## ⚙️ How to Run

```bash
git clone https://github.com/sanjida-khanom/HemaVision-WBC-Classification-XAI.git
pip install torch torchvision timm grad-cam scikit-learn matplotlib seaborn pandas pillow
```

1. Download the [Raabin-WBC dataset](https://www.kaggle.com/datasets/raabindata/raabin-wbc).
2. Open `Hema_Vision_Final_Pipeline.ipynb` and set `BASE` to your dataset path (the default is the Kaggle path).
3. Run all cells. A GPU is recommended.

**Training setup:** 224×224 input, batch size 32, AdamW (backbone LR 2e-4, head LR 1e-3), cosine annealing with warm restarts, early stopping (patience 3).

> ⚠️ This is a research prototype and not a substitute for professional clinical diagnosis.

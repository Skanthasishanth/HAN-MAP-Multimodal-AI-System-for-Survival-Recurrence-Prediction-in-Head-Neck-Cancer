# HAN-MAP 🧠🩺

**Multimodal AI System for Survival & Recurrence Prediction in Head & Neck Cancer**

---

## 📌 Overview

HAN-MAP (**Head And Neck – Multimodal AI Prediction**) is a comprehensive **multimodal deep learning framework** designed to predict **5-year overall survival** and **2-year cancer recurrence** in patients diagnosed with **Head & Neck Cancer**.

The system integrates **five heterogeneous medical data modalities** into a single, uncertainty-aware predictive pipeline using **Variational Autoencoders (VAEs)** and a **Hierarchical Cross-modal Attention Transformer (HCAT)** architecture. By jointly modeling diverse clinical evidence, HAN-MAP captures complex inter-modal relationships that are often missed by traditional single-modality approaches.

This project was developed as part of **Project Work – Phase II**, motivated by real-world challenges in precision oncology, and evaluated using the **HANCOCK multimodal head and neck cancer dataset**.

---

## 🚀 Key Highlights

* 🔗 **True Multimodal Fusion** across Clinical, Pathological, Semantic, Spatial, and Temporal data
* 🧠 **Advanced Missing-Data Handling** using Joint Multimodal VAEs and graph-based smoothing
* 🎯 **Dual-Task Learning Framework** for survival and recurrence prediction
* ⚖️ **Uncertainty-Aware Modeling** with quality gates and Monte Carlo dropout
* 🧩 **Hierarchical Cross-modal Attention Transformer (HCAT)** for structured fusion
* 📈 **Strong Predictive Performance** on real-world, sparse clinical data

  * **5-Year Survival F1-score:** 0.80
  * **2-Year Recurrence F1-score:** 0.95

---

## 🏥 Clinical Motivation

Accurate prediction of survival and recurrence is critical for effective cancer care, as it directly impacts:

* Personalized treatment planning
* Risk-adaptive follow-up and monitoring
* Efficient allocation of healthcare resources

Conventional machine learning systems typically rely on **single-modality data**, limiting their ability to reflect the full clinical picture. HAN-MAP addresses this limitation by leveraging **deep multimodal learning**, enabling a more holistic and clinically meaningful representation of each patient.

---

## 🧬 Modalities Used

| Modality      | Description                                   | Encoder                     | Output |
| ------------- | --------------------------------------------- | --------------------------- | ------ |
| Clinical      | Demographics & structured clinical attributes | VAE + Denoising Autoencoder | 512-D  |
| Pathological  | Tumor and pathology features                  | VAE + Graph Smoothing       | 512-D  |
| Semantic Text | Free-text clinical and surgical reports       | ClinicalBERT / TF-IDF + SVD | 512-D  |
| Spatial       | Histopathology WSI patch features             | Spatial Transformer         | 512-D  |
| Temporal      | Longitudinal blood test records               | Physiology-aware LSTM       | 512-D  |

---

## 🧠 System Architecture

### 1️⃣ Single-Modality Preprocessing

Each modality is processed independently to address sparsity, noise, and heterogeneity:

* **Structured Clinical & Pathological Data**

  * Ensemble imputation (Median → KNN → VAE)
  * Patient similarity graph smoothing (RBF kernel)
  * Feature representation using mean, variance, and missingness masks

* **Temporal Blood Data**

  * Physiology-aware normalization
  * Cohort-level KNN refinement
  * Sequence encoding using denoising LSTM

* **Spatial Histopathology (WSI)**

  * Patch-level clustering (MiniBatch K-Means)
  * Positional bias injection via coordinate MLP
  * Transformer-based aggregation with Monte Carlo dropout

* **Semantic Text Data**

  * Contextual embeddings using ClinicalBERT
  * Lightweight fallback using TF-IDF + SVD

All preprocessing pipelines generate standardized **512-dimensional embeddings** per modality.

---

### 2️⃣ Advanced Cross-Modal Imputation (JAMIE-style VAE)

To handle incomplete patient records, HAN-MAP employs a **Joint Multimodal Variational Autoencoder** that:

* Learns a shared latent representation across all modalities
* Uses cross-modal attention to infer missing embeddings
* Estimates uncertainty for imputed features
* Iteratively refines latent representations using transformer layers

This design ensures robust performance even when one or more modalities are missing.

---

### 3️⃣ Hierarchical Cross-modal Attention Transformer (HCAT)

The fusion backbone consists of:

* **Quality Gates** to down-weight unreliable or imputed modalities
* **Modality Positional Encodings** to preserve modality identity
* **Local Branch Transformers**

  * Clinical ↔ Temporal fusion
  * Pathological ↔ Spatial fusion
* **Global Transformer Encoder** for holistic patient representation
* **Task-Specific Attention Heads** for survival and recurrence prediction

---

## 🎯 Prediction Tasks

HAN-MAP performs two binary classification tasks:

| Task              | Description                                |
| ----------------- | ------------------------------------------ |
| 5-Year Survival   | Predict long-term patient survival outcome |
| 2-Year Recurrence | Predict short-term cancer relapse risk     |

### Loss Functions

* Focal Loss for class imbalance
* VAE reconstruction + KL divergence loss
* Contrastive InfoNCE loss for representation learning

---

## 📊 Results

| Task              | Best F1-score |
| ----------------- | ------------- |
| 5-Year Survival   | 0.80          |
| 2-Year Recurrence | 0.95          |
| **Average**       | **0.875**     |

These results demonstrate strong generalization and robustness on sparse, real-world multimodal clinical data.

---

## 🛠️ Tech Stack

* **Programming Language:** Python 3.9+
* **Deep Learning Frameworks:** PyTorch, scikit-learn
* **Libraries:** NumPy, Pandas, h5py, TorchVision, HuggingFace Transformers
* **Hardware:** CUDA-enabled GPU recommended
* **Deployment (Optional):** Docker

---

## 📁 Repository Structure

```
HAN-MAP/
│── data/                  # Preprocessed HDF5 embeddings
│── models/                # Model architectures (VAE, HCAT)
│── preprocessing/         # Modality-specific pipelines
│── training/              # Training & evaluation scripts
│── inference/             # Prediction pipeline
│── checkpoints/           # Pretrained model weights
│── utils/                 # Helper functions
│── requirements.txt
│── README.md
```

---

## ▶️ Usage (High-Level)

```bash
pip install -r requirements.txt

python training/train_hcat.py

python inference/predict.py --input features.h5
```

---

## 🔒 Ethics & Data Privacy

* Designed with **HIPAA/GDPR-aligned principles**
* Supports controlled access and encrypted storage
* Intended strictly for **research and clinical decision support**
* Not intended for autonomous medical diagnosis

---

## 🌍 Sustainable Development Goals (SDGs)

* **SDG 3:** Good Health & Well-being
* **SDG 9:** Industry, Innovation & Infrastructure
* **SDG 10:** Reduced Inequalities
* **SDG 17:** Partnerships for the Goals

---

## 🔮 Future Work

* End-to-end learning from raw whole-slide images (WSI)
* Integration of genomics and proteomics data
* Explainable AI (XAI) dashboards for clinicians
* External validation on diverse oncology cohorts

---

## 👨‍🎓 Authors

**Kantha Sishanth S**

B.E. Computer Science & Engineering (CS)
Saveetha Engineering College, Chennai

**Perarasu M**

B.E. Computer Science & Engineering (CS)
Saveetha Engineering College, Chennai

**Santhosh S**

B.E. Computer Science & Engineering (CS)
Saveetha Engineering College, Chennai

---

## 📜 License

Released for **academic and research use only**.
Commercial usage requires explicit permission.

---

⭐ If you find this project useful, consider starring the repository!

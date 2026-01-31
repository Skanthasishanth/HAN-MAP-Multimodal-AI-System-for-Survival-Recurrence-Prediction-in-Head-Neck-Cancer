# HAN-MAP 🧠🩺

**Multimodal AI System for Survival & Recurrence Prediction in Head & Neck Cancer**

---

## 📌 Overview

HAN-MAP (**Head And Neck – Multimodal AI Prediction**) is an advanced multimodal deep learning framework designed to predict **5-year survival** and **2-year recurrence** outcomes for patients with **Head & Neck Cancer**.

The system integrates **five heterogeneous clinical modalities** into a unified, uncertainty-aware predictive pipeline using **Variational Autoencoders (VAE)** and a **Hierarchical Cross-modal Attention Transformer (HCAT)** architecture.

This project was developed as part of **Project Work – Phase II** and is inspired by real-world clinical challenges in precision oncology, leveraging the **HANCOCK multimodal cancer dataset**.

---

## 🚀 Key Highlights

* 🔗 **True Multimodal Fusion** (Clinical, Pathological, Semantic, Spatial, Temporal)
* 🧠 **Advanced Imputation** using Joint Multimodal VAE + Graph Smoothing
* 🎯 **Dual-Task Learning**: Survival & Recurrence prediction
* ⚖️ **Uncertainty-Aware Modeling** with Quality Gates & Monte-Carlo Dropout
* 🧩 **Hierarchical Transformer Fusion (HCAT)**
* 📈 **State-of-the-art Performance**

  * 5-Year Survival F1-score: **0.80**
  * 2-Year Recurrence F1-score: **0.95**

---

## 🏥 Clinical Motivation

Accurate prediction of cancer survival and recurrence is critical for:

* Personalized treatment planning
* Risk-adaptive follow-up strategies
* Optimized healthcare resource allocation

Traditional ML systems rely on **single-modality data**, failing to capture the complex interactions between clinical history, pathology, imaging, lab results, and textual reports. HAN-MAP overcomes this limitation through **deep multimodal learning**.

---

## 🧬 Modalities Used

| Modality      | Description                          | Encoder                     | Output |
| ------------- | ------------------------------------ | --------------------------- | ------ |
| Clinical      | Demographics & clinical attributes   | VAE + Denoising AE          | 512-D  |
| Pathological  | Tumor & pathology features           | VAE + Graph Smoothing       | 512-D  |
| Semantic Text | Free-text clinical & surgery reports | ClinicalBERT / TF-IDF + SVD | 512-D  |
| Spatial       | Histopathology WSI patches           | Spatial Transformer         | 512-D  |
| Temporal      | Blood test time-series               | Physiology-aware LSTM       | 512-D  |

---

## 🧠 System Architecture

### 1️⃣ Single-Modality Preprocessing

Each modality undergoes **independent preprocessing** to handle sparsity, noise, and heterogeneity.

* **Structured Data (Clinical/Pathological)**

  * Ensemble imputation (Median → VAE → KNN)
  * Patient graph smoothing (RBF kernel)
  * Composite features: Mean + Variance + Missingness Mask

* **Temporal Blood Data**

  * Physiology-aware filling
  * KNN refinement across cohort
  * Denoising LSTM encoder

* **Spatial Histopathology (WSI)**

  * Patch clustering (MiniBatch KMeans)
  * Positional bias injection (coordinate MLP)
  * Transformer aggregation + Monte-Carlo Dropout

* **Semantic Text**

  * ClinicalBERT or TF-IDF + SVD embeddings

All pipelines output **512-dimensional embeddings** per modality.

---

### 2️⃣ Advanced Cross-Modal Imputation (JAMIE-style VAE)

To handle **missing modalities**, HAN-MAP uses a **Joint Multimodal Variational Autoencoder**:

* Learns a shared latent space across modalities
* Uses cross-modal attention to synthesize missing embeddings
* Outputs both **imputed features** and **uncertainty estimates**
* Iteratively refined using Transformer layers

This ensures robust predictions even with incomplete patient data.

---

### 3️⃣ Hierarchical Cross-modal Attention Transformer (HCAT)

Key components:

* **Quality Gate** – dynamically down-weights uncertain or imputed modalities
* **Modality Positional Encoding** – preserves modality identity
* **Local Branch Transformers**

  * Clinical ↔ Temporal
  * Pathological ↔ Spatial
* **Global Transformer Encoder** – holistic patient fusion
* **Task-Specific Attention Routing**

  * Separate heads for Survival & Recurrence

---

## 🎯 Prediction Tasks

HAN-MAP performs two binary classification tasks:

| Task              | Description                        |
| ----------------- | ---------------------------------- |
| 5-Year Survival   | Predict long-term patient survival |
| 2-Year Recurrence | Predict short-term cancer relapse  |

Loss Functions:

* Focal Loss (class imbalance)
* VAE KL + Reconstruction Loss
* Contrastive InfoNCE Loss

---

## 📊 Results

| Task              | Best F1-score |
| ----------------- | ------------- |
| 5-Year Survival   | **0.80**      |
| 2-Year Recurrence | **0.95**      |
| **Average**       | **0.875**     |

The system demonstrates excellent generalization and robustness on sparse clinical data.

---

## 🛠️ Tech Stack

* **Language**: Python 3.9+
* **Frameworks**: PyTorch, scikit-learn
* **Libraries**:

  * NumPy, Pandas, h5py
  * Transformers (HuggingFace)
  * TorchVision
* **Optional**: Docker for deployment

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
# Install dependencies
pip install -r requirements.txt

# Train model
python training/train_hcat.py

# Run inference
python inference/predict.py --input features.h5
```

---

## 🔒 Ethics & Data Privacy

* Designed with **HIPAA/GDPR compliance** in mind
* Supports encrypted storage & controlled access
* Intended strictly for **research & clinical decision support**, not autonomous diagnosis

---

## 🌍 Sustainable Development Goals (SDGs)

* **SDG 3** – Good Health & Well-being
* **SDG 9** – Industry, Innovation & Infrastructure
* **SDG 10** – Reduced Inequalities
* **SDG 17** – Partnerships for the Goals

---

## 🔮 Future Work

* End-to-end learning from **raw WSI images**
* Integration of **genomics / proteomics** data
* Explainable AI dashboards for clinicians
* External validation on global oncology cohorts

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

This project is released for **academic and research use only**.
Commercial usage requires explicit permission.

---

⭐ If you find this project useful, consider starring the repository!

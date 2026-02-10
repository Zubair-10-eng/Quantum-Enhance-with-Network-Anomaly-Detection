


# Quantum Feature Enhancement for Network Anomaly Detection  
**Task-Adaptive Quantum Feature Enhancement with Kernel Target Alignment (KTA)**  

*Hybrid Quantum–Classical Learning Framework*

---

## 📌 Overview

This project presents a **hybrid quantum–classical network anomaly detection framework** that integrates **fixed and trainable ZZ quantum feature maps** into high-performance classical learning pipelines. The system systematically evaluates **geometry-dependent quantum advantage** across two complementary cybersecurity benchmarks:

- **SNT Dataset (Structured Network Traffic)** - Synthetic network traffic with labeled anomalies  
- **CICIDS-2017 Dataset** - Real-world intrusion detection benchmark from Canadian Institute for Cybersecurity  

A **Kernel Target Alignment (KTA)** optimization strategy is used to train quantum feature maps that explicitly maximize class separability in the quantum-induced feature space, enabling task-adaptive geometric transformations that improve robustness and discriminative power.

---

## 🔗 Dataset Downloads

### SNT Dataset (Structured Network Traffic)
**Kaggle Download:**  
[https://www.kaggle.com/datasets/sntnetwork/snt-dataset](https://www.kaggle.com/datasets/sntnetwork/snt-dataset)

### CICIDS-2017 Dataset (Canadian Institute for Cybersecurity)
**Official Source:**  
[https://www.unb.ca/cic/datasets/ids-2017.html](https://www.unb.ca/cic/datasets/ids-2017.html)

---

## 🧠 Key Contributions

- 128-parameter **Trainable ZZ Quantum Feature Map** optimized via KTA
- Scalable **hybrid quantum–classical pipeline** using 8-qubit embeddings
- Dataset geometry analysis (raw vs PCA-reduced features)
- Gaussian noise robustness benchmarking up to 70%
- 300 statistically independent model evaluations across stratified subsets

---

## 🏗️ System Architecture
Raw / PCA Features
↓
Quantum Feature Maps (8-Qubit Circuit)
├── Fixed ZZ Embedding
└── Trainable ZZ (KTA-Optimized)
↓
16-D Quantum Feature Vector
↓
Classical Classifier
├── XGBoost
├── Random Forest
└── SVM (RBF)
↓
Accuracy · F1-Score · KTA · Noise Robustness



---

## 📊 Dataset Protocol

**Evaluation Design**
- 50,000 samples per dataset (SNT + CICIDS-2017)
- 5 stratified subsets per dataset (10,000 samples each)
- 70/30 train-test split per subset
- 3 classifiers × 3 feature types × 10 subsets = **300 total evaluations**

---

## ⚙️ Preprocessing Pipeline

- Remove NaN and infinite values
- Classical normalization: StandardScaler
- Quantum encoding: Feature scaling to [0, 2π]
- Dual regime evaluation: Raw features and PCA (8 components, 70–90% variance)
- Class imbalance handling via `scale_pos_weight` (XGBoost)

---

## 🧪 Quantum Feature Maps

### Fixed ZZ Feature Map
- 8-qubit ring entanglement topology
- 2-layer circuit depth
- No trainable parameters
- Baseline quantum kernel representation

### Trainable ZZ Feature Map
- 128 learnable parameters
- Trainable single-qubit rotations
- Bilinear entanglement terms
- KTA-optimized task-adaptive geometry
Θij(x) = aij xi xj + bij xi + cij xj + dij

text

---

## 📐 Kernel Target Alignment (KTA)
KTA(K, Y) = <K,YYᵀ> / (||K||F ||YYᵀ||F)



## 🏆 Classifiers

| Classifier | Configuration |
|------------|---------------|
| XGBoost | 200 trees · max depth = 5 · learning rate = 0.05 |
| Random Forest | 150 trees · max depth = 10 |
| SVM (RBF) | C = 1.0 |

---


---

## 🚀 Future Work

- Deployment on NISQ hardware
- One-class quantum anomaly detection
- Multi-class intrusion detection
- Fidelity-based quantum kernels

---

## 📬 Contact

**Author:** [Mohd Zubair Khan, Dr.Rajendra Hegadi]  
**Email:** [2bec027@iiitdwd.ac.in, rajendra.hegadi@gmail.com] 



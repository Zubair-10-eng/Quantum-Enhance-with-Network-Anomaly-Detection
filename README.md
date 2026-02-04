


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

text

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
KTA(K, Y) = <K, YYᵀ> / (||K||F ||YYᵀ||F)

text

- **Optimizer:** Adam
- **Learning Rate:** 0.05
- **Epochs:** 15
- **Calibration Set:** 80 samples per subset

---

## 🏆 Classifiers

| Classifier | Configuration |
|------------|---------------|
| XGBoost | 200 trees · max depth = 5 · learning rate = 0.05 |
| Random Forest | 150 trees · max depth = 10 |
| SVM (RBF) | C = 1.0 |

---

## 📊 Experimental Results — Full Tables

### SNT Dataset — Raw Features

#### Mean Classification Performance

##### Random Forest
| Model | Accuracy | F1-Score |
|-------|----------|----------|
| RF-Classical | 0.9999 ± 0.0003 | 0.9999 ± 0.0003 |
| RF-Fixed-ZZ | 0.9829 ± 0.0023 | 0.9829 ± 0.0021 |
| **RF-Trainable-ZZ** | **1.0000 ± 0.0000** | **1.0000 ± 0.0000** |

##### XGBoost
| Model | Accuracy | F1-Score |
|-------|----------|----------|
| XGB-Classical | 1.0000 ± 0.0000 | 1.0000 ± 0.0000 |
| XGB-Fixed-ZZ | 0.9933 ± 0.0023 | 0.9933 ± 0.0023 |
| **XGB-Trainable-ZZ** | **0.9999 ± 0.0001** | **0.9999 ± 0.0002** |

##### SVM
| Model | Accuracy | F1-Score |
|-------|----------|----------|
| SVM-Classical | 0.9999 ± 0.0003 | 0.9999 ± 0.0003 |
| SVM-Fixed-ZZ | 0.9407 ± 0.0049 | 0.9429 ± 0.0045 |
| **SVM-Trainable-ZZ** | **1.0000 ± 0.0000** | **1.0000 ± 0.0000** |

#### Kernel Target Alignment (KTA)

| Subset | Classical | Fixed ZZ | Trainable ZZ | Gain |
|--------|-----------|----------|--------------|------|
| 1 | 0.2571 | 0.1349 | **0.7437** | +189% |
| 2 | 0.3016 | 0.1951 | **0.7442** | +147% |
| 3 | 0.0001 | 0.1400 | **0.7706** | +793% |
| 4 | 0.2853 | 0.1897 | **0.7311** | +156% |
| 5 | 0.2434 | 0.1700 | **0.6912** | +184% |

#### Noise Robustness (Accuracy)

| Noise % | Classical | Fixed ZZ | Trainable ZZ |
|---------|-----------|----------|--------------|
| 0 | 1.0000 | 0.9923 | **1.0000** |
| 5 | 0.9717 | 0.5677 | **0.9960** |
| 10 | 0.9720 | 0.5390 | **0.9880** |
| 20 | 0.9487 | 0.5320 | **0.9600** |
| 30 | 0.9267 | 0.5150 | **0.9247** |

---

### SNT Dataset — PCA (8 Components)

#### Mean Classification Performance

| Model | Accuracy | F1-Score |
|-------|----------|----------|
| RF-Classical | 0.9993 | 0.9993 |
| RF-Fixed-ZZ | 0.9921 | 0.9919 |
| **RF-Trainable-ZZ** | **0.9983** | **0.9983** |
| XGB-Classical | 0.9993 | 0.9993 |
| XGB-Fixed-ZZ | 0.9947 | 0.9946 |
| **XGB-Trainable-ZZ** | **0.9977** | **0.9976** |
| SVM-Classical | 0.9986 | 0.9986 |
| SVM-Fixed-ZZ | 0.9915 | 0.9914 |
| **SVM-Trainable-ZZ** | **0.9973** | **0.9972** |

#### Mean Kernel Target Alignment

| Kernel | Mean KTA | Improvement |
|--------|----------|-------------|
| Classical (RBF) | 0.2093 | — |
| Fixed ZZ | 0.1698 | -18.9% |
| **Trainable ZZ** | **0.5896** | **+181.7%** |

#### Noise Robustness (XGBoost Accuracy)

| Noise % | Classical | Fixed ZZ | Trainable ZZ |
|---------|-----------|----------|--------------|
| 0 | 1.0000 | 0.9977 | **0.9983** |
| 10 | 0.9713 | 0.9580 | **0.9883** |
| 30 | 0.8980 | 0.8010 | **0.9320** |
| 70 | 0.7827 | 0.6317 | **0.8137** |

---

### CICIDS-2017 — Raw Features

#### Mean Classification Performance (XGBoost)

| Model | Accuracy | F1-Score |
|-------|----------|----------|
| **Classical** | **0.9955** | **0.9908** |
| Fixed ZZ | 0.9623 | 0.9265 |
| Trainable ZZ | 0.9861 | 0.9716 |

#### Kernel Target Alignment

| Subset | Classical | Fixed ZZ | Trainable ZZ |
|--------|-----------|----------|--------------|
| 1 | **0.3495** | 0.2339 | 0.2119 |
| 2 | **0.3219** | 0.2386 | 0.2847 |
| 3 | **0.3847** | 0.3068 | 0.3335 |
| 4 | **0.3380** | 0.2354 | 0.2492 |
| 5 | **0.3196** | 0.2476 | 0.2466 |

#### Noise Robustness (Accuracy)

| Noise % | Classical | Fixed ZZ | Trainable ZZ |
|---------|-----------|----------|--------------|
| 5 | **0.8243** | 0.8120 | 0.8110 |
| 20 | **0.8140** | 0.7733 | 0.7457 |
| 50 | **0.7940** | 0.7470 | 0.7057 |

---

### CICIDS-2017 — PCA (8 Components)

#### Mean Kernel Target Alignment

| Kernel | Mean KTA | Improvement |
|--------|----------|-------------|
| **Classical (RBF)** | **0.3914** | — |
| Fixed ZZ | 0.3417 | -12.7% |
| Trainable ZZ | 0.3757 | -4.0% |

#### Noise Robustness (XGBoost Accuracy)

| Noise % | Classical | Fixed ZZ | Trainable ZZ |
|---------|-----------|----------|--------------|
| 0 | **0.9880** | 0.9857 | 0.9880 |
| 20 | **0.8460** | 0.8067 | 0.8453 |
| 50 | 0.7923 | 0.7300 | **0.7900** |
| 70 | 0.7823 | 0.7060 | **0.7590** |

---

## ⚠️ Limitations

- Quantum circuits evaluated on noiseless simulators
- Binary classification only
- 8-qubit topology limits kernel expressivity

---

## 🚀 Future Work

- Deployment on NISQ hardware
- One-class quantum anomaly detection
- Quantum autoencoders
- Multi-class intrusion detection
- Fidelity-based quantum kernels

---

**Quantum Feature Enhancement for Network Anomaly Detection**  
*Hybrid Quantum–Classical Learning Framework*

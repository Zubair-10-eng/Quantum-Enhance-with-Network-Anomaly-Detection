## Task-Adaptive Quantum Feature Enhancement for Network Anomaly Detection  
**Hybrid Quantum–Classical Learning with Kernel Target Alignment (KTA)**

### Overview

This project presents a **hybrid quantum–classical network anomaly detection framework** that integrates **fixed and trainable ZZ quantum feature maps** into classical machine learning pipelines.

The framework:

- **Embeds** preprocessed network traffic features into an **8-qubit quantum circuit**.
- Uses both **fixed** and **trainable** ZZ feature maps.
- Optimizes the **trainable feature map geometry** via **Kernel Target Alignment (KTA)** to maximize class separability.
- Benchmarks across two complementary intrusion detection datasets:
  - **SNT Dataset** (Structured Network Traffic)
  - **CICIDS-2017** (Canadian Institute for Cybersecurity)

The main objective is to study **geometry-dependent quantum advantage** for anomaly detection under realistic constraints (limited qubits, noise, dataset geometry).

---

### Datasets

- **SNT Dataset (Structured Network Traffic)**  
  Kaggle: `https://www.kaggle.com/datasets/sntnetwork/snt-dataset`

- **CICIDS-2017 (Intrusion Detection)**  
  Official site: `https://www.unb.ca/cic/datasets/ids-2017.html`

Both datasets are downsampled and stratified to build comparable evaluation protocols for classical and quantum-enhanced models.

---

### Repository Structure

- `trainable-zz-(CICDS without PCA).ipynb` – Hybrid quantum–classical pipeline on **CICIDS-2017 raw features**.
- `trainable-zz-feature(SNT without PCA).ipynb` – Hybrid pipeline on **SNT raw features**.
- `ZZ_trainalbe(CICDS With PCA).ipynb` – Hybrid pipeline on **CICIDS-2017 with PCA (8 components)**.
- `ZZ_trainalbe(SNT With PCA).ipynb` – Hybrid pipeline on **SNT with PCA (8 components)**.

Each notebook implements:

- Data loading and preprocessing.
- Quantum feature map construction (fixed vs trainable ZZ).
- KTA-based optimization of quantum circuit parameters.
- Classical classifier training and evaluation.
- Noise robustness and KTA analysis.

---

### System Architecture

1. **Input Features**
   - Raw features or PCA-reduced (8 components).
2. **Quantum Feature Maps (8 Qubits)**
   - **Fixed ZZ embedding**:
     - 8-qubit ring entanglement.
     - 2-layer circuit depth.
     - No trainable parameters.
   - **Trainable ZZ feature map**:
     - 128 learnable parameters.
     - Trainable single-qubit rotations and bilinear entanglement terms.
     - Parameters learned with **KTA** on a calibration set.
3. **Quantum Feature Vector**
   - 16-dimensional quantum feature vector extracted from the circuit.
4. **Classical Classifiers**
   - **XGBoost**
   - **Random Forest**
   - **SVM (RBF)**
5. **Evaluation Metrics**
   - Accuracy
   - F1-score
   - Kernel Target Alignment (KTA)
   - Noise robustness under Gaussian input noise.

---

### Preprocessing Pipeline

- Remove NaN and infinite values.
- Normalize features using `StandardScaler`.
- Scale features to \([0, 2\pi]\) for quantum encoding.
- Evaluate in two regimes:
  - **Raw features**
  - **PCA (8 components)** capturing ~70–90% variance.
- Handle class imbalance via `scale_pos_weight` in XGBoost.

---

### Quantum Feature Maps

**Fixed ZZ Feature Map**

- 8-qubit ring entanglement.
- 2-layer depth.
- No trainable parameters.
- Baseline quantum kernel representation.

**Trainable ZZ Feature Map**

- 128 trainable parameters.
- Single-qubit and bilinear entangling terms.
- **Task-adaptive geometry** learned by maximizing KTA.

The feature map parameterization:

\[
\Theta_{ij}(x) = a_{ij} x_i x_j + b_{ij} x_i + c_{ij} x_j + d_{ij}
\]

Parameters \(\{a_{ij}, b_{ij}, c_{ij}, d_{ij}\}\) are optimized to align the quantum kernel with the label structure.

---

### Kernel Target Alignment (KTA)

For a kernel matrix \(K\) and label matrix \(YY^\top\):

\[
\text{KTA}(K, Y) = \frac{\langle K, YY^\top \rangle}{\|K\|_F \, \|YY^\top\|_F}
\]

- **Optimizer**: Adam  
- **Learning rate**: 0.05  
- **Epochs**: 15  
- **Calibration set**: 80 labeled samples per subset  

The KTA objective drives the quantum feature map to produce kernels that are geometrically aligned with the underlying class structure.

---

### Evaluation Protocol

- **50,000 samples per dataset** (SNT and CICIDS-2017).
- **5 stratified subsets** per dataset (10,000 samples each).
- Per subset:
  - **70/30 train–test split**.
  - Models trained independently.
- **Configurations**:
  - 3 classifiers (XGBoost, Random Forest, SVM).
  - 3 feature types (classical, fixed ZZ, trainable ZZ).
  - 10 total subsets (2 datasets × 5 subsets).
- **Total**: 300+ evaluations including repeated runs and noise sweeps.

---

### Classifier Configurations

- **XGBoost**
  - 200 trees
  - `max_depth = 5`
  - `learning_rate = 0.05`
  - `scale_pos_weight` for imbalance.

- **Random Forest**
  - 150 trees
  - `max_depth = 10`

- **SVM (RBF)**
  - `C = 1.0`

---

### Key Results (High-Level)

- On **SNT (raw and PCA)**, the **trainable ZZ feature map**:
  - Matches or slightly trails the best classical baselines in accuracy/F1.
  - Achieves **large KTA improvements** (up to ~+180–790% vs classical).
  - Provides **superior noise robustness**, especially at medium-to-high noise levels.

- On **CICIDS-2017 (raw)**:
  - Classical XGBoost remains strongest in accuracy and KTA.
  - Quantum feature maps (fixed and trainable) underperform classical kernels on this higher-dimensional raw space.

- On **CICIDS-2017 (PCA)**:
  - **Trainable ZZ** is competitive with classical kernels.
  - Shows **slight robustness advantages** at higher noise levels (50–70%).

---

### Limitations

- Experiments run on **noiseless quantum simulators** (no hardware noise).
- **Binary classification** setting only.
- **8-qubit topology** limits kernel expressivity and possible quantum advantage.
- Quantum preprocessing can be more computationally expensive than purely classical approaches.

---

### Future Work

- Deployment and benchmarking on **real NISQ hardware**.
- **One-class** quantum anomaly detection.
- **Quantum autoencoders** for unsupervised detection.
- **Multi-class** intrusion detection.
- Exploration of **fidelity-based quantum kernels** and richer circuit geometries.
- Scaling to **more qubits** and deeper circuits with hardware-aware noise mitigation.

---

### Citation (Placeholder)

If you use this work or its ideas, please cite:

```bibtex
@misc{qml_network_anomaly_detection,
  title        = {Task-Adaptive Quantum Feature Enhancement for Network Anomaly Detection},
  author       = {Your Name},
  year         = {2026},
  note         = {Hybrid quantum--classical learning with KTA-optimized ZZ feature maps}
}
```

Replace `Your Name` and metadata with the final publication details once available.


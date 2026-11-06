# QML-Hackathon
an attempt to build a framewrok of QML to predict the crystals 

**Perovskite Energy Prediction: ML & VQE Quantum Approach** 

Combining Machine Learning (Random Forest) and Variational Quantum Eigensolver (VQE) for perovskite material formation energy prediction and ground-state energy analysis.

---

## Overview
This project focuses on material property analysis and energy prediction using the **Matbench Perovskites Dataset**:
1. **Machine Learning (ML)**: Utilizes `matminer` for materials feature engineering combined with `RandomForestRegressor` to benchmark the predictive performance of structural, chemical, and combined feature sets on formation energy ($e\_form$).
2. **Quantum Computing (VQE)**: Leverages `PennyLane` to construct a variational quantum circuit, solving for the ground-state energy of a 2-qubit Hamiltonian via the COBYLA optimizer and verifying its numerical precision.

---

## Packages & Prerequisites

The following Python packages are required to run this project. You can install them directly in Google Colab or your local Python environment:

### Installation
```bash
pip install matminer pennylane scikit-learn pandas numpy scipy matplotlib
```

### Core Package List

* **Materials Data & Feature Extraction**:
  * `matminer`: Used for loading the Matbench material dataset and extracting chemical/structural features.
* **Quantum Computing & Simulation**:
  * `PennyLane`: Used for constructing Variational Quantum Circuits (VQC) and executing VQE simulations.
* **Machine Learning & Scientific Computing**:
  * `scikit-learn`: Provides `RandomForestRegressor` baseline models and performance evaluation metrics.
  * `SciPy`: Provides `scipy.optimize.minimize` (COBYLA algorithm) for VQE parameter optimization.
  * `NumPy` & `Pandas`: Data processing, feature matrix construction, and statistical analysis.
* **Data Visualization**:
  * `Matplotlib` / `Seaborn`: Plotting predicted vs. actual scatter plots and VQE energy convergence curves.

---

### Workflow & Steps

1. **Environment Setup**
   * Installed and imported essential packages for cross-domain analysis spanning materials science, quantum simulation, and machine learning.
2. **Data Loading & EDA**
   * Loaded the Matbench Perovskites dataset (18,928 total entries).
   * Inspected core attributes including crystal structure (`structure`), formation energy (`e_form`), and physical/chemical properties (composition, electronegativity, lattice parameters, volume, density).
3. **Feature Engineering & Initial Modeling**
   * Sampled 1,000 structures as a prototype dataset for rapid experimentation.
   * Built an `extract_features` function to capture lattice parameters, chemical properties, and atomic distances.
   * Trained a baseline `RandomForestRegressor` to predict formation energy ($\text{MAE} \approx 0.526$, $R^2 \approx 0.31$) and generated predicted vs. actual scatter plots.
4. **Quantum Computing: VQE Ground State Search**
   * Defined a 2-qubit Hamiltonian and built a PennyLane variational circuit.
   * Optimized circuit parameters via `scipy.optimize.minimize` (COBYLA algorithm).
   * Estimated ground-state energy ($-1.529705850$), which matched exact diagonalization ($-1.529705854$) with an error on the order of $10^{-9}$; plotted convergence curves.
5. **Feature Group Benchmarking**
   * Analyzed physical insights: single geometric parameters (e.g., nearest-neighbor distance) are insufficient to determine formation energy without chemical composition.
   * Categorized features into three groups:
     1. **Structural Features**: Lattice constants, cell volume, nearest-neighbor distance.
     2. **Chemical Features**: Mean atomic number, mean/delta electronegativity, mean atomic radius.
     3. **Combined Features**: Fusion of structural and chemical features.
   * Benchmarked three Random Forest models across groups; results confirmed that the **Combined** feature set yields the highest predictive performance.



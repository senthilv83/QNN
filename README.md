# Quantum Neural Networks for High-Dimensional Genomic Pattern Detection in Personalized Medicine

[![Quantum Framework: PennyLane](https://img.shields.io/badge/Quantum-PennyLane-blueviolet)](https://pennylane.ai/)
[![Framework: PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-ee4c2c.svg)](https://pytorch.org/)
[![Bioinformatics](https://img.shields.io/badge/Genomics-Personalized%20Medicine-green)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 🚀 Overview

This repository hosts a cutting-edge framework utilizing **Quantum Neural Networks (QNNs)** to analyze genomic data for personalized medicine. With the rapid expansion of genetic sequencing, this project tackles the high-dimensional complexity of genomic pattern recognition, an area where classical neural networks often face computational bottlenecks.

Designed by **Senthilkumar Vijayakumar** (IEEE Senior Member).

## 🧠 Technical Deep Dive

By leveraging the principles of quantum computation, this QNN model is designed to detect intricate and subtle patterns across massive arrays of genetic variants. These quantum-enhanced capabilities allow for highly optimized predictions related to:
*   **Disease Risk Prediction:** Identifying multi-gene interactions that elevate susceptibility to specific conditions.
*   **Drug Response Modeling:** Forecasting how individuals will respond to pharmacological treatments based on their unique genomic signatures.
*   **Optimal Treatment Pathways:** Assisting in the formulation of hyper-personalized therapeutic strategies.

### Architecture & Tech Stack
*   **Quantum Backend:** Built using [PennyLane](https://pennylane.ai/) for seamless integration of quantum circuits into classical machine learning workflows.
*   **Classical Deep Learning:** [PyTorch](https://pytorch.org/) handles classical preprocessing and hybrid optimization layers.
*   **Optimization:** Integration with Scikit-learn and OpenVINO for fast, scalable inference and classical-quantum hybrid training loops.


## ⚙️ Technical Architecture & Pipeline

This repository implements a sophisticated data pipeline that blends classical machine learning optimizations with advanced high-dimensional pattern recognition for genomic arrays (Single Nucleotide Polymorphisms - SNPs).

### 1. Genomic Data Ingestion & Preprocessing
*   **High-Dimensional Parsing:** Processes raw genetic variant data (SNPs) via `pandas` and `numpy`, robustly handling malformed sequences and missing values.
*   **Dimensionality Reduction:** Employs **Principal Component Analysis (PCA)** (`scikit-learn`) to distill the genetic data, maintaining a 99% explained variance threshold. This critically reduces the feature space complexity required for neural network processing.
*   **Data Standardization:** Applies `StandardScaler` to normalize the reduced genomic features, ensuring stable gradient flow during network optimization.

### 2. Hybrid Neural Network Optimization
*   **PyTorch Deep Learning:** Constructs a tailored neural network architecture designed to classify disease risks based on the processed genomic arrays.
*   **Hyperparameter Tuning:** Utilizes `skorch` alongside `GridSearchCV` to bridge PyTorch with Scikit-learn's ecosystem, enabling automated cross-validation and hyperparameter optimization.
*   **Hardware Acceleration:** Implements PyTorch Automatic Mixed Precision (AMP) via `GradScaler` and `autocast` to maximize training throughput on available GPUs.

### 3. Edge-Optimized Inference & Deployment
*   **ONNX Export:** Translates the optimized PyTorch model into an Open Neural Network Exchange (ONNX) format, decoupling the model from its training environment.
*   **OpenVINO Integration:** Leverages Intel's **OpenVINO** (`openvino.runtime`) toolkit to compile and deploy the ONNX model, drastically reducing inference latency for real-world clinical applications on edge devices and CPUs.
*   **Quantum Extensibility:** The environment is pre-configured with **PennyLane** to support hybrid Quantum-Classical layers (QNNs) designed to evaluate classically intractable genomic state-spaces.

## 📂 Repository Structure
*   `QNNGPD.ipynb`: The primary Jupyter Notebook containing the full implementation of the **Q**uantum **N**eural **N**etwork for **G**enomic **P**attern **D**etection (QNNGPD).

## 🛠️ Getting Started

Ensure you have Python 3.12+ and the following critical dependencies installed:
```bash
pip install pennylane torch scikit-learn openvino-dev pandas numpy
```

Run the `QNNGPD.ipynb` notebook to see the hybrid quantum-classical pipeline in action.

## 🤝 Contributing
We welcome contributions in the fields of Quantum Machine Learning (QML) and Bioinformatics. Please open an issue or submit a pull request!

## 📝 Citation

If you utilize this framework or code in your research, please use the following citation:

```bibtex
@software{Vijayakumar_QNN_Genomics_2026,
  author = {Vijayakumar, Senthilkumar},
  title = {Quantum Neural Networks for High-Dimensional Genomic Pattern Detection in Personalized Medicine},
  year = {2026},
  url = {https://github.com/senthilv83/QNN},
  orcid = {0009-0009-6436-9003}
}
```
*(See `CITATION.cff` for more details).*

## 📓 Notebook Cell-by-Cell Technical Walkthrough (`QNNGPD.ipynb`)

### Cells 1-3: Project Initialization & Motivation
*   **Overview:** Sets up the interactive environment and introduces the conceptual framework of Quantum Neural Networks (QNNs) for Genomic Pattern Detection.
*   **Focus:** Highlights the necessity of using QNNs to overcome classical computing bottlenecks when processing high-dimensional genetic variants for personalized medicine.

### Cell 4: Environment Setup & Dependencies
*   **Package Installation:** Installs a robust stack of Machine Learning, Deep Learning, and Quantum computation libraries.
*   **Key Libraries:** `pennylane` (Quantum circuits), `torch` (Deep Learning), `scikit-learn` & `skorch` (Classical ML and tuning), `openvino-dev` & `onnx` (Model compilation and edge inference), `pandas` & `numpy` (Data manipulation).

### Cell 5: Genomic Data Ingestion
*   **Data Loading:** Uses `pandas` to read the genomic dataset (e.g., `a.csv`).
*   **Error Handling:** Implements `on_bad_lines='skip'` to robustly bypass malformed genomic sequence rows, ensuring continuous pipeline execution without crashing.

### Cell 6: Data Standardization
*   **Feature Scaling:** Applies Scikit-learn's `StandardScaler` to normalize the raw genetic features.
*   **Statistical Importance:** Forces zero mean and unit variance across the dataset, which is a strict mathematical prerequisite for the stability and convergence speed of gradient descent in the neural network.

### Cell 7: Dimensionality Reduction (PCA)
*   **Principal Component Analysis:** Fits and applies PCA to the normalized dataset.
*   **Variance Retention:** Configured with a strict `0.99` threshold to retain 99% of the explained variance while aggressively discarding noise.
*   **Optimization Strategy:** Radically reduces the input vector size, making subsequent quantum and classical computations mathematically tractable and memory-efficient.

### Cell 8: Neural Network Architecture & Data Splitting
*   **Train/Test Split:** Partitions the reduced genomic dataset into training and out-of-sample testing sets.
*   **PyTorch Model (`SNPClassifier`):** Defines a feed-forward Deep Neural Network using `nn.Sequential`.
*   **Layer Composition:** Utilizes `Linear` fully connected layers, `ReLU` activations for non-linearity, `Dropout` for regularization (preventing overfitting on sparse genomic data), and `Sigmoid` for binary classification outputs (e.g., disease risk prediction).

### Cell 9: Hyperparameter Tuning (GridSearchCV & Skorch)
*   **Skorch Wrapper:** Wraps the PyTorch `SNPClassifier` into a `NeuralNetClassifier`, establishing direct compatibility with the Scikit-learn API.
*   **Grid Search:** Iterates through arrays of hyperparameters (e.g., learning rates, epochs, dropout rates) using `GridSearchCV`.
*   **Automated Cross-Validation:** Programmatically identifies the most optimal architectural weights and learning configurations tailored to the specific genomic dataset.

### Cell 10: Hardware-Accelerated Training (AMP)
*   **Automatic Mixed Precision (AMP):** Utilizes `torch.cuda.amp.GradScaler` and `autocast`.
*   **Execution Efficiency:** Dynamically casts specific tensor operations to lower-precision floats (FP16), vastly accelerating matrix multiplications on modern GPUs while preserving FP32 precision for sensitive gradient updates.

### Cell 11: ONNX Model Export
*   **Model Serialization:** Exports the fine-tuned, optimal PyTorch model to the Open Neural Network Exchange (`.onnx`) format via `torch.onnx.export`.
*   **System Interoperability:** Decouples the underlying model weights from the PyTorch ecosystem, allowing it to be natively ingested by cross-platform inference engines.

### Cell 12: OpenVINO Edge Deployment
*   **Intel OpenVINO Core:** Initializes the OpenVINO hardware-aware runtime environment.
*   **Model Compilation:** Loads and compiles the serialized `.onnx` model (`core.compile_model`), specifically optimizing its graph for the target hardware architecture (e.g., CPU, integrated GPU).
*   **Clinical Application:** Demonstrates the final phase: deploying a computationally heavy genomic model for ultra-low latency, localized inference on edge devices (simulating real-world clinical or laboratory settings).

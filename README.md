# DL_final


# Comparing Vision Transformers and CNNs under Resource-Constrained Image Classification

## Overview

This project investigates the performance tradeoffs between **Convolutional Neural Networks (CNNs)** and **Vision Transformers (ViTs)** under **resource-constrained and low-data image classification settings**.
We systematically compare representative lightweight CNN and ViT architectures in terms of **accuracy, model size, computational cost (FLOPs), and inference latency**.

The goal is to understand **when CNNs or Vision Transformers are more suitable** for deployment under limited data and compute budgets.

---

## Models

We evaluate the following lightweight architectures:

### CNNs

* **ResNet-18**
* **EfficientNet-B0**

### Vision Transformers

* **ViT-Tiny (patch16, 224)**
* **DeiT-Tiny (patch16, 224)**

All models are trained using identical optimization settings to ensure a fair comparison.

---

## Datasets

Experiments are conducted on two benchmark datasets:

* **CIFAR-100**

  * 100 classes
  * Original resolution: 32×32 (resized to 224×224)
* **Tiny-ImageNet-200**

  * 200 classes
  * Resolution: 64×64 (resized to 224×224)

To simulate data scarcity, we train models using **three data fractions**:

* **10%** (extreme low-data)
* **25%** (moderate low-data)
* **50%** (relatively sufficient but constrained)

---

## Experimental Setup

* Input resolution: **224×224**
* Optimizer: **AdamW**
* Learning rate: **3e-4**
* Weight decay: **0.05**
* Batch size: **128**
* Training epochs: **20**
* Mixed-precision training (AMP) enabled
* Same data augmentation and preprocessing across all models

All experiments are run with a fixed random seed for reproducibility.

---

## Evaluation Metrics

We report the following metrics for each model and setting:

* **Top-1 classification accuracy**
* **Number of parameters**
* **FLOPs** (floating-point operations)
* **Inference latency** (measured with batch size = 1)

The analysis focuses on the **accuracy–cost tradeoff**, rather than accuracy alone.

---

## Results Summary

Key findings from the experiments include:

* On **CIFAR-100**, Vision Transformers achieve higher accuracy than CNNs even under limited data, offering a strong accuracy–compute tradeoff.
* On **Tiny-ImageNet**, CNNs (especially EfficientNet-B0) demonstrate superior robustness and resource efficiency in low-data regimes.
* FLOPs do not fully reflect inference efficiency; models with lower FLOPs may still incur higher latency due to architectural characteristics.

These results indicate that **no single architecture dominates across all settings**, and the optimal choice depends on dataset complexity, data availability, and deployment constraints.

---

## Visualizations

The project includes:

* Accuracy vs. data fraction plots
* Accuracy vs. FLOPs tradeoff plots
* Accuracy vs. inference latency tradeoff plots

These visualizations illustrate how model performance changes across data regimes and resource constraints.

---

## Files

* `vit_vs_cnn_full_experiment_results.csv`
  Contains all experimental results, including accuracy and resource metrics.

* `notebook.ipynb`
  Colab notebook used to run experiments and generate figures.

---

## How to Run

1. Install dependencies:

   ```bash
   pip install timm ptflops
   ```
2. Download datasets:

   * CIFAR-100 will be downloaded automatically via torchvision.
   * Tiny-ImageNet can be downloaded via Kaggle (CLI or kagglehub).
3. Run the notebook cells sequentially to reproduce results.

---

## Conclusion

This study demonstrates that **Vision Transformers are not inherently unsuitable for low-data settings**, but their effectiveness strongly depends on dataset characteristics.
CNNs remain competitive and often preferable under stricter resource and data constraints, while ViTs can offer superior accuracy when computational budgets allow.

---


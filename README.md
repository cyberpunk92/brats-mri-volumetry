**Domain:** Neuro-Oncology | Medical Image Analysis (Computer Vision)  
**Objective:** Automated tumor sub-region localization and RANO-compliant surgical volumetry.

## 📌 Project Overview
This repository contains an end-to-end clinical deep learning pipeline engineered to segment brain tumors from multi-parametric MRI scans. Utilizing the BraTS 2020 dataset, the pipeline transitions from standard 2D image classification to complex spatial volumetry. A custom Attention U-Net isolates the necrotic core, peritumoral edema, and active enhancing tumor directly from four co-registered MRI modalities (FLAIR, T1-contrast, T1, and T2).

## 📁 Repository Structure
* `Brain_Tumor_Segmentation_Report.pdf`: Clinical evaluation report featuring multi-modal visual comparisons, voxel-level metrics, and anatomical volumetry output.
* `brats20_tumor_segmentation.ipynb`: The complete PyTorch pipeline, including NIfTI data ingestion, Z-score normalization, model architecture, compound loss implementation, and the surgical volumetry engine.
* `README.md`: Technical documentation.

## 🧠 Technical Highlights
* **Multi-Modal Normalization:** Voxel-specific Z-score intensity normalization restricted strictly to non-zero brain voxels.
* **Attention U-Net:** Spatial attention gates suppress healthy background tissue and focus gradients on complex tumor boundaries.
* **Compound Loss:** Hybrid formulation of Cross-Entropy and multi-class Soft Dice Loss mitigating extreme foreground-background class imbalance.
* **Clinical Volumetry Engine:** Derives physical tumor volume (cm³) directly from raw NIfTI voxel spacing to align with RANO 2.0 evaluation criteria.

## 📊 Baseline Performance
* **Whole Tumor (WT) Dice Score:** 0.906
* **Weighted F1-Score:** 0.987

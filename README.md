# Multi-Parametric MRI Brain Tumor Segmentation & Clinical Volumetry

This repository contains an end-to-end deep learning pipeline for automated brain tumor sub-region segmentation and quantitative surgical volumetry using the BraTS 2020 multi-parametric MRI dataset. The primary objective is to transition from standard 2D image classification to complex 3D spatial feature extraction, mitigating extreme foreground-background class imbalances to produce clinically actionable volumetric metrics compliant with RANO 2.0 assessment standards.

## Pipeline Architecture & Methodology

### Multi-Parametric Data Engineering
* **Modalities:** Simultaneous 4-channel input fusion utilizing co-registered FLAIR, T1-contrast (T1ce), T1, and T2 sequences.
* **Intensity Normalization:** Voxel-specific Z-score standardization strictly isolated to non-zero intracranial tissue, suppressing background scanner noise and non-biological acquisition artifacts.

### Attention U-Net Architecture (Spatial Gating)
* Built a custom encoder-decoder Attention U-Net from scratch in PyTorch.
* Incorporated spatial attention gates at each skip connection to dynamically suppress healthy anatomical background tissue while amplifying gradient flow along irregular, infiltrative tumor margins.
* Segmented three distinct pathological sub-regions: Necrotic Core (NCR), Peritumoral Edema (ED), and active Enhancing Tumor (ET).

### Imbalance-Aware Optimization & Loss Formulation
* **Compound Loss Function:** Hybrid objective combining multi-class Cross-Entropy with multi-label Soft Dice Loss to counteract severe spatial sparsity (tumor foreground voxels accounting for $<1\%$ of total volume).
* **Validation Performance:** Achieved a **0.9064 Whole Tumor (WT) Dice score** and a **0.9872 weighted average F1-score** across voxel-level evaluations.

### Automated Surgical Volumetry Engine
* Directly extracts affine voxel dimensions from raw NIfTI headers (`.nii`) to convert computational mask predictions into absolute physical volumes ($cm^3$).
* Automates volumetric tracking across sub-regions to supply the quantitative 3D measurements necessary for evaluating disease progression ($>40\%$ volume increase) and therapeutic response ($>65\%$ volume reduction) under RANO 2.0 oncology protocols.

## Repository Contents

* `brats20_tumor_segmentation.ipynb`: End-to-end PyTorch pipeline covering multi-modal data loading, Attention U-Net architecture, compound loss implementation, model inference, and the automated volumetry engine.
* `Brain_Tumor_Segmentation_Report.pdf`: Executive-grade clinical report detailing multi-parametric input alignments, ground truth comparisons, voxel classification tables, and calculated tumor loads.

## Live Interactive Code

The full experimental environment, including data processing, neural network training, and visual evaluation, can be executed directly on Kaggle: [View Kaggle Notebook](https://www.kaggle.com/)

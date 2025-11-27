# RA-UAMT: Residual Attention–based Uncertainty-Guided Mean Teacher for Semi-Supervised Breast Mass Segmentation

This repository contains the official implementation of our paper:

> **Residual attention based uncertainty-guided mean teacher model for semi-supervised breast masses segmentation in 2D ultrasonography**  
> M. U. Farooq, Z. Ullah, J. Gwak  
> *Computerized Medical Imaging and Graphics*, Vol. 104, 102173, 2023  
> [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0895611122001434) · [DOI: 10.1016/j.compmedimag.2022.102173](https://doi.org/10.1016/j.compmedimag.2022.102173)

---

<div align="center">

[![Journal](https://img.shields.io/badge/Journal-Computerized%20Medical%20Imaging%20and%20Graphics-2F4F4F.svg)](https://www.sciencedirect.com/science/article/pii/S0895611122001434)
[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.compmedimag.2022.102173-blue.svg)](https://doi.org/10.1016/j.compmedimag.2022.102173)
[![Year](https://img.shields.io/badge/Year-2023-lightgrey.svg)](https://doi.org/10.1016/j.compmedimag.2022.102173)
<!-- If you later put code on HF or a project page, you can add more badges here -->

</div>

---

<p align="center">
  <!-- Replace with your own architecture figure -->
  <img src="images/architecture.png" alt="Residual attention based uncertainty-guided mean teacher framework" width="80%">
</p>

---

## Table of Contents

- [Overview](#overview)
- [Method](#method)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
  - [Environment Setup](#environment-setup)
  - [Data Preparation](#data-preparation)
- [Training](#training)
- [Evaluation](#evaluation)
- [Results](#results)
- [Citation](#citation)
- [Acknowledgements](#acknowledgements)

---

## Overview

Breast ultrasound segmentation is challenging due to low contrast, fuzzy lesion boundaries, and large variations in mass shape and size. At the same time, high-quality pixel-wise annotations are scarce and expensive to obtain.

Our work proposes a **semi-supervised mean teacher framework** that:

- Uses a **residual attention U-Net** backbone to enhance feature extraction and focus on lesion regions.
- Incorporates **uncertainty estimation** to weight the consistency loss on unlabeled images.
- Exploits both **labeled and unlabeled ultrasound images** to improve segmentation performance on BUSI and UDIAT datasets.

The proposed model achieves competitive or superior performance to fully supervised and existing semi-supervised methods while using significantly fewer labeled samples.

---

## Method

The framework follows a standard teacher–student paradigm with three key components:

1. **Residual Attention Backbone**  
   - Residual blocks facilitate gradient flow and stabilize training of deeper networks.  
   - Attention modules highlight informative spatial regions corresponding to breast lesions.

2. **Mean Teacher with Consistency Regularization**  
   - A teacher network is updated as the exponential moving average (EMA) of the student.  
   - Consistency losses encourage the student predictions to match the teacher under different perturbations.

3. **Uncertainty-Guided Weighting**  
   - Pixel-wise uncertainty maps are estimated from the teacher predictions.  
   - Unreliable regions receive lower weight in the consistency loss, reducing the effect of noisy pseudo-labels from unlabeled images.

(See the paper for full mathematical details and ablation studies.)

---

## Repository Structure

> **Note:** Adjust this section to match your actual folder structure.

```text
.
├── configs/                 # YAML or JSON configuration files
├── data/                    # Dataset splits / CSVs (paths only, not raw data)
├── models/                  # Model definitions (RA-UNet, mean teacher wrapper, etc.)
├── train.py                 # Training script
├── eval.py                  # Evaluation / inference script
├── utils/                   # Data loading, metrics, logging helpers
└── README.md

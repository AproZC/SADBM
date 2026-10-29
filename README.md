# SADBM: Structure-Aware Diffusion Bridge Model for SAR-to-Optical Image Translation (S2OIT)

> **SADBM** is a theoretically grounded diffusion-bridge framework for **SAR-to-Optical Image Translation (S2OIT)**, designed to improve structural fidelity by explicitly modeling the cross-domain mapping from SAR distributions to optical imagery.
>
> **Dataset release:** We will publicly release the **SEN1-2 Scene** dataset, including paired SAR–optical images, scene-level annotations, and the training/test splits used in our experiments, through this repository alongside the SADBM implementation.

---

## Release Status

| Resource | Status |
| --- | --- |
| SADBM source code, configurations, and evaluation scripts | Planned for release upon paper acceptance |
| Pretrained models | Planned for release upon paper acceptance |
| SEN1-2 Scene images, annotations, and training/test splits | Release planned; download links will be added here |

Release announcements, download links, and usage instructions will be maintained in this repository.

---

## 1. Overview

Synthetic Aperture Radar (SAR) can observe the Earth under all-weather and day-night conditions, yet it is difficult for non-experts to interpret. **SAR-to-Optical Image Translation (S2OIT)** aims to generate visually interpretable optical-like imagery from SAR inputs, facilitating cross-modal Earth observation and downstream tasks.

Preserving geometry, edges, and scene layouts remains challenging because of SAR speckle interference and the differences between SAR and optical imaging. To address these challenges, we propose **SADBM (Structure-Aware Diffusion Bridge Model)**, which combines an explicit diffusion-bridge formulation with a structure-aware network design.

---

## 2. Key Contributions

### 2.1 Structure-Aware Diffusion Bridge (Doob’s h-transform)

We incorporate **Doob’s h-transform** into the diffusion process to build an explicit **SAR-to-optical diffusion bridge**. The formulation introduces endpoint-dependent guidance into the translation dynamics.

### 2.2 Edge-information Enhancement (E²)

**E²** enhances SAR structural cues by fusing SAR edge maps with guidance from optical edges, while suppressing speckle-induced artifacts.

### 2.3 Hierarchical Structural Extraction (HSE)

**HSE** extracts **global-to-local** structures and injects **multi-scale** cues into intermediate layers for structural representation.

### 2.4 SEN1-2 Scene Dataset

We curate **SEN1-2 Scene**, a labeled subset of SEN1-2 with six scene categories, for evaluating SAR-to-optical translation and downstream scene classification. The planned public release will include the paired images, annotations, and fixed training/test splits.

---

## 3. Evaluation

We evaluate SADBM on **SEN1-2 Scene** and **SAR2Opt**, using both quantitative metrics and qualitative comparisons to assess translation quality and structural preservation.

The reported metrics are **PSNR ↑**, **SSIM ↑**, **CW-SSIM ↑**, **ERQA ↑**, **RMSE ↓**, **LPIPS ↓**, **FSIM ↑**, **FID ↓**, and **KID ↓**. PSNR is computed over all three RGB channels.

We also evaluate downstream scene classification by concatenating SAR inputs with translated optical images, using **ResNet-18**, **ResNet-50**, **DINO**, and **DINOv2** backbones. Detailed results and category-specific failure analyses are reported in the manuscript and supplementary material.

---

## 4. Datasets

### 4.1 SEN1-2 Scene

**SEN1-2 Scene** is curated from the [SEN1-2 benchmark](https://isprs-annals.copernicus.org/articles/IV-1/141/2018/) for paired SAR-to-optical translation and scene-level classification.

SAR–optical image pairs were manually selected according to scene content. Winter samples were excluded to distinguish SAR-to-optical translation from optical snow removal. Scene labels were assigned by the authors and jointly reviewed until consensus was reached.

The dataset covers six categories: **Farmland, Forest, Mountain, Rural, Semi-Urban, and Urban**.

| Split | Number of SAR–optical image pairs |
| --- | ---: |
| Training | 3,785 |
| Test | 944 |
| Total | 4,729 |

#### Planned Public Release

The dataset and its annotations will be made publicly available through **this same GitHub repository**, together with the SADBM code. The release will contain:

- **Paired SAR and optical images** for the training and test sets.
- **Scene-level labels** and the class-to-index mapping for all six categories.
- **Sample identifiers and pairing information** linking each SAR image to its optical counterpart and annotation.
- **Fixed training/test split files** matching the 3,785-pair training set and 944-pair test set used in the revised manuscript.
- **Dataset documentation** describing curation, annotation, directory organization, source attribution, and applicable usage terms.

**Download status:** The dataset release is being prepared. Download links and loading instructions will be added to this section once the files are available.

SEN1-2 Scene is a curated and annotated subset of SEN1-2. Please acknowledge the original SEN1-2 benchmark as well as our work when using this subset.

### 4.2 SAR2Opt

We also evaluate SADBM on **SAR2Opt**. Please refer to the [official SAR2Opt repository](https://github.com/MarsZhaoYT/SAR2Opt-Heterogeneous-Dataset) for dataset downloads, documentation, and citation information.

---

## 5. Installation and Usage

Installation instructions, dependency versions, and commands for training, inference, and evaluation will be provided with the code release. Pretrained model download links and the corresponding configurations will also be documented here.

# SADBM: Structure-Aware Diffusion Bridge Model for SAR-to-Optical Image Translation (S2OIT)

> SADBM translates a synthetic aperture radar (SAR) image into an optical image using a diffusion bridge that starts from an edge-enhanced version of the SAR input.

---

## Release Status

| Resource | Status |
| --- | --- |
| SADBM source code, configurations, and evaluation scripts | Planned for release upon paper acceptance |
| Pretrained models | Planned for release upon paper acceptance |

---

## 1. Overview

SAR can image the Earth day and night through cloud cover. Translating a SAR observation into optical imagery can make a scene easier to interpret, but speckle and differences between the two sensors can obscure field boundaries, roads, and buildings. SADBM uses the geometry visible in the SAR observation to guide translation. It learns from paired SAR and optical images and requires only a SAR image at inference.

---

## 2. Key Contributions

### 2.1 Structure-Aware Diffusion Bridge (Doob’s h-transform)

We use **Doob’s h-transform** to construct a diffusion bridge between an edge-enhanced SAR image and its paired optical target. During inference, the reverse sampler starts at the SAR-derived endpoint and uses that endpoint to guide each denoising step.

### 2.2 Edge-information Extraction (E²)

A lightweight U-Net learns to refine Sobel edges from SAR images using paired optical edge maps as supervision during pretraining. A learned weight blends the raw and refined SAR edge maps. A multi-scale residual network then fuses the blended edges with the SAR image to form the source endpoint.

### 2.3 Hierarchical Structural Extraction (HSE)

The **Global-structure Interaction (GI)** block combines patch-wise self-attention with dilated depthwise convolutions to capture long-range structure and local detail. The **Shallow-information Injection (SI)** module uses cross-attention to bring features from several encoder resolutions into the bottleneck, preserving fine geometric detail for the decoder.

### 2.4 SEN1-2 Scene Dataset

We curate **SEN1-2 Scene**, a six-class subset of SEN1-2, to evaluate both image translation and the value of translated optical imagery for scene classification.

---

## 3. Evaluation

### Image translation

We compare SADBM with 12 baselines on **SEN1-2 Scene** and **SAR2Opt**. Tables II and III of the manuscript report nine metrics.

| Comparison | Metrics (↑ higher is better, ↓ lower is better) |
| --- | --- |
| Each translation and its paired optical reference | PSNR ↑, SSIM ↑, CW-SSIM ↑, MHD ↓, RMSE ↓, LPIPS ↓, FSIM ↑ |
| The sets of translated and real optical images | FID ↓, KID ↓ |

Paired metrics use the full image at its inference resolution. For SEN1-2 Scene, both images are evaluated at their native 256 × 256 pixels. For SAR2Opt, the full 600 × 600 optical reference is resized to 512 × 512 with bicubic interpolation to match the prediction. RGB PSNR uses one mean squared error over all pixels and all three channels. The **modified Hausdorff distance (MHD)** measures boundary localization error in pixels between Canny edge maps extracted from the translation and its optical reference.

SADBM ranks first on all seven paired metrics on SEN1-2 Scene and on six of seven on SAR2Opt, where cBBDM achieves the lowest LPIPS. Palette achieves the lowest FID and KID on SEN1-2 Scene, and ASGIT achieves the lowest FID and KID on SAR2Opt.

### Downstream scene classification

On SEN1-2 Scene, we concatenate the SAR input with its translated optical image and compare classification against a SAR-only baseline. Tables IX–XII report per-class precision, overall accuracy (OA), average accuracy (AA, the mean per-class recall), and Cohen’s kappa for **ResNet-18**, **ResNet-50**, **DINO**, and **DINOv2**.

---

## 4. Datasets

### 4.1 SEN1-2 Scene

The six scene categories are **Farmland, Forest, Mountain, Rural, Semi-Urban, and Urban**. The paired SAR and optical images come from the [SEN1-2 benchmark](https://isprs-annals.copernicus.org/articles/IV-1/141/2018/).

| Split | Number of SAR–optical image pairs |
| --- | ---: |
| Training | 3,785 |
| Test | 944 |
| Total | 4,729 |

### 4.2 SAR2Opt

SAR2Opt contains co-registered SAR and optical images from multiple cities, with dense urban structures imaged at 1 m resolution. Dataset downloads, documentation, and citation information are available from the [official SAR2Opt repository](https://github.com/MarsZhaoYT/SAR2Opt-Heterogeneous-Dataset).

---

## 5. Installation and Usage

Installation instructions, dependency versions, and commands for training, inference, and evaluation will be provided with the code release. Pretrained model download links and the corresponding configurations will also be documented here.

# 3D Gaussian Splatting (3DGS): Literature Review, Coding & Resources

A curated repository dedicated to prior art research, tool curation, datasets, coding standards, and literature review on **3D Gaussian Splatting (3DGS)**, developed in the context of M.Sc. research.

> **Main Focus:** The end-to-end 3DGS ecosystem — from reconstruction (*Structure-from-Motion*) and splat training to **interoperable coding/compression (MPEG-I GSC)**, rendering, and perceptual quality assessment (*Quality Assessment*).

## Table of Contents

* [Pipeline Overview](#pipeline-overview)
* [Highlight: MPEG-I GSC Standardization](#highlight-mpeg-i-gsc-standardization)
* [SfM and Sampling Tools](#sfm-and-sampling-tools)
* [Splat Generation and Training Tools](#splat-generation-and-training-tools)
* [Coding and Compression Tools](#coding-and-compression-tools)
* [Rendering and Visualization Tools](#rendering-and-visualization-tools)
* [Datasets](#datasets)
* [Papers and Literature Review](#papers-and-literature-review)
* [Update Guidelines](#update-guidelines)

## Pipeline Overview

```
[ Capture / Datasets ] ──► [ SfM / Poses ] ──► [ Splat Generation ] ──► [ Coding (GSC) ] ──► [ Rendering & QA ]
```

## Highlight: MPEG-I GSC Standardization

### [ISO/IEC MPEG-I — Gaussian Splat Coding (GSC)](https://mpeg.expert/gsc/index.html)

Official portal tracking the **MPEG (WG 7, WG 4, and JVET)** standardization activities for interoperable compression of 3D Gaussian Splat representations. This is the primary normative reference for 3DGS coding and evaluation.

The MPEG GSC effort is structured into two main tracks:

1. **Short-Term (Profiles within Existing Standards):**
   * **GS4 — V-PCC Gaussian Splat Profile (`ISO/IEC 23090-5`):** Video-based solution (*Video-based Point Cloud Compression*) that maps Gaussian Splat parameters into 2D representations compressed using standard video codecs. Finalized as a *Final Draft Amendment (FDAM)* in October 2026 (consolidated into the 5th edition of V-PCC).
   * **GS5 — G-PCC Gaussian Splat Profile (`ISO/IEC 23090-9`):** Geometry-based solution (*Geometry-based Point Cloud Compression*) focused on efficient coding of explicit Gaussian primitive parameters. FDAM expected in January 2027.

2. **Long-Term (Joint Exploration):**
   * Collaborative research (WG 7, WG 4, and JVET) targeting new coding tools (quantization, parameter ordering, prediction), support for **dynamic Gaussian Splats**, temporal consistency, and the consolidation of reference software and evaluation metrics under *Common Test Conditions (CTC)*.

**Resources available on the portal:**

* **Live Browser Demo (WebAssembly):** Real-time decoding and side-by-side visual comparison of GS4 and GS5 bitstreams directly in the browser.
* **Reference Software (Public):** [V-PCC Test Model — TMC2 (with GS4 profile)](https://github.com/MPEGGroup/mpeg-pcc-tmc2).
* **Evaluation Framework:** Anchor methodologies, objective metrics over rendered views, and guidelines for subjective quality evaluation using controlled camera trajectories (*pose traces*).

## SfM and Sampling Tools

Tools responsible for camera pose estimation, calibration, and sparse point cloud generation used to initialize Gaussian Splats.

| Tool | Description | Link |
| :--- | :--- | :--- |
| **COLMAP** | General-purpose *Structure-from-Motion* (SfM) and *Multi-View Stereo* (MVS) pipeline. The de facto standard for camera pose extraction and sparse initialization in 3DGS workflows. | [Official Website](https://colmap.github.io/index.html) |
| **Spirula Studio** *(SfM module)* | Includes a high-speed built-in SfM module, video frame extraction, AI-based masking, and metric scale support, eliminating the need to run COLMAP separately. | [GitHub](https://github.com/harry7557558/spirula-studio) |

## Splat Generation and Training Tools

Libraries, frameworks, and standalone applications for optimizing/training 3DGS models from multi-view images or videos.

| Tool | Backend / Stack | Highlights | Link |
| :--- | :--- | :--- | :--- |
| **gsplat** | CUDA / PyTorch | Open-source library by the *Nerfstudio* team for accelerated differentiable rasterization of 3DGS. Widely adopted in academic research due to its modularity and memory efficiency. | [GitHub](https://github.com/nerfstudio-project/gsplat) |
| **Spirula Studio** | Vulkan / CUDA (C++) | Cross-vendor trainer (NVIDIA, AMD, Intel, Apple Silicon) in a single binary (video → splat → mesh). Features VRAM-efficient quantized training and native support for 360° and fisheye cameras. | [GitHub](https://github.com/harry7557558/spirula-studio) |
| **Brush** | WebGPU / Rust (Burn) | Cross-platform 3DGS reconstruction engine (Windows, Linux, macOS, Android, and browser via WASM). Free of heavy CUDA dependencies, allowing real-time inspection and interaction during training. | [GitHub](https://github.com/ArthurBrussee/brush) |

## Coding and Compression Tools

Standards, reference codecs, and research methods aimed at bitrate reduction and compact storage of 3DGS models.

| Resource | Approach | Status / Notes | Link |
| :--- | :--- | :--- | :--- |
| **MPEG-I GSC (GS4 / GS5)** | Standardization (V-PCC & G-PCC) | Official ISO/IEC profiles for interoperable Gaussian Splat compression, including anchors and *Common Test Conditions (CTC)*. | [MPEG GSC Portal](https://mpeg.expert/gsc/index.html) |
| **MPEG V-PCC TMC2 (GS4)** | Video-based (`ISO/IEC 23090-5`) | Public reference software on GitHub with support for the GS4 profile. | [GitHub](https://github.com/MPEGGroup/mpeg-pcc-tmc2) |
| *To be added...* | *Neural / entropy-based codecs* | *Reserved for literature methods (e.g., HAC, ContextGS, CompGS).* | — |

## Rendering and Visualization Tools

Interactive viewers, rasterizers, and players (desktop and web) for visual inspection and quality evaluation of Gaussian Splats.

| Tool | Platform | Highlights | Link |
| :--- | :--- | :--- | :--- |
| **Brush (Viewer)** | Desktop, Android & Web (WebGPU) | Real-time viewer supporting `.ply`, `.compressed.ply`, URL streaming, and animated sequences (`.zip` / delta frames). | [GitHub](https://github.com/ArthurBrussee/brush) |
| **MPEG GSC Live Demo** | Web (WebAssembly) | Integration of the *SuperSplat* player with GS4 and GS5 reference decoders compiled to WASM for direct comparison against uncompressed originals. | [MPEG GSC Portal](https://mpeg.expert/gsc/index.html) |
| **Spirula Studio (Viewer)** | Desktop & Web (HTTP) | Built-in viewer for inspecting 3DGS models, sparse reconstructions, meshes, and exporting renders (images and videos). | [GitHub](https://github.com/harry7557558/spirula-studio) |

## Datasets

*Section under construction — this table will catalog datasets used for training, compression (MPEG GSC CTC), and perceptual quality assessment.*

| Dataset | Content Type | Primary Use | Link |
| :--- | :--- | :--- | :--- |
| *Cataloging in progress...* | *Static / Dynamic / Objects / Scenes* | *Training, Compression (CTC), or QA* | — |

## Papers and Literature Review

Curated list of scientific papers relevant to the state of the art in 3DGS, compression, and Quality Assessment.

### Quality Assessment (3DGS-QA) & Surveys

| Year | Title | Authors | Focus / Main Contribution | Link |
| :--- | :--- | :--- | :--- | :--- |
| 2025 | **3DGS-IEval-15K: A Large-scale Image Quality Evaluation Database for 3D Gaussian-Splatting** | Yuke Xing, Jiarui Wang, William Gordon, Zhu Li, Guangtao Zhai, Yiling Xu | 3DGS-IEval-15K is the first large-scale image quality assessment (IQA) dataset specifically designed for compressed 3DGS representations. | [github.com/YukeXing/3DGS-IEval-15K](https://github.com/YukeXing/3DGS-IEval-15K) |
| 2026 | **Quality Assessment of 3D Gaussian Splatting: Distortions, Benchmarks, and Open Challenges** | Shuai Liu, Binqiang Liu, Qingyu Mao, Jiacong Chen, Yongsheng Liang, Youneng Bao | Critical survey on 3DGS-QA. Establishes a taxonomy of native 3DGS distortions (*needle-like*, *floaters*, *popping*, *cloud-like blur*, *aliasing*), compares subjective benchmarks, analyzes objective metric reliability, and proposes guidelines for native evaluation protocols. | [arXiv:2609.23027](https://arxiv.org/abs/2609.23027) |
| 2026 | **Perceptual Quality Assessment of 3D Gaussian Splatting: A Subjective Dataset and Prediction Metric** | Zhaolin Wan, Yining Diao, Jingqi Xu, Hao Wang, Zhiyang Li, Xiaopeng Fan, Wangmeng Zuo, Debin Zhao | An publicly-available 3DGS-QA dataset | [github.com/diaoyn/3DGSQA](https://github.com/diaoyn/3DGSQA) |


### 3DGS Compression and Representation

| Year | Title | Authors | Focus / Main Contribution | Link |
| :--- | :--- | :--- | :--- | :--- |
| — | *To be added...* | — | *Seminal 3DGS papers and coding/compression methods.* | — |

## Update Guidelines

To keep the repository well-organized throughout the M.Sc. research, new entries should follow this convention:

* **Tools:** Name, pipeline stage, requirements/stack, and official link.
* **Papers:** Year, title, authors, concise summary of the contribution (1–2 sentences), and link (arXiv/DOI/GitHub).
* **Datasets:** Name, resolution/scene count, license, and download link.

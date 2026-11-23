---
title: Introduction — 3DGS Research & Pipeline
date: 2026-11-23
tags:
  - 3dgs
  - gaussian-splatting
  - msc-research
  - lgm
  - daily-log
status: in-progress
---

# Introduction — 3D Gaussian Splatting (3DGS)

> [!info] Repository Context
> This vault organizes the M.Sc. research notes on the end-to-end **3D Gaussian Splatting (3DGS)** ecosystem — from reconstruction and splat generation to interoperable coding/compression (**MPEG-I GSC**), rendering, and perceptual quality assessment (**3DGS-QA**).

---

## Progress Log — 2026-11-19 to 2026-11-23

### 1. Single-Image 3D Generation Notebook (`01_single_image_to_3dgs_lgm.ipynb`)
Built and optimized an end-to-end notebook to generate a 3D **Gaussian Splatting** model from a single 2D image:

1. **Two-Stage Pipeline:**
   - **Multi-view Diffusion** (`dylanebert/multi-view-diffusion`): synthesizes 4 views of the object (*Right, Front, Left, Back*) from one input image.
   - **LGM — Large Gaussian Model** (`dylanebert/LGM`): reconstructs a 3D Gaussian representation from the 4 views and exports it as a `.ply` file.
2. **Environment Compatibility:**
   - Added a conditional **Python 3.13+** workaround for `kiui` typing issues.
   - Replaced `xformers.ops.memory_efficient_attention` with PyTorch's native **SDPA** (`scaled_dot_product_attention`), handling 4D tensor transposition `(B, L, H, D) <-> (B, H, L, D)` and optional `scale`/`p` arguments.
3. **PLY Inspection & 3D Visualization:**
   - Inspected the saved `.ply` file with `plyfile` and rendered a dynamic Markdown summary (`IPython.display.Markdown`) reporting total generated Gaussians, pruned low-opacity Gaussians, and final useful count.
   - Added interactive 3D visualization with **Plotly** (`go.Scatter3d`), supporting both RGB and Spherical Harmonics (`f_dc_0..2`) color extraction, configurable subsampling (`MAX_PLOT_POINTS = 20_000`), and white title typography over a dark canvas.
4. **Refactoring, Error Handling & VRAM Optimization:**
   - Removed a duplicated `splat_pipeline` inference cell.
   - Wrapped inference calls in `torch.inference_mode()` and added CPU/GPU offloading (`to("cpu")` + `torch.cuda.empty_cache()`) between stages to prevent `OutOfMemoryError`.
   - Added CUDA/VRAM validation, safe image loading (`timeout`, `raise_for_status()`, local path support, and RGBA-to-RGB white-background compositing), `.ply` I/O checks, fixed `SEED = 42` for reproducibility, and standardized the notebook in English.

### 2. Repository Reference Base (`README.md`)
- Structured the end-to-end pipeline overview: `Capture / Datasets -> SfM / Poses -> Splat Generation -> Coding (GSC) -> Rendering & QA`.
- Curated core tools (**COLMAP**, **Spirula Studio**, **gsplat**, **Brush**), **MPEG-I GSC** reference software (**TMC2 / GS4** and **TMC13-GS / GS5**), and **3DGS-QA** papers/datasets (`3DGS-IEval-15K`, `3DGSQA`, and the 2026 survey).

---

## Next Steps

- [ ] Run `gaussian_splatting_lgm_test.ipynb` end-to-end and log benchmarks (inference time, peak VRAM, `.ply` file size, and final Gaussian count).
- [ ] Inspect the exported `.ply` model in dedicated viewers (e.g., **Brush** or **SuperSplat**).
- [ ] Test the pipeline with custom input images (including transparent PNGs).
- [ ] Expand `README.md` with benchmark datasets and 3DGS compression papers (e.g., HAC, ContextGS, CompGS).
- [ ] Create linked notes for each pipeline stage:
  - [[MPEG-I GSC - GS4 and GS5]]
  - [[3DGS Quality Assessment]]
  - [[Experiments - LGM]]

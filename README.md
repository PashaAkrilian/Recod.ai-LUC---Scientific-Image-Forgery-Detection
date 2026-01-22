# Recod.ai/LUC — Scientific Image Forgery Detection

This document summarizes the **Recod.ai/LUC Scientific Image Forgery Detection** Kaggle competition and explains what is contained in this repository.

## Competition Overview
The competition focuses on **detecting forgery in scientific images**. The primary task is to identify manipulated regions and export them as **segmentation masks**. Participants generate predictions in **Run-Length Encoding (RLE)** format for every `case_id` listed in `sample_submission.csv`.

> Note: official competition details (rules, evaluation, examples) are available on Kaggle: <https://www.kaggle.com/competitions/recodai-luc-scientific-image-forgery-detection>.

## Dataset (brief)
The notebooks in this repo expect the Kaggle dataset under:

```
/kaggle/input/recodai-luc-scientific-image-forgery-detection/
```

Typical contents:
- `train_images/` — training images.
- `train_masks/` — forgery masks for training (can be multiple masks per image).
- `test_images/` — test images.
- `sample_submission.csv` — submission template with `case_id` and `annotation` columns.

> Note: verify the exact structure on Kaggle by adding the competition dataset as an input.

## Submission Format
The submission file follows `sample_submission.csv` with columns:
- `case_id` — image ID.
- `annotation` — RLE mask for forged regions.

**RLE** uses **column-major (Fortran order)**, which is standard for Kaggle CV challenges. Ensure the mask dimensions match the original image size.

## Repo Contents & Notebook Flow
This repo contains experiments and a DINOv2-based pipeline for feature extraction, mask reconstruction, and submission generation:

- `recod-ai-luc.ipynb` — end-to-end pipeline (profiling → feature extraction → mask reconstruction → submission).
- `recod-ai-luc dinov2 prep.ipynb` — dataset profiling, manifest creation, and DINOv2 feature caching.
- `recod-ai-luc dinov2 base.ipynb` & `recod-ai-luc dinov2 base upgrade.ipynb` — DINOv2 experiment variants.
- `recod-ai-luc-submission.ipynb` — submission-focused notebook.

## Quick Usage
1. Open the main notebook (`recod-ai-luc.ipynb`) in Kaggle.
2. Add the competition dataset as an input.
3. Run the cells in order to perform:
   - profiling & sanity checks,
   - feature extraction,
   - mask reconstruction,
   - submission generation.

## License & Notes
- These notebooks are provided as experimental references and baselines.
- Check the Kaggle competition rules for data usage and sharing requirements.

 # Dataset Preparation Guide

## Data Source

This project uses a Kaggle brain MRI dataset for binary classification (tumor vs healthy).

## Required Directory Structure

Prepare the following structure under the project root (matches the default paths in `Model_Comparison.ipynb`):

```text
Brain-Tumor-Detection-CNN-vs-ViT/
├─ metadata.csv
├─ metadata_rgb_only.csv
└─ Brain Tumor Data Set/
   └─ Brain Tumor Data Set/
      ├─ Brain Tumor/
      │  ├─ xxx.jpg
      │  └─ ...
      └─ Healthy/
         ├─ yyy.jpg
         └─ ...
```

## File Description

- `metadata.csv`: Original metadata (`image / class / format / mode / shape`)
- `metadata_rgb_only.csv`: RGB-only metadata (recommended for main experiment)
- `Brain Tumor/`: Tumor image directory
- `Healthy/`: Healthy image directory

## Default Notebook Paths

`Model_Comparison.ipynb` reads the following by default:
- `metadata_rgb_only.csv`
- `Brain Tumor Data Set/Brain Tumor Data Set/Brain Tumor`
- `Brain Tumor Data Set/Brain Tumor Data Set/Healthy`

If your local directory structure is different, update variables such as `PROJECT_ROOT` and `DATA_ROOT` in the notebook path configuration cell.

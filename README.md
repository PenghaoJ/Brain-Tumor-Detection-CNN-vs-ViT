# Brain-Tumor-Detection-CNN-vs-ViT

Binary classification project on a Kaggle brain MRI dataset, comparing CNN and Vision Transformer (ViT) approaches for tumor detection.

## Main Experiment Entry

Use `Model_Comparison.ipynb` as the primary and recommended workflow. It includes:
- Environment and dependency checks
- Dataset path validation and loading
- Unified train/validation/test splitting
- CNN and Transformer training
- Metric comparison (Accuracy, AUC, Precision, Recall, F1)
- Confusion matrix, ROC curve, and conclusion outputs

## Quick Start

1. Create and activate a virtual environment (recommended)
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Prepare the dataset structure according to `DATASET.md`
4. Open and run `Model_Comparison.ipynb` from top to bottom

## Project Files

- `Model_Comparison.ipynb`: Main comparison notebook (recommended)
- `metadata_rgb_only.csv`: RGB-only metadata used in the main experiment
- `metadata.csv`: Original metadata (includes non-RGB entries)
- `comparison_summary.csv`: Key metric summary table
- `model_comparison_line.png`: Metric comparison figure
- `MODEL_COMPARISON_GUIDE.md`: Notebook usage guide
- `DATASET.md`: Dataset preparation instructions

## Notes

- On Windows, if TensorFlow import fails with DLL/path-related errors, use a shorter virtual environment path and verify the selected interpreter.

## Runtime Verification (2026-05-07, re-validated)

Two rounds were tested:
- Round 1 (deep project `.venv` path): failed with `ImportError: DLL load failed while importing _ml_dtypes_ext: The filename or extension is too long.`
- Round 2 (short-path env `C:\venv311bt`): full notebook execution succeeded

Successful execution command (project root):
```bash
C:\venv311bt\Scripts\jupyter.exe execute Model_Comparison.ipynb --kernel_name=venv311bt --timeout=-1 --output Model_Comparison.executed.ipynb
```

Execution notes:
- Generated artifact: `Model_Comparison.executed.ipynb`
- Notebook JSON validation warnings were observed (some historical stream outputs miss `name`), but training/evaluation completed successfully

## Current Comparison Results (`comparison_summary.csv`)

- `CNN_Light`: Accuracy `0.6347`, AUC `0.7282`, Precision `0.7027`, Recall `0.5714`, F1(tumor) `0.6303`
- `Transformer_Light`: Accuracy `0.5449`, AUC `0.5637`, Precision `0.5449`, Recall `1.0000`, F1(tumor) `0.7054`

Interpretation:
- CNN is stronger on Accuracy/AUC/Precision
- Transformer is stronger on Recall and tumor-class F1 (better for missed-tumor-sensitive scenarios)

## Re-run Result Summary (`Model_Comparison.executed.ipynb`)

- Auto-conclusion (priority: Accuracy/AUC/F1): `CNN_Light` ranked first
- Relative gains over runner-up:
  - Accuracy gain: `8.98%`
  - AUC gain: `16.45%`
  - Tumor-class F1 gain: `-7.51%` (CNN lower than Transformer on tumor F1)
- Medical-priority addendum (missed tumor risk):
  - Higher tumor recall: `Transformer_Light (1.0000)`
- Overall average score (5 metrics):
  - Best overall model: `Transformer_Light`
  - Lead over `CNN_Light`: `1.83%`

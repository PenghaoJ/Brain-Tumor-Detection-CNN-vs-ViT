# 数据集准备说明

## 数据来源

本项目使用脑部 MRI 脑肿瘤二分类数据集（Kaggle 来源）。

## 目录结构要求

请在项目根目录下准备如下结构（与 `Model_Comparison.ipynb` 默认路径一致）：

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

## 文件说明

- `metadata.csv`: 原始元数据（包含 image / class / format / mode / shape）
- `metadata_rgb_only.csv`: 仅 RGB 样本元数据（主实验推荐）
- `Brain Tumor/`: 肿瘤类图像目录
- `Healthy/`: 健康类图像目录

## Notebook 默认读取路径

`Model_Comparison.ipynb` 默认使用以下路径：
- `metadata_rgb_only.csv`
- `Brain Tumor Data Set/Brain Tumor Data Set/Brain Tumor`
- `Brain Tumor Data Set/Brain Tumor Data Set/Healthy`

如果你本地目录不同，请在 notebook 的路径配置单元中修改 `PROJECT_ROOT`、`DATA_ROOT` 等变量。

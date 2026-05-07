# Brain-Tumor-Detection-CNN-vs-ViT

基于 Kaggle 脑部 MRI 数据集的二分类项目，用于对比 CNN 与 Vision Transformer (ViT) 在脑肿瘤检测任务中的表现。

## 当前主线实验

本仓库推荐以 `Model_Comparison.ipynb` 作为唯一主入口运行，完成以下流程：
- 环境与依赖检查
- 数据路径验证与读取
- 统一数据切分（train/val/test）
- CNN 与 Transformer 训练
- 指标对比（Accuracy、AUC、Precision、Recall、F1）
- 混淆矩阵、ROC 曲线与结论输出

## 快速开始

1. 创建并激活虚拟环境（可选，但推荐）
2. 安装依赖：
   ```bash
   pip install -r requirements.txt
   ```
3. 按 `DATASET.md` 准备数据目录
4. 打开并从上到下运行 `Model_Comparison.ipynb`

## 项目文件说明

- `Model_Comparison.ipynb`: 主对比实验 Notebook（推荐使用）
- `metadata_rgb_only.csv`: RGB 样本元数据（主实验使用）
- `metadata.csv`: 原始元数据（包含非 RGB 条目）
- `comparison_summary.csv`: 关键指标汇总
- `model_comparison_line.png`: 指标对比图
- `MODEL_COMPARISON_GUIDE.md`: 对比实验运行说明
- `DATASET.md`: 数据集准备说明

## 备注

- 如果在 Windows 下遇到 TensorFlow 导入异常（如 DLL / path 相关报错），优先缩短虚拟环境路径并确认解释器版本与依赖匹配。

## 运行可用性检查（2026-05-07，已复测）

已完成两轮实测：
- 第一轮（项目内深路径 `.venv`）：失败，报错 `ImportError: DLL load failed while importing _ml_dtypes_ext: The filename or extension is too long.`
- 第二轮（短路径环境 `C:\venv311bt`）：**整本执行成功**

本次成功执行命令（项目根目录）：
```bash
C:\venv311bt\Scripts\jupyter.exe execute Model_Comparison.ipynb --kernel_name=venv311bt --timeout=-1 --output Model_Comparison.executed.ipynb
```

说明：
- 已生成执行产物：`Model_Comparison.executed.ipynb`
- 执行过程中有 notebook JSON 校验告警（历史输出中个别 `stream` 缺少 `name` 字段），但不影响本次训练与评估流程完成

## 当前已有对比结果（来自 `comparison_summary.csv`）

在已保存的历史结果中：
- `CNN_Light`: Accuracy `0.6347`, AUC `0.7282`, Precision `0.7027`, Recall `0.5714`, F1(tumor) `0.6303`
- `Transformer_Light`: Accuracy `0.5449`, AUC `0.5637`, Precision `0.5449`, Recall `1.0000`, F1(tumor) `0.7054`

简要解读：
- CNN 在 Accuracy/AUC/Precision 上更高；
- Transformer 在 Recall 和肿瘤类 F1 上更高（更偏向减少漏检）。

## 本次复跑结果摘要（来自 `Model_Comparison.executed.ipynb`）

- 自动结论（按 Accuracy/AUC/F1 优先排序）：表现最好的是 `CNN_Light`
- 指标差值（相对第二名）：
  - 准确率提升：`8.98%`
  - AUC 提升：`16.45%`
  - 肿瘤类 F1 提升：`-7.51%`（即 CNN 在肿瘤 F1 上低于 Transformer）
- 医疗场景补充判断（更关注漏检）：
  - 肿瘤召回率更高的是 `Transformer_Light (1.0000)`
- 综合平均分（五项指标均值）结论：
  - 总体最优模型：`Transformer_Light`
  - 相对 `CNN_Light` 平均指标领先：`1.83%`

# SciDiagFuse-Net

Multimodal Visual Fusion for Automatic Classification of Scientific Diagram Types in LGS-Aligned 8th Grade Science Exam Questions

## Overview

SciDiagFuse-Net is a multimodal image fusion framework that classifies scientific diagram types embedded in Turkish 8th-grade science (LGS) exam questions. The model fuses visual features from a Swin Transformer backbone with textual features from a Turkish BERT encoder via a bidirectional cross-attention module.

## Dataset: TurkSciDiag

- 722 labeled images (after augmentation)
- 7 diagram categories: Force/Motion, Graph/Chart, Molecular/Chemical, Experimental Setup, Biological/Anatomical, Astronomical/Earth, Table/Matrix
- Source: LGS exam archives (2018–2025) and MEB official question banks
- Annotated using Label Studio (Cohen's κ = 0.84)

## Model Architecture

| Component | Detail |
|---|---|
| Visual Encoder | Swin Transformer Tiny (ImageNet-21k pretrained) |
| Text Encoder | BERTurk (dbmdz/bert-base-turkish-cased) |
| Fusion | Bidirectional Cross-Attention (8 heads) |
| Input | 224×224 image + 128 token text |
| Output | 7-class softmax |

## Results

| Model | Test F1 | Test Acc |
|---|---|---|
| ResNet-50 | 0.765 | 0.761 |
| Swin-T (image-only) | 0.749 | 0.743 |
| BERTurk (text-only) | 0.041 | — |
| Concat Fusion | 0.688 | 0.688 |
| **SciDiagFuse-Net (Ours)** | **0.799** | **0.798** |

## Ablation Study

| Configuration | Test F1 | Test Acc |
|---|---|---|
| Full Model (Bidirectional + Dropout) | 0.799 | 0.798 |
| Unidirectional Cross-Attention | 0.681 | 0.679 |
| No Dropout | 0.773 | 0.771 |
| Concat Fusion (no cross-attention) | 0.688 | 0.688 |

## Requirements

```bash
pip install torch torchvision timm transformers
pip install albumentations pytesseract pymupdf
pip install scikit-learn pandas matplotlib seaborn
```

## Usage

Open and run `SciDiagFuse_Net.ipynb` in Google Colab.

1. Mount Google Drive
2. Set `BASE_DIR` to your dataset path
3. Run cells sequentially

## Citation

If you use this work, please cite:
T. Aslan, "SciDiagFuse-Net: Multimodal Visual Fusion for Automatic
Classification of Scientific Diagram Types in LGS-Aligned 8th Grade
Science Exam Questions," Abdullah Gül University, 2026.

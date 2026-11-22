# CFMCD-Net

### Adapting SAM for Remote Sensing Change Detection via Local-Global Feature Fusion and Frequency-Aware Interaction

This repository provides reproducibility information for CFMCD-Net, including dataset partitions, training configurations, pretrained model information, and key module settings.

## Code Availability

Detailed experimental configurations and pretrained model information are provided below. The complete source code, training and evaluation scripts, pretrained checkpoints, and usage instructions will be made publicly available upon acceptance of the paper.


## Datasets

All images are cropped into 256 × 256 patches using the dataset partitions listed below.

| Dataset | Training | Validation | Test | Patch size |
|---|---:|---:|---:|---:|
| LEVIR-CD | 7,120 | 1,024 | 2,048 | 256 × 256 |
| WHU-CD | 5,947 | 743 | 744 | 256 × 256 |
| CLCD | 1,440 | 480 | 480 | 256 × 256 |

## Training Configuration

| Item | Configuration |
|---|---|
| SAM backbone | SAM ViT-L |
| CNN branch | ResNet-50 |
| Input size | 256 × 256 |
| Optimizer | AdamW |
| Initial learning rate | 1 × 10⁻⁴ |
| Learning-rate schedule | Cosine annealing |
| Batch size | 4 |
| Training epochs | 200 |
| Hardware | Single NVIDIA GeForce RTX 3060 |
| Model selection | Best checkpoint on the validation set |
| Data augmentation | Rotation, flipping, random cropping, and photometric distortion |
| Training objective | Weighted cross-entropy loss and Dice loss |
| Loss weights | λ_WCE = 0.8 and λ_Dice = 0.2 |
| Dice smoothing term | 1 × 10⁻⁶ |

## Key Module Settings

| Component | Configuration |
|---|---|
| MoRA rank | 16 |
| MoRA target module | QKV projection layers |
| MoRA insertion | All Transformer blocks of SAM ViT-L |
| Effective MoRA matrix size | 256 × 256 |
| DAFM fusion positions | Transformer blocks 5, 11, and 17 (zero-based indexing) |
| FEFI positions | Transformer blocks 5, 11, 17, and 23 (zero-based indexing) |
| Number of experts | 12 |
| Top-k experts | 6 |
| SAM prompt encoder | Not used |
| SAM mask decoder | Not used |
| Prediction task | Binary change detection |

## Pretrained Model

| Model | Pretraining dataset | Checkpoint | Download |
|---|---|---|---|
| SAM ViT-L | SA-1B | `vit-large-p16_sam-pre_3rdparty_sa1b-1024px_20230411-595feafd.pth` | [Download](https://download.openmmlab.com/mmclassification/v1/vit_sam/vit-large-p16_sam-pre_3rdparty_sa1b-1024px_20230411-595feafd.pth) |

## Release Plan

- [x] Dataset partitions
- [x] Training configurations
- [x] Key module settings
- [x] Pretrained model information
- [ ] Environment installation instructions
- [ ] Training and evaluation code
- [ ] Pretrained CFMCD-Net checkpoints
- [ ] Inference examples

The remaining materials will be released upon acceptance of the paper.

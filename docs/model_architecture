# Model Architecture Documentation
## SurfaceGuard AI: Industrial Defect Segmentation

### 1. Overview

This project implements three deep learning architectures for multi-label industrial surface defect segmentation.

The objective is to predict pixel-level defect masks for four defect categories.

All models accept grayscale images and generate four output channels. Sigmoid activation is used for multi-label prediction because multiple defect categories can occur in the same image.

**Input dimensions:** 1 × 128 × 800  
**Output channels:** 4

---

### 2. Model 1: U-Net from Scratch

**Model name:** `unet_scratch`

This architecture is implemented from scratch using PyTorch without pretrained encoder weights.

Key components:

- Five encoder stages with channel sizes 32, 64, 128, 256 and 512.
- Residual convolutional blocks.
- Max pooling for spatial downsampling.
- Dropout for regularization.
- Transposed convolutions for upsampling.
- Skip connections between encoder and decoder stages.
- SCSE (Spatial and Channel Squeeze-and-Excitation) attention in the decoder.
- Four-channel output convolution.

The model applies input normalization using mean 0.5 and standard deviation 0.25.

**Purpose:** Establish a baseline segmentation architecture and evaluate learning from randomly initialized weights.

---

### 3. Model 2: ResNet34 U-Net

**Model name:** `resnet34_unet`

This model combines an ImageNet-pretrained ResNet34 encoder with a custom U-Net-style decoder.

Key components:

- ImageNet-pretrained ResNet34 backbone.
- Multi-level encoder feature extraction.
- Custom decoder blocks with convolution and batch normalization.
- SCSE attention in decoder stages.
- Hypercolumn feature fusion combining multiple decoder levels.
- Dropout regularization.
- Four-channel output convolution.

Since the original dataset contains grayscale images, the input channel is repeated three times to match the pretrained ResNet34 encoder.

**Purpose:** Use pretrained visual features to improve segmentation performance through transfer learning.

---

### 4. Model 3: DeepLab ResNet50

**Model name:** `deeplab_resnet50`

This architecture uses a pretrained ResNet50 backbone with an Atrous Spatial Pyramid Pooling (ASPP) module and low-level feature fusion.

Key components:

- ImageNet-pretrained ResNet50 backbone.
- Dilated convolution configuration for output stride 16.
- ASPP module for multi-scale contextual feature extraction.
- Low-level feature fusion from the early backbone.
- Decoder for spatial refinement.
- Four-channel segmentation output.

Grayscale images are repeated across three channels to match the pretrained backbone input.

**Purpose:** Capture multi-scale contextual information and improve the segmentation of industrial defects.

---

### 5. Model Comparison

| Feature | U-Net Scratch | ResNet34 U-Net | DeepLab ResNet50 |
|---|---|---|---|
| Encoder | Custom | ResNet34 | ResNet50 |
| Pretrained weights | No | ImageNet | ImageNet |
| Decoder | U-Net | Custom U-Net | DeepLab-style |
| Residual blocks | Yes | Backbone | Backbone |
| SCSE attention | Yes | Yes | Not specified |
| Output channels | 4 | 4 | 4 |

---

### 6. Common Training Design

The training pipeline uses:

- AdamW optimizer.
- OneCycleLR learning-rate scheduler.
- BCE and Dice-based combined loss.
- Exponential Moving Average (EMA).
- Automatic mixed precision when CUDA is available.
- Weighted sampling for defect imbalance.
- Validation-based checkpoint selection.
- Weights & Biases experiment tracking.

The models are trained and evaluated using a common dataset pipeline to support comparison.

---

### 7. Conclusion

The three architectures provide different approaches to industrial defect segmentation.

The scratch-built U-Net provides a custom baseline, ResNet34 U-Net uses transfer learning with a multi-level decoder, and DeepLab ResNet50 uses multi-scale contextual feature extraction.

Their comparative performance is evaluated using validation metrics and Kaggle competition submissions.

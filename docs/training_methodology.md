# Training Methodology
## SurfaceGuard AI: Industrial Defect Segmentation

### 1. Dataset Preparation

The project uses industrial grayscale surface images with four defect categories:

- defect_a
- defect_b
- defect_c
- defect_d

Each image is resized or represented at a fixed spatial resolution of 128 × 800 pixels.

The corresponding segmentation masks are decoded from Run-Length Encoding (RLE) into four-channel binary masks.

**Input image shape:** (128, 800)  
**Input tensor shape:** (1, 128, 800)  
**Target mask shape:** (4, 128, 800)

Images are loaded using OpenCV and stored in memory for efficient training.

### 2. Dataset Splitting

A stratified splitting strategy is used to preserve defect-category combinations across training and validation sets.

The implementation uses:

- StratifiedKFold
- Number of folds: 5
- Shuffle: True
- Random seed: 42

The first fold is selected for training and validation, resulting in approximately 80% training data and 20% validation data.

### 3. Data Preprocessing and Augmentation

Images are converted into floating-point values and normalized to the range [0, 1].

Training augmentation includes:

- Random horizontal flipping.
- Random vertical flipping.
- Random brightness scaling.

The same geometric transformations are applied to the corresponding segmentation masks to preserve image-mask alignment.

Validation images are evaluated without augmentation.

### 4. Class Imbalance Handling

Industrial defect datasets often contain significantly different frequencies of defect categories.

To address this, the training pipeline uses WeightedRandomSampler.

Sampling weights are increased for images containing selected rare defect categories:

| Defect category | Sampling weight |
|---|---:|
| defect_a | 2.0 |
| defect_b | 4.0 |
| defect_d | 1.5 |
| defect_c | 1.0 |

The sampler uses replacement to increase the probability of sampling images containing rare defects.

### 5. Loss Function

The training objective combines Binary Cross-Entropy loss and Dice loss.

The combined loss is:

Loss = 0.5 × BCE Loss + 0.5 × Dice Loss

Class-specific positive weights are:

[3.0, 5.0, 1.0, 1.5]

This gives greater importance to positive pixels belonging to selected rare defect classes.

### 6. Optimizer and Learning Rate Scheduling

The project uses the AdamW optimizer with weight decay of 0.0001.

The learning rate is adjusted using the OneCycleLR scheduler.

The configured maximum learning rates are:

| Model | Learning rate |
|---|---:|
| U-Net from Scratch | 0.002 |
| ResNet34 U-Net | 0.0005 |
| DeepLab ResNet50 | 0.0005 |

For pretrained models, separate parameter groups are used:

- Encoder learning rate: 0.5 × base learning rate.
- Decoder learning rate: 2 × base learning rate.

The OneCycleLR scheduler uses a warm-up proportion of 20%.

### 7. Training Configuration

| Parameter | Configuration |
|---|---|
| Batch size | 16 |
| U-Net epochs | 40 |
| ResNet34 U-Net epochs | 40 |
| DeepLab ResNet50 epochs | 45 |
| Weight decay | 0.0001 |
| Optimizer | AdamW |
| Scheduler | OneCycleLR |
| Mixed precision | Enabled when CUDA is available |
| Random seed | 42 |
| Early stopping patience | 8 |

The

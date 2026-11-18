# SurfaceGuard AI: Industrial Defect Segmentation

## Deep Learning & Generative AI Project | IIT Madras

**Student:** Pallavi Hazra  
**Roll Number:** 23f1002888  
**Term:** T3-2026  
**Programme:** BS in Data Science and Applications  
**Project:** Industrial Surface Defect Segmentation

---

## 1. Project Overview

SurfaceGuard AI is an industrial defect segmentation project that uses deep learning and computer vision to identify and segment defects in industrial surface images.

The objective is to develop segmentation models capable of identifying defective regions at the pixel level, helping distinguish defective surfaces from defect-free areas.

## 2. Project Objectives

- Understand and preprocess industrial surface image data.
- Decode and visualize segmentation masks.
- Develop and evaluate multiple deep learning architectures.
- Apply data augmentation to improve model generalization.
- Track experiments and evaluate model performance.
- Generate predictions in the required Kaggle submission format.

## 3. Models Implemented

Three distinct segmentation architectures were explored:

| Model | Architecture |
|---|---|
| Model 1 | U-Net from Scratch |
| Model 2 | U-Net with ResNet34 Encoder |
| Model 3 | DeepLab with ResNet50 Backbone |

## 4. Experiment Tracking

Experiments were tracked using **Weights & Biases (W&B)**.

The project includes recorded experiment runs for the three model architectures.

Experiment tracking includes:
- Training loss
- Validation loss
- Validation metrics
- Epoch tracking
- Model configurations
- Hyperparameter settings

### DeepLab ResNet50 Experiment

One recorded experiment includes:

| Parameter | Value |
|---|---:|
| Epochs | 45 |
| Batch size | 16 |
| Learning rate | 0.0005 |
| Training loss | 0.1794 |
| Validation loss | 0.2123 |
| Validation foreground Dice | 0.5426 |
| Validation score | 0.6772 |

## 5. Kaggle Performance

The project was evaluated through the Kaggle competition.

**Final recorded Kaggle submission score: 0.66080**

The project achieved the required minimum threshold of 0.65.

## 6. Tools & Technologies

- Python
- PyTorch
- NumPy
- Pandas
- OpenCV
- Albumentations
- Matplotlib
- Weights & Biases
- Kaggle
- GitHub

## 7. Repository Structure

- `notebooks/` – Model experiments and inference notebooks.
- `scripts/` – Training and preprocessing scripts.
- `data/` – Dataset documentation.

## 8. Project Workflow

1. Dataset exploration and preprocessing.
2. Image and mask visualization.
3. Segmentation pipeline development.
4. Model training and experimentation.
5. Validation and performance evaluation.
6. Experiment tracking using W&B.
7. Kaggle inference and submission.
8. Model comparison and analysis.

## 9. Future Improvements

- Further optimization of segmentation architectures.
- Improved handling of class imbalance.
- Test-time augmentation and model ensembling.
- Deployment through an interactive web application.

---

**Project Author:** Pallavi Hazra  
**IIT Madras | BS Data Science and Applications | T3-2026**

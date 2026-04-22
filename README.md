# Image Inpainting with Generative Models

This repository contains a series of **image inpainting experiments** using multiple deep learning approaches:

* Convolutional-based Autoencoder
* Partial Convolutional Autoencoder
* Generative Adversarial Network (GAN)

The experiments were conducted using the **CIFAR-10 dataset** with different masking strategies and training configurations.

---

# Overview

Image inpainting is the task of reconstructing missing or corrupted regions in an image. In this project, several deep learning architectures were implemented and evaluated to determine their performance on small-resolution images.

Three main model types were explored:

1. **Convolutional-based Autoencoder**
2. **Partial Convolutional Autoencoder**
3. **GAN (with Global and Local Discriminators)**

Performance was evaluated using:

* Mean Absolute Error (MAE)
* Mean Squared Error (MSE)
* Dice Coefficient

The best-performing model was the **Convolutional-based Autoencoder**, particularly due to its simplicity and compatibility with small datasets like CIFAR-10. 

---

# Dataset

The dataset used in all experiments is **CIFAR-10**.

* 60,000 RGB images
* Image size: **32×32**
* 10 classes
* Train/Test split:

  * 50,000 training images
  * 10,000 testing images
* Validation set:

  * 20% of training data


---

# Masking Strategies

Three types of masks were used:

1. **Regular Center Mask**
2. **Regular Random Mask**
3. **Irregular Mask**

Mask sizes were randomly generated to simulate missing image regions.

---

# Models

## 1. Convolutional Autoencoder

Architecture:

* Encoder:

  * Convolution layers
  * Activation (ReLU)
  * Pooling layers
* Decoder:

  * Transposed Convolution
  * Skip connections (UNet-like structure)

Used for:

* Experiments **1–3**

---

## 2. Partial Convolutional Autoencoder

Uses **Partial Convolution layers** that operate only on valid pixels.

Features:

* Dynamic mask updates
* Skip connections
* UNet-based architecture

Used for:

* Experiments **4–5**

---

## 3. GAN-Based Inpainting

Architecture:

* Generator (Autoencoder-style)
* Two Discriminators:

  * Global Discriminator
  * Local Discriminator

Training Phases:

1. Generator-only training
2. Discriminator-only training
3. Combined GAN training

Used for:

* Experiments **6–7**

---

# Experiment Summary

| Exp | Model            | Mask Type      | Epochs | Batch Size | Notebook                                               |
| --- | ---------------- | -------------- | ------ | ---------- | ------------------------------------------------------ |
| 1   | Conv Autoencoder | Regular Center | 20     | 32         | `convolutional_autoencoder_regular_center.ipynb`       |
| 2   | Conv Autoencoder | Regular Random | 20     | 32         | `convolutional_autoencoder_regular_random.ipynb`       |
| 3   | Conv Autoencoder | Irregular      | 20     | 32         | `convolutional_autoencoder_irregular.ipynb`            |
| 4   | Partial Conv AE  | Regular Random | 30     | 32         | `partial_convolusion_autoencoder_reguler_center.ipynb` |
| 5   | Partial Conv AE  | Irregular      | 30     | 32         | `partial_convolusion_autoencoder_irreguler.ipynb`      |
| 6   | GAN              | Regular Random | 30     | 32         | `gan_regular_center_b32.ipynb`                         |
| 7   | GAN              | Regular Random | 30     | 800        | `gan_regular_center_b800.ipynb`                        |

---

# Evaluation Results

The following table summarizes the final performance of each experiment on the **test dataset**.

Lower values are better for **MAE** and **MSE**, while higher values are better for **Dice Coefficient**.

| Model            | Mask Type      | Epoch | Batch | MSE ↓       | MAE ↓       | Dice ↑      |
| ---------------- | -------------- | ----- | ----- | ----------- | ----------- | ----------- |
| Conv Autoencoder | Regular Center | 20    | 32    | **0.00108** | 0.01598     | **0.61100** |
| Conv Autoencoder | Regular Random | 20    | 32    | 0.00136     | **0.01103** | 0.60543     |
| Conv Autoencoder | Irregular      | 20    | 32    | 0.00106     | 0.01238     | 0.60701     |
| Partial Conv AE  | Regular Random | 30    | 32    | 0.00284     | 0.02639     | 0.60200     |
| Partial Conv AE  | Irregular      | 30    | 32    | 0.00158     | 0.01912     | 0.60529     |
| GAN              | Regular Random | 30    | 32    | 0.01290     | 0.07920     | 0.57555     |
| GAN              | Regular Random | 30    | 800   | 0.01610     | 0.09060     | 0.56377     |

---

# Key Findings from Experiments

* **Convolutional Autoencoder achieved the best overall performance**, especially for small datasets like CIFAR-10.
* **Partial Convolution performed better with irregular masks**, as expected due to its mask-aware design.
* **GAN showed lower performance**, likely due to its higher complexity compared to dataset size.
* **Smaller batch sizes improved GAN stability**, leading to better results.

---

# Environment

Experiments were conducted using:

* Platform: Kaggle
* GPU: NVIDIA T4 (16 GB)

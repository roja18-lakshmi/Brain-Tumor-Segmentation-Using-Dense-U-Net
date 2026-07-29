# Brain Tumor Segmentation using Optimized Depthwise Separable Convolutional Neural Network with Dense U-Net

A deep learning project for automated brain tumor segmentation from multi-modal MRI scans using the **DSCNN-DU-Net** architecture. The model segments three clinically significant tumor regions—**Enhancing Tumor (ET)**, **Tumor Core (TC)**, and **Whole Tumor (WT)**—to assist in diagnosis and treatment planning.

---

## Overview

Brain tumor segmentation plays a crucial role in medical diagnosis and treatment planning. Manual segmentation of MRI scans is time-consuming, subjective, and difficult to scale for large datasets.

This project implements the **DSCNN-DU-Net** architecture proposed in the research paper *"Brain Tumor Segmentation using Optimized Depthwise Separable Convolutional Neural Network with Dense U-Net"* for automatic segmentation of brain tumors using multi-modal MRI images.

---

## Objectives

* Implement the DSCNN-DU-Net architecture for brain tumor segmentation.
* Segment the three tumor sub-regions:

  * Enhancing Tumor (ET)
  * Tumor Core (TC)
  * Whole Tumor (WT)
* Utilize four MRI modalities (T1, T1ce, T2, and FLAIR).
* Apply preprocessing techniques to improve feature representation.
* Train the network using a hybrid Dice + Binary Cross-Entropy loss.
* Evaluate segmentation performance using medical imaging metrics.

---

## Dataset

**BraTS 2020 (Brain Tumor Segmentation Challenge)**

Dataset Statistics:

* 369 patients
* 4 MRI modalities:

  * T1
  * T1ce
  * T2
  * FLAIR
* 155 slices per patient
* Total images: **57,195**
* Image size: **240 × 240**

Dataset Split:

| Dataset    | Patients | Slices |
| ---------- | -------: | -----: |
| Training   |      258 | 25,397 |
| Validation |       55 |  8,525 |
| Test       |       56 |  8,680 |

---

## Data Preprocessing

The following preprocessing techniques were applied before training:

* Min-Max Normalization
* Two-stage Gaussian Filtering
* Histogram Equalization
* Z-score Normalization

Only slices containing tumors, along with a limited number of empty slices, were retained to reduce class imbalance.

---

## Feature Extraction

The model uses both image information and handcrafted features.

### MRI Modalities

* T1
* T1ce
* T2
* FLAIR

### Global Features

* Major Axis Length
* Size
* Area
* Perimeter
* Roundness

### Statistical Features

* Mean
* Standard Deviation
* Variance
* Skewness
* Kurtosis

These features were combined to create a **14-channel input tensor** for the segmentation model.

---

## Data Augmentation

To improve generalization and reduce overfitting, the training data was augmented using:

* Rotations (0°, 90°, 180°, 270°)
* Vertical Flip

This increased the effective training dataset by **8×**.

---

## Model Architecture

The proposed DSCNN-DU-Net consists of:

* Depthwise Separable Convolution (DSConv) blocks
* Encoder-Decoder architecture
* Dense bottleneck block
* Skip Connections
* Bilinear Upsampling
* Final 1×1 Convolution with Sigmoid activation

The network predicts segmentation masks for:

* Enhancing Tumor (ET)
* Tumor Core (TC)
* Whole Tumor (WT)

---

## Loss Function

The model was trained using a hybrid loss function:

* Dice Loss (50%)
* Binary Cross-Entropy Loss (50%)

This combination improves overlap accuracy while addressing severe class imbalance.

---

## Evaluation Metrics

The model was evaluated using:

* Mean Dice Coefficient
* Dice Score (ET)
* Dice Score (TC)
* Dice Score (WT)
* Jaccard Index (IoU)
* Sensitivity
* Specificity
* Pixel Accuracy

---

## Training Configuration

* Optimizer: Adam
* Learning Rate: 0.0001
* Batch Size: 16
* Epochs: 50
* Learning Rate Scheduler: ReduceLROnPlateau

The project was developed and trained using **Google Colab (T4 GPU)**.

---

## Technologies Used

* Python
* TensorFlow
* Keras
* OpenCV
* NumPy
* Pandas
* Matplotlib
* Scikit-learn
* Google Colab

---

## Repository Structure

```text
Brain-Tumor-Segmentation/
│
├── Brain_Tumor_Segmentation.ipynb
├── README.md
├── requirements.txt
├── LICENSE
├── .gitignore
├── images/
└── outputs/
```

---

## Installation

```bash
git clone https://github.com/your-username/Brain-Tumor-Segmentation.git
cd Brain-Tumor-Segmentation
```

Install the required libraries:

```bash
pip install tensorflow keras opencv-python nibabel numpy pandas matplotlib scikit-learn scipy
```

---

## Usage

1. Download the BraTS 2020 dataset.
2. Open the notebook in Google Colab or Jupyter Notebook.
3. Install the required dependencies.
4. Run the notebook to preprocess the data, train the model, and generate segmentation masks.

---

## Future Work

* Train on larger computational resources for additional epochs.
* Evaluate on newer BraTS datasets.
* Develop a web-based interface for MRI segmentation.
* Improve segmentation accuracy through further architecture optimization.

---

## References

* BraTS 2020 Dataset
* TensorFlow
* Keras
* Brain Tumor Segmentation using Optimized Depthwise Separable Convolutional Neural Network with Dense U-Net

---

## Authors

**M. Roja Lakshmi**

**Sarada Prasanna Behera**

**Satyendar Kumar**

Department of Computer Science and Engineering

National Institute of Technology Andhra Pradesh

---

⭐ If you found this project useful, consider giving it a star.

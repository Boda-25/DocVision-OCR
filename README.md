# 🧠 DocVision OCR

### End-to-End Intelligent Handwritten Optical Character Recognition System

DocVision OCR is an end-to-end Computer Vision and Deep Learning project for recognizing handwritten text from word-level images.

The project explores multiple OCR approaches, starting with a traditional OCR baseline and progressing through a custom deep learning experiment to a pretrained Transformer-based OCR model.

---

## 🚀 Project Overview

The system follows a complete OCR pipeline:

```text
IAM Handwriting Dataset
        ↓
Exploratory Data Analysis
        ↓
Data Cleaning
        ↓
Image Preprocessing
        ↓
Tesseract Baseline
        ↓
CRNN + CTC Experiment
        ↓
Pretrained TrOCR
        ↓
Model Evaluation
        ↓
Visualization & Error Analysis
        ↓
Interactive OCR Dashboard
        ↓
Custom Image Inference
```

The main objective is to investigate how different OCR approaches perform on handwritten word recognition and build a practical inference pipeline.

---

## 📊 Dataset

The project uses the **IAM Handwriting Word Database**.

Dataset source:

**Kaggle:**
https://www.kaggle.com/datasets/nibinv23/iam-handwriting-word-database

Dataset statistics used in the project:

* Original annotation records: **44,564**
* Clean samples: **44,531**
* Removed samples: **33**
* Writers: **28**
* Unique transcriptions: **7,433**
* Character vocabulary: **76 characters**

The dataset contains handwritten word images together with their corresponding transcriptions.

> The dataset itself is not included in this repository.

---

## 🧹 Data Cleaning

The dataset was inspected and cleaned before model training and evaluation.

The cleaning process included:

* Image existence validation
* Image readability validation
* Image dimension validation
* Metadata extraction
* Writer ID extraction
* Aspect-ratio analysis
* Removal of corrupted or invalid samples

After cleaning:

```text
44,564 → 44,531 valid samples
```

---

## 🖼️ Image Preprocessing

Images are converted to grayscale and resized while preserving their original aspect ratio.

The preprocessing pipeline uses:

* Target height: **64 pixels**
* Target width: **256 pixels**
* Aspect-ratio preserving resize
* Centered white canvas
* Pixel normalization to `[0, 1]`

The resulting representation is compatible with the deep learning OCR pipeline.

---

# 🤖 OCR Approaches

## 1. Tesseract OCR Baseline

Tesseract was used as a traditional OCR baseline to establish a reference point for handwritten word recognition.

The baseline demonstrates the challenges of applying traditional OCR directly to handwritten text.

---

## 2. CRNN + CTC

A custom **Convolutional Recurrent Neural Network (CRNN)** was implemented using:

```text
CNN
 ↓
BiLSTM
 ↓
Linear Layer
 ↓
CTC
```

The experiment was designed to investigate an end-to-end neural OCR architecture.

During experimentation, the model showed **CTC blank-collapse behavior** during general training.

Additional diagnostics were performed to verify:

* Input images
* Encoded labels
* CTC tensor shapes
* Gradient flow
* Single-sample memorization behavior

The CRNN experiment was therefore kept as an experimental stage rather than being presented as the final model.

---

## 3. TrOCR

The final OCR experiment uses:

**`microsoft/trocr-small-handwritten`**

TrOCR is a Transformer-based OCR architecture designed for handwritten text recognition.

The model was used as a **pretrained model** without fine-tuning in this project.

Model parameters:

```text
~61.6M parameters
```

---

# 📈 TrOCR Evaluation

The final TrOCR benchmark was evaluated on:

```text
3,734 test samples
```

### Results

| Metric                     |     Result |
| -------------------------- | ---------: |
| Exact Word Accuracy        | **54.50%** |
| Character Error Rate (CER) | **0.3525** |
| Word Error Rate (WER)      | **0.4550** |

### Metric Definitions

**Exact Word Accuracy**

Percentage of samples where the predicted word exactly matches the reference word.

**Character Error Rate (CER)**

Measures character-level edit distance between the reference and predicted text.

**Word Error Rate (WER)**

Measures word-level recognition errors.

---

# 📊 Visualization & Error Analysis

The notebook includes visual analysis of the OCR predictions, including:

* TrOCR performance overview
* Ground-truth vs prediction examples
* Correct predictions
* Incorrect predictions
* Character-level recognition errors
* Spacing and segmentation errors
* Final inference demonstrations

Example:

```text
Ground Truth : Gaitskell
Prediction   : Gaits hell
Status       : Incorrect
```

This demonstrates an observed spacing/segmentation-type recognition error.

---

# 🖥️ Interactive OCR Dashboard

DocVision OCR also includes an interactive dashboard built directly inside the notebook environment.

The dashboard allows users to:

* Select handwriting samples
* Run TrOCR inference
* View the input image
* Compare Ground Truth with the prediction
* Identify correct/incorrect predictions
* View model performance metrics

---

# 📤 Custom Image OCR

The project also includes a custom inference interface where users can upload a handwriting image and run OCR on it.

```text
Upload Image
     ↓
TrOCR Processor
     ↓
TrOCR Model
     ↓
Generated Text
```

The predicted text is displayed directly below the uploaded image.

---

# 🛠️ Technologies

* Python
* PyTorch
* Hugging Face Transformers
* TrOCR
* Tesseract OCR
* OpenCV
* NumPy
* Pandas
* Matplotlib
* PIL
* IPyWidgets
* Jupyter / Kaggle Notebooks

---

# 📂 Repository Structure

```text
DocVision-OCR/
│
├── DocVision_OCR.ipynb
├── requirements.txt
├── .gitignore
└── README.md
```

The IAM dataset and pretrained model weights are intentionally not stored in this repository.

---

# ▶️ How to Run

The easiest way to reproduce the project is through Kaggle.

##

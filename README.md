# Breast Ultrasound Lesion Segmentation and Diagnosis

This project uses two diff models for:

1. **Image segmentation** → predicts lesion mask, with a
2. **Classifier** → predicts diagnosis (**normal / benign / malignant**) using the predicted mask

---

## Demo
![Demo](Images/Demo_1.gif)


## Dataset

**Breast Ultrasound Images Dataset (BUSI)**  
https://www.kaggle.com/datasets/aryashah2k/breast-ultrasound-images-dataset

### Dataset Structure

```
DATASET_ROOT/
├── benign/
│   ├── image.png
│   ├── image_mask.png
├── malignant/
│   ├── image.png
│   ├── image_mask.png
├── normal/
│   └── image.png
```
![Data](Images/Data.png)
Notes:
- Masks exist mostly for benign and malignant
- Normal class is treated as **empty mask**

## Segmentation Results:
![Results](Images/Results_1.png)

## Classifier Results
### Model Performance
The classifier achieves an overall **accuracy of 80%** across 160 evaluated cases.

#### Summary Metrics

| Class | Samples | Correctly Identified | Recall | Precision |
| :--- | :---: | :---: | :---: | :---: |
| **Normal** | 27 | 27 / 27 | 100% | 93% |
| **Benign** | 91 | 84 / 91 | 92% | 77% |
| **Malignant** | 42 | 17 / 42 | 40% | 77% |

#### Confusion Matrix 

This matrix compares the true labels against what the model predicted:

| Actual \ Predicted | Predicted Normal | Predicted Benign | Predicted Malignant |
| :--- | :---: | :---: | :---: |
| **Actual Normal** | **27** (correct) | 0 | 0 |
| **Actual Benign** | 2 | **84** (correct) | 5 |
| **Actual Malignant** | 0 | **25** (false negative) | **17** (correct) |

The results indicate that the malignant class suffers from low recall, whereas the benign class performs significantly better. Notably, the confusion matrix reveals 25 false negatives where malignant cases were incorrectly predicted as benign

## Repository Structure

```
Breast_Cancer_Detection_Deep_Learning/
├── Images/
├── ├── Data.png
├── ├── Demo.gif
├── ├── Results_1
├── ├── Results_2
├── Trained_Weights/
│   └── readme.md - Download Models weights from here(Google Drive)
├── notebook/
├── ├── Breast_Cancer_Detection_Deep_Learning.ipynb
├── src/
│   ├── init.py
│   ├── classifier_model.py
│   ├── config.py
│   ├── data.py
│   ├── gui_app.py
│   ├── infer.py
│   ├── losses.py
│   ├── train_classifier.py
│   ├── train_unet.py
│   ├── unet_model.py
├── Requirements.txt
└── README.md
```


---

## Installation

### 1. Clone repository
```
git clone https://github.com/Gokulos/Breast-Ultrasound-Lesion-Segmentation-Diagnosis-U-Net-Mask-Aware-Classifier.git
cd Breast-Ultrasound-Lesion-Segmentation-Diagnosis-U-Net-Mask-Aware-Classifier
```
### 2.Create a Virtual Environment(Optional)
```
python -m venv busi
source busi/bin/activate        # Linux / Mac
busi\Scripts\activate         # Windows
```
### 3. Install Requirements
```
pip install -r Requirements.txt
```

## Method Overview
```
Segmentation (U-Net)

- Encoder–decoder CNN with skip connections
- Predicts binary lesion mask
- Trained using BCE + Dice loss
- Evaluated using Dice coefficient

Classification

Classifier input: (original ultrasound image, predicted lesion mask)

Outputs: (Normal, Benign, Malignant)
```
---


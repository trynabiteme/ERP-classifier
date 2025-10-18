# EEG-based ERP Signal Classification for Target and Non-Target Detection

This repository contains the code and documentation for a project focused on classifying target and non-target signals in EEG data using machine learning models. The goal of this project is to compare the performance of multiple classification models, including **Nearest Class Centroid (NCC)**, **Linear Discriminant Analysis (LDA)**, **Regularized LDA (RLDA)**, and **Logistic Regression**, applied to EEG data that corresponds to different stimuli markers. The aim is to classify brain responses in real-time for applications such as brain-computer interfaces (BCI) and cognitive state monitoring.

## Project Overview

The project implements several machine learning models to classify **target** and **non-target** events based on EEG responses:

- **Target**: Brain activity in response to a target stimulus.
- **Non-Target**: Brain activity in response to a non-target stimulus.

This project aims to understand the subtle differences in brain activity induced by different stimuli and develop a robust classifier that can distinguish these states effectively. These findings could have applications in fields such as cognitive monitoring and BCI systems for real-time mental state detection.

## Dataset

- **Source**: EEG data from a BrainVision `.vhdr` file.
- **Data Description**: The dataset contains EEG recordings from multiple channels that capture brain activity in response to different stimulus markers. These recordings are pre-processed to extract events corresponding to target and non-target stimuli.
- **Channels**: The EEG data consists of multiple channels, including frontal, parietal, and occipital regions.
- **Class Imbalance**: The dataset exhibits some imbalance between the target and non-target classes, which required handling during model training.

## Key Challenges and Solutions

### 1. **Class Imbalance**
   - **Problem**: The dataset contained more non-target responses than target responses, leading to class imbalance.
   - **Solution**: Techniques such as **undersampling** of the majority class and **class weight adjustments** were used to balance the dataset and improve model performance on the minority class (target).

### 2. **Feature Extraction**
   - **Problem**: EEG data is high-dimensional, making it computationally expensive to process.
   - **Solution**: **Principal Component Analysis (PCA)** was applied to reduce the dimensionality of the feature space, retaining 93% of the variance, which sped up training and improved model efficiency.

### 3. **Noise and Artifacts**
   - **Problem**: Raw EEG data often includes noise and artifacts, which can negatively affect model accuracy.
   - **Solution**: A **band-pass filter** (1–40 Hz) was applied to the data to remove irrelevant frequencies and ensure cleaner signals for classification.

### 4. **Distinguishing Subtle Differences**
   - **Problem**: The difference between target and non-target signals can be subtle, making classification challenging.
   - **Solution**: Several machine learning models were tested, and **LDA** and **RLDA** showed the best performance for distinguishing between these subtle signal differences.

## Methods

### Preprocessing Steps:
- **Noise Filtering**: A **band-pass filter** was applied to retain only the relevant EEG frequency ranges.
- **Feature Scaling**: The EEG data was normalized using **StandardScaler** to ensure that all features were on a comparable scale.
- **Dimensionality Reduction**: **PCA** was applied to reduce the number of features, improving computational efficiency and mitigating overfitting.
- **Class Balancing**: Techniques such as **undersampling** of the majority class were used to balance the target and non-target classes during training.

### Machine Learning Models:
- **Nearest Class Centroid (NCC)**
- **Linear Discriminant Analysis (LDA)**
- **Regularized Linear Discriminant Analysis (RLDA)**
- **Logistic Regression**

### Performance Metrics:
Models were evaluated using the **ROC AUC score** to measure classification performance, particularly focusing on distinguishing between target and non-target classes.

## Results

| Model                     | Target AUC | Non-Target AUC | Avg AUC |
|---------------------------|------------|----------------|---------|
| NCC                       | 0.572      | 0.563          | 0.592   |
| LDA                       | 0.826      | 0.826          | 0.825   |
| RLDA                      | 0.835      | 0.835          | 0.835   |
| Logistic Regression (LogReg)| 0.755      | 0.755          | 0.749   |

The **RLDA** model outperforms the other models, achieving the highest average AUC score of **0.835**.

## Discussion

- **NCC** showed moderate performance in distinguishing between target and non-target classes, with **spatio-temporal** features providing the best results.
- **LDA** and **RLDA** demonstrated strong classification accuracy, particularly in the **spatial** and **temporal** domains.
- **Logistic Regression** performed reasonably well but did not match the classification performance of LDA and RLDA.

## Limitations and Future Work

- **Data Limitations**: The dataset is limited in terms of **participant diversity**, and **missing sessions** or EEG channels may affect generalizability.
- **Feature Set**: While PCA was used for dimensionality reduction, future work could explore additional features, such as **spectral power** and **connectivity measures**, to enhance model performance.
- **Deep Learning**: Future research could incorporate **deep learning** techniques, such as **Convolutional Neural Networks (CNNs)** or **Recurrent Neural Networks (RNNs)**, to better capture the temporal and spatial dependencies in EEG data.

# EEG Seizure Classification Using Signal Processing and Machine Learning

## Overview

This project investigates the classification of EEG recordings associated with epileptic seizure activity and other neurological states/artifacts using signal processing and machine learning techniques. This project combines exploratory data analysis, frequency-domain extraction, and RandomForestClassifier to evaluate the clinical usefulness of EEG-derived features for distinguishing between seizure and non-seizure brain states.

A core focus of this project is demonstrating that clinically motivated feature engineering outperforms raw time-series classification. 

----------------------------------------
# Medical Context

Epilepsy affects millions of people worldwide, making it one of the most prevalent neurological disorders. Accurate and rapid identification of seizure activity from EEG recordings are critical for:
* Clinical Diagnosis - distinguishes seizure from non-epileptic events
* Real time monitoring - detecting seizure onset in ICU and ambulatory settings
* Surgical Planning - identifying epileptogenic zones in pre-surgical evaluation
* Treatment assessment - evaluating antiepileptic drug efficacy 

Manual EEG review by trained neurologists is time-intensive and subject to inter-rater variability. Automated machine learning classification offers a pathway toward faster, more consistent seizure detection

----------------------------------------
# Key Findings

* Seizure activity achieved 98% recall, demonstrating strong separability of ictal recordings from all non-seizure states
* FFT band power features alone achieved 73.96% test accuracy which outperformed both raw EEG time points (57.8%) and various amplitude features (60.9%)
* All 9 combined features achieved 76.3% test accuracy with an 7.96% generalization gap, confirming amplitude and frequency features are complimentary
* Adding raw EEG to FFT features reduced test accuracy from 73.96% to 73.5% while also having a higher generalization gap (11.7%) suggesting potential noise that hurts overall performance
* Seizure recordings showed broadband power elevation across all 5 frequency bands which is consistent with the neural hyperactivation characteristic of ictal activity
* Tumor and Healthy area recordings showed less than 2% band power distribution difference, explaining the primary classification challenge between 2 and 3

----------------------------------------
# Dataset: UCI Machine Learning Repository Epileptic Seizure Recognition Dataset

Contains:

* 11,500 total EEG recordings
* 178 time points per second per sample
* 5 original classes
* 2300 samples per class
* 500 individuals, 23 chunks (seconds) each
  
----------------------------------------
# Class Descriptions

1 - Seizure activity

2 - Non-Seizure activity (Tumor region)

3 - Non-Seizure activity (Healthy region)

4 - Non-Seizure activity (Eyes closed)

5 - Non-Seizure activity (Eyes open)

----------------------------------------
# Project Workflow

* Data Cleaning & Validation

* EEG Waveform Visualization (All 5 Classes)

* Bandpass filtering (0.5-40 Hz)

* Feature Extraction

* Power Spectral Density Analysis

* Random Forest Classification (5 Model Comparison)

* Model Evaluation - Confusion Matrix, Feature Importance, Statistical Significance

----------------------------------------
# Signal Processing

Bandpass Filtering
* A 4th order bandpass filter (0.5-40 Hz) was applied to isolate clinically relevant brain rhythms while removing
        * Sub 0.5 Hz baseline drift and electrode movement artifacts
        * Above 40 Hz muscle (EMG) contamination and 60 Hz power line interference

The filter was validated by comparing a raw vs filtered signals and quantifying the difference by comparing raw vs filtered signals and quantifying the mean difference, confirming the dataset contains unwanted noise artifacts which is useful to reduce before feature extraction. 

Frequency Band Definitions
* Delta - 0.5-4 Hz
* Theta - 4-8 Hz
* Alpha - 8-13 Hz
* Beta - 13-30 Hz
* Gamma 30-40 Hz 

----------------------------------------
# Feature Engineering

9 Total Extracted Features - Clinical Relevancy

* Average Amplitude - Signal
* Variance - Signal Variability - Elevated in seizure
* Root Mean Square Amplitude - Signal Power (More sensitive than mean)
* Dominant Frequency (Welch PSD peak) - Primary brain rhythm frequency
* Delta Power (FFT mean power 0.5-4 Hz) - Slow wave activity
* Theta Power (FFT mean power 4–8 Hz) - Ictal oscillations
* Alpha Power (FFT mean power 8–13 Hz) - Resting rhythm
* Beta Power (FFT mean power 13–30 Hz) - Active state marker
* Gamma Power (FFT mean power 30–40 Hz) - High frequency bursts

----------------------------------------
# Power Spectral Biological Interpretation 

<img width="1189" height="2227" alt="Power Spectral Density by EEG Classification" src="https://github.com/user-attachments/assets/bbd64fef-455c-4a7e-9c0f-9f8c4b21d78a" />

## Normalized Band Power distribution
________________________
Seizure
* Delta - 27.0%
* Theta - 47.3%
* Alpha - 18.0%
* Beta - 7.4%
* Gamma - 0.3%

Non-Seizure (Tumor Area)
* Delta - 72.9%
* Theta - 19.1%
* Alpha - 6.9%
* Beta - 1.0%
* Gamma - 0.1%

Non-Seizure (Healthy Area)
* Delta - 71.3%
* Theta - 20.1%
* Alpha - 7.1%
* Beta - 1.3%
* Gamma - 0.2%

Non-Seizure (Eyes Closed)
* Delta - 26.7%
* Theta - 14.1%
* Alpha - 51.6%
* Beta - 7.1%
* Gamma - 0.4%

Non-Seizure (Eyes Open)
* Delta - 54.4%
* Theta - 19.7%
* Alpha - 19.3%
* Beta - 6.0%
* Gamma - 0.7% 

________________________

For Seizure EEG recordings, Theta dominant at 47.3% which is consistent with ictal theta oscillations during focal seizure onset. Crucially, seizure recordings showed the highest absolute power 5 bands compared to every other class that was a broadband power elevation consistent with the neural hyperactivation characteristic of ictal activity.

For EEG Classified Non-Seizure Tumor Area and Healthy Area, both classes show near-identical relative band power distributions (delta ~72%, theta ~20%, alpha ~7%, beta ~1.2%), differing by less than 2% across all bands. However, tumor area recordings show consistently higher absolute power, consistent with chronic cortical hyperexcitability of epileptogenic tissue. This magnitude-without-shape-difference is the primary source of misclassification between these classes.  


Eyes Closed — Alpha dominant at 51.6%, directly confirming the Berger effect — the well-documented emergence of alpha rhythm upon eye closure first described by Hans Berger in 1929.

Eyes Open — Alpha suppressed to 19.3% compared to 51.6% in eyes closed, representing a 32.3% alpha power reduction consistent with alpha blocking (alpha desynchronization) driven by visual cortex activation.


Seizure activity is highly distinguishable from the other EEG neurological states. Furthermore, the Non-seizure states are also distinguishable from each other. 

----------------------------------------
# Machine Learning (RandomForestClassifier)
## Model Comparison Results

Raw 178 Time Points 
* Training Accuracy - 64.58%
* Testing Accuracy - 57.83%
* Gap - 6.75%

4 Extracted Features
* Training Accuracy - 71.22%
* Testing Accuracy - 60.87%
* Gap - 10.36%

5 FFT Band Powers
* Training Accuracy - 83.05%%
* Testing Accuracy - 73.96%
* Gap - 9.09%

Raw EEG & FFT Band Powers
* Training Accuracy - 85.29%
* Testing Accuracy - 73.52%
* Gap - 11.77%

All 9 Features (4 + FFT)
* Training Accuracy - 84.26%
* Testing Accuracy - 76.30%
* Gap - 7.96%


## Best Model Performance - All 9 Features

* Train Accuracy - 84.26%
* Test Accuracy - 76.30%
* Generalization Gap - 7.96%
* CV Method - 5-Fold Stratified

## Per Class Performance 

* Seizure
- Precision - 95%
- Recall - 98%
- F-1 Score - 96%
- Support - 465

* Non-Seizure (Tumor Area)
- Precision - 64%
- Recall - 55%
- F-1 Score - 59%
- Support - 459

* Non-Seizure (Healthy Area)
- Precision - 64%
- Recall - 68%
- F-1 Score - 66%
- Support - 450

* Non-Seizure (Eyes Closed)
- Precision - 84%
- Recall - 78%
- F-1 Score - 81%
- Support - 457

* Non-Seizure (Eyes Open)
- Precision - 73%
- Recall - 82%
- F-1 Score - 77%
- Support - 469

## Feature Importance (5-Fold CV)

Mean FFT Band Powers collectively accoutned for the largest share of model decision making, confirming that frequency domain decomposition captures more clinically meaningful information than time-domain amplitude statistics alone.


----------------------------------------
# Visualizations

## EEG Waveforms

Example waveforms from each class showing differences in amplitude and temporal behavior. (Including sample mean)

<img width="1389" height="2045" alt="image" src="https://github.com/user-attachments/assets/b5b14ec4-e783-45af-ae3a-95a21c70b0eb" />


## Frequency vs Amplitude Scatter Plot (2d vs 3d)

<img width="1189" height="790" alt="Dominant Frequency over Avg Amplitude" src="https://github.com/user-attachments/assets/7d6a27c6-b3bb-40b4-9dce-1a7bf85af609" />

<img width="969" height="989" alt="image" src="https://github.com/user-attachments/assets/73e6dc33-ceb2-4cea-b5a2-ced39e77306a" />

Comparison of dominant frequency and average amplitude across all classes.

Dominant Frequency Ranges by Class
=============================================
Seizure
  Range : 2.78 Hz — 16.69 Hz
  Mean  : 6.01 Hz
---------------------------------------------
Tumor Area (non-seizure)
  Range : 2.78 Hz — 8.34 Hz
  Mean  : 3.84 Hz
---------------------------------------------
Healthy Area (non-seizure)
  Range : 2.78 Hz — 11.12 Hz
  Mean  : 3.48 Hz
---------------------------------------------
Eyes Closed (non-seizure)
  Range : 2.78 Hz — 19.47 Hz
  Mean  : 10.65 Hz
---------------------------------------------
Eyes Open (non-seizure)
  Range : 2.78 Hz — 25.03 Hz
  Mean  : 7.79 Hz
---------------------------------------------

Dominant Frequency ranges by class represent clear highlights and struggles when analyzing the performance of the ML through the confusion matrix. Non-Seizure Tumor Area and Healthy Area had the most mistakes when classifying those two specifically due to similar data and features. When looking at Dominant Freq. Range Tumor/Healthy area are almost identical especially with the same mean frequency. 
* Dominant Freq. Range, Mean Freq. and FFT Data all show similarity in data and thus overlap when classyfing Tumor/Healthy

Seizure signals tend to have different frequency characteristics compared to the Non-Seizure classifications and this is shown through the 98% recall from the ML with classifying seizures. Furthermore, in accordance with theta dominant bands shown in the plotted FFT data, the mean dominant frequency for seizures are 6.01 Hz which further solidifies seizure theta dominant activity.

The 2D model shows significant overlap over many of the classes in terms of dominant frequency.
The 3D models also shows overlap, however while also displaying the power disparity between seizure and non seizure classifications which further demonstrate hyperactivity in seizure EEG recordings.




## Bandpass Filter

<img width="1389" height="1180" alt="image" src="https://github.com/user-attachments/assets/7e03e455-f59a-4f66-a7c1-605315a9ad47" />

## Model Comparison

<img width="1289" height="590" alt="image" src="https://github.com/user-attachments/assets/c3ee7240-d7c8-4541-925d-99dd2addd4ab" />

## Confusion Matrix

<img width="742" height="590" alt="image" src="https://github.com/user-attachments/assets/6b071bf5-cce3-4c62-b1c3-d675f65c4b6d" />

## Feature Importance Report

<img width="1089" height="590" alt="image" src="https://github.com/user-attachments/assets/0744ad2b-0d02-4b9e-bb60-b57f02c49a06" />


----------------------------------------
# Limitations

## Class 2 / Class 3 Separability

Tumor area and healthy area recordings exhibited near-identical relative band power distributions with less than 2% difference across all frequency bands. The primary discriminator between these classes is the absolute signal magnitude rather than frequency composition which shows a distinction that is difficult to capture reliably at 1 second recording resolution across multiple patients with different baseline amplitudes. 

## Single Dataset Generalization

All results are from a single publicly available dataset. Real world EEG classification systems must account for inter-subject variability, (Shown in standard deviations from Mean Power Band distribution by class) electrode placement differences, and recording equipment variation. None of which are represented in this dataset's controlled conditions.

## 1 Second Recording Window

Each sample represents exactly 1 second of EEG. Seizure dynamics evolve over seconds to minutes which is a longer temporal window with sliding analysis would likely improve classification and better reflect clinical monitoring conditions.

## Patient Level Validation

Standard train/test splitting does not prevent data leakage between recordings from the same patient. A leave-one-subject-out cross validation would provide a more honest estimate of generalization to new patients

----------------------------------------
# Future Work

## Immediate Next Steps 
* Add total spectral power as a 10th feature to directly capture absolute magnitude differences between tumor and healthy area recordings
* Implement leave-one-subject-out cross validation to assess true patient level generalization

## Signal Processing Extensions
* Utilize Discrete Wavelet Transform for time-frequency localization and captures non-stationary EEG dynamics that FFT cannot
* Calculating Spectral Entropy for analyzing ictal/interictal/normal segments and improving ML classifier performance

## Machine Learning Extension
* Compare RandomForest against SVM and XGBoost
* Explore 1D CNN directly on raw EEG time series

----------------------------------------
# Skills Demonstrated

## Data Science

Data cleaning, validation, and integrity checking
Exploratory data analysis on clinical signal data
Statistical analysis with cross-validated significance testing
Multi-class imbalance assessment

## Signal Processing

EEG waveform visualization and interpretation
Butterworth bandpass filter design and validation
Welch Power Spectral Density estimation
FFT-based frequency band power extraction
Time-domain and frequency-domain feature engineering

## Machine Learning

Random Forest classification with constrained hyperparameters
5-model feature engineering progression study
Overfitting detection and mitigation
5-fold stratified cross-validation
Confusion matrix and per-class performance analysis
Feature importance with statistical significance (±1 std dev)

## Computational Neuroscience Interpretation

* EEG interpretation
* Seizure detection concepts
* Neural signal characterization
* Brain-state classification

## Professional Application

* Working with real-world EEG data
* Interpreting noisy biological signals
* Feature extraction from neural recordings
* Building machine learning workflows
* Communicating technical findings through visualizations



----------------------------------------
# Requirements

Package/Purpose
* numpy - Numerical computations and arrays
* pandas - Data loading and manipulation
* matplotlib - Plotting EEG waveforms and scatter plots
* scipy - Signal processing and Feature analysis
* scikit-learn - RandomForestClassifier and evaluation metrics
* seaborn - Confusion matrix heatmap

----------------------------------------
# How to Run

This project was developed and run in **Google Colab**.

## 1. Download the dataset
Download `Epileptic Seizure Recognition.csv` from Kaggle:
[UCI Epileptic Seizure Recognition Dataset](https://www.kaggle.com/datasets/harunshimanto/epileptic-seizure-recognition)

## 2. Open the notebook in Google Colab
- Go to [Google Colab](https://colab.research.google.com)
- Select **File -> Upload notebook** and upload `EEG_Analysis_Notebook.ipynb` 

## 3. Upload the dataset
Each time you connect to a new Colab runtime, upload the CSV:
from google.colab import files
* Select `Epileptic Seizure Recognition.csv` when prompted.

## 4. Run all cells
Runtime -> Run all

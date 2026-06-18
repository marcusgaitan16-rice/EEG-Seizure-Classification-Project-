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

* Seizure activity acheived 98% recall, demonstrating strong seperability of ictal recordings from all non-seizure states
* FFT band power features alone acheived 74.0% test accuracy which outperformed both raw EEG time points (57.8%) and various amplitude features (60.9%)
* All 9 combined features achieved 76.3% test accuracy with an 9.0% generalization gap, confirming amplitude and frequency features are complimentary
* Adding raw EEG to FFT features reduced test accuracy from 74.0% to 73.5% while also having a higher generalization gap (11.7%) suggesting potential noise that hurts overall performance
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
* Gamma - 0.7%%

________________________

For Seizure EEG recordings, Theta dominant at 47.3% which is consistent with ictal theta oscillations during focal seizure onset. Crucially, seizure recordings showed the highest absolute power 5 bands compared to every other class — a broadband power elevation consistent with the neural hyperactivation characteristic of ictal activity.

For EEG Classified Non-Seizure Tumor Area and Healthy Area, both classes show near-identical relative band power distributions (delta ~72%, theta ~20%, ), differing by less than 2% across all bands. However, tumor area recordings show consistently higher absolute power, consistent with chronic cortical hyperexcitability of epileptogenic tissue. This magnitude-without-shape-difference is the primary source of misclassification between these classes.

Eyes Closed — Alpha dominant at 51.6%, directly confirming the Berger effect — the well-documented emergence of alpha rhythm upon eye closure first described by Hans Berger in 1929.

Eyes Open — Alpha suppressed to 19.3% compared to 51.6% in eyes closed, representing a 32.3% alpha power reduction consistent with alpha blocking (alpha desynchronization) driven by visual cortex activation.

----------------------------------------

Skills Demonstrated

Data Science

* Data cleaning
* Exploratory Data Analysis (EDA)
* Feature engineering
* Statistical analysis
* Data visualization
* EEG waveform interpretation
* Amplitude analysis
* Frequency-domain analysis
* Dominant frequency extraction
* Time-series visualization



Machine Learning

* Train/test splitting
* Feature scaling
* Random Forest Classification
* Model evaluation
* Confusion matrix analysis

Computational Neuroscience Interpretation

* EEG interpretation
* Seizure detection concepts
* Neural signal characterization
* Brain-state classification

Professional Application

* Working with real-world EEG data
* Interpreting noisy biological signals
* Feature extraction from neural recordings
* Building machine learning workflows
* Communicating technical findings through visualizations

----------------------------------------

Requirements

Package/Purpose


numpy - Numerical computations and arrays

pandas - Data loading and manipulation

matplotlib - Plotting EEG waveforms and scatter plots

scipy - Signal processing and Feature analysis

scikit-learn - RandomForestClassifier and Model Evaluation

----------------------------------------

Visualizations

EEG Waveforms

Example waveforms from each class showing differences in amplitude and temporal behavior.

<img width="1389" height="2045" alt="Example Waveforms 5-Classifications" src="https://github.com/user-attachments/assets/544dc877-a3e5-4461-930d-82204926716a" />

----------------------------------------

Frequency vs Amplitude Scatter Plot

<img width="1189" height="790" alt="Dominant Frequency over Avg Amplitude" src="https://github.com/user-attachments/assets/7d6a27c6-b3bb-40b4-9dce-1a7bf85af609" />

----------------------------------------

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

Frequency Analysis Shows

* Seizure signals tend to have different frequency characteristics
* Certain classes overlap
* Frequency information contains signal

----------------------------------------

Confusion Matrix and Classification Report

Class

Seizure - 96%

Tumor Region - 56%

Healthy Region - 56%

Eyes Closed - 75%

Eyes Open - 67%

* Random Forest achieved 70.17% overall accuracy across five EEG classes.
* Seizure activity was identified with 96% recall, indicating strong separability from non-seizure states.
* Classes 2 and 3 exhibited substantial overlap, resulting in frequent misclassification.
* Eyes Open and Eyes Closed recordings also showed moderate overlap.
* These findings suggest seizure activity possesses distinctive EEG characteristics that can be effectively captured by machine learning models.

----------------------------------------
Current Status

* In Progress

* Still need to add hyperparamters and then rerun confusion matrix
* Add Features - Avg Amplitude, Variance, RMS Amplitude, Dominant Frequency
* Make a feature importance plot
* Stack features to ML
* 

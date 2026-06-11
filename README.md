# EEG-Seizure-Classification-Project-

Overview

This project investigates EEG recordings from the UCI Epileptic Seizure Recognition Dataset. The goal is to explore neural activity patterns, visualize seizure-related signals, extract signal features, and develop machine learning models capable of classifying EEG recordings into seizure and non-seizure categories.

----------------------------------------

Objectives

* Analyze EEG time-series data
* Visualize seizure and non-seizure brain activity
* Extract signal characteristics
* Explore frequency-domain behavior
* Train machine learning classifiers
* Evaluate classification performance
* Interpret model outputs for neuroscience applications

----------------------------------------

Dataset: UCI Epileptic Seizure Recognition Dataset

Contains:

* 11,500 EEG recordings
* 178 time points per sample
* 5 original classes
* EEG activity collected from multiple subjects

----------------------------------------

Class Descriptions

1 - Seizure activity

2 - Non-Seizure activity (Tumor region)

3 - Non-Seizure activity (Healthy region)

4 - Non-Seizure activity (Eyes closed)

5 - Non-Seizure activity (Eyes open)

----------------------------------------

Skills Demonstrated

Data Science

* Data cleaning
* Exploratory Data Analysis (EDA)
* Feature engineering
* Statistical analysis
* Data visualization

Signal Processing

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

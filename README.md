# ECG-Based Stress Detection using Heart Rate Variability (HRV)

## Project Overview

This project demonstrates an end-to-end pipeline for detecting stress from Electrocardiogram (ECG) signals using Heart Rate Variability (HRV) features and machine learning classification. The pipeline covers data loading, signal preprocessing, HRV feature extraction using a sliding window approach, and training various machine learning models to classify stress vs. baseline states.

## Features

-   **Data Loading**: Supports loading the WESAD dataset (specifically `S2.pkl`) or generating synthetic ECG data if the WESAD file is not available.
-   **ECG Preprocessing**: Cleans ECG signals and detects R-peaks using `neurokit2`.
-   **HRV Feature Extraction**: Extracts time-domain and frequency-domain HRV features (e.g., `HRV_MeanNN`, `HRV_SDNN`, `HRV_RMSSD`, `HRV_LF`, `HRV_HF`, `HRV_LFHF`) from sliding windows of ECG data.
-   **Machine Learning Classification**: Trains and evaluates popular classification algorithms (Logistic Regression, Random Forest, SVM) to distinguish between baseline and stress conditions.
-   **Feature Importance Visualization**: Visualizes the importance of HRV features using Random Forest insights.
-   **Physiological Interpretation**: Provides a brief interpretation of HRV changes during stress.

## Methodology

1.  **Data Acquisition**: ECG signals and labels are loaded either from the WESAD `S2.pkl` file or synthetically generated to mimic baseline and stress states.
2.  **Preprocessing**: The raw ECG signal is cleaned using NeuroKit2's `ecg_clean` function, and R-peaks are detected to calculate inter-beat intervals (NN intervals).
3.  **Feature Extraction**: A sliding window approach is applied to the cleaned ECG data. For each window, if it falls entirely within a 'Baseline' or 'Stress' labeled segment, HRV features are extracted. Windows containing mixed labels are skipped.
4.  **Machine Learning**: The extracted HRV features serve as input to classification models. The data is split into training and testing sets, features are scaled, and models are trained and evaluated.
5.  **Evaluation**: Model accuracy, precision, recall, and F1-score are reported for each classifier.
6.  **Feature Importance**: Random Forest's feature importance mechanism is utilized to identify the most discriminative HRV features.

## Models Used

-   **Logistic Regression**
-   **Random Forest Classifier**
-   **Support Vector Machine (SVM)** with RBF Kernel

## Key Findings (Synthetic Data Example)

With synthetic data designed to clearly separate baseline and stress conditions, the models often achieve high accuracy. For real-world WESAD data, performance may vary, reflecting the complexity and variability of physiological signals.

**Physiological Interpretation:**

*   Stress typically leads to **LOWER HRV** (e.g., decreased SDNN, RMSSD).
*   Stress generally **increases LF power** (sympathetic activity) and **decreases HF power** (parasympathetic activity).
*   Consequently, the **LF/HF ratio usually INCREASES** during stress.

## Dependencies

The following Python libraries are required:

-   `numpy`
-   `pandas`
-   `scikit-learn`
-   `neurokit2`
-   `matplotlib`
-   `pickle`

Install them using pip:

```bash
pip install numpy pandas scikit-learn neurokit2 matplotlib
```

## How to Run

1.  **Clone the repository** (if applicable).
2.  **Install dependencies** as listed above.
3.  **Obtain WESAD `S2.pkl` file** (if you want to use real data) and place it in the project directory, or the script will automatically generate synthetic data.
4.  **Run the Python script/Jupyter Notebook** (e.g., in Google Colab). The script will execute the full pipeline from data loading to model evaluation and visualization.

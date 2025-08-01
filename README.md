# Emotion Detection Using Non-EEG Physiological Signals

This project focuses on detecting emotional states (`calm` vs `stress`) using **non-invasive biosignals** collected from wearable sensors. The dataset is derived from wrist-worn devices that capture signals like electrodermal activity (EDA), heart rate (HR), temperature, and acceleration.

---

## Dataset

**Source**: [PhysioNet - Non-EEG Dataset for Assessment of Neurological Status](https://physionet.org/content/noneeg/get-zip/1.0.0/)  
**Signals Used**:
- `EDA` (Electrodermal Activity)
- `HR` (Heart Rate)
- `SpO2` (Oxygen Saturation)
- `TEMP` (Skin Temperature)
- `ax`, `ay`, `az` (3-axis Accelerometer)

---

## Objective

To process and classify the **physiological responses** of subjects into emotional states:
- First half of each recording: `calm`
- Second half of each recording: `stress`

---

## Method

### 1. Data Loading
- Loaded files using the `wfdb` library.
- Each subject has two recordings: one for EDA+Accel+Temp, one for HR+SpO2.

### 2. Signal Preprocessing
- Applied **Savitzky-Golay filter** (`window=51`, `polyorder=3`) to smooth:
  - `EDA`, `HR`, `SpO2`, `TEMP`, `ax`, `ay`, `az`
  
### 3. Labeling
- First half of samples → `'calm'`
- Second half → `'stress'`
- `subject_id` tag added for tracking

### 4. Feature Extraction
- Sliding window of size `1000`
- For each window:
  - Aggregated stats: `mean`, `std`, `min`, `max`
  - Flattened feature vector
  - Assigned most frequent label in the window
### 5. Data preprocessing
- Filled missing values with mean
- Scaled X values

### 6. Final Dataset
- Created a structured `X_df` containing features + labels
### 7. Model training
- Performed scaling on X features
- Implemented 5 models ( 1D CNN, SVM, Random forest, KNN, logical regression )
- Evaluated models and summarized results.
---

## Visualization
Following is the distribution of calm and stress labels
<img width="789" height="586" alt="image" src="https://github.com/user-attachments/assets/64463101-4734-4f8f-86ff-0a20f1a513df" />


Plotted **EDA signal (first 500 samples)** for calm vs stress across subjects.
<img width="1376" height="279" alt="image" src="https://github.com/user-attachments/assets/bbc0a644-0320-4c05-b68b-a4cf322651c7" />

<img width="1381" height="529" alt="image" src="https://github.com/user-attachments/assets/2a794c50-303c-4867-af2a-3f80f8a369a2" />

<img width="1398" height="558" alt="image" src="https://github.com/user-attachments/assets/1816cbc9-030f-4ef8-8afd-929274282119" />

<img width="1161" height="641" alt="image" src="https://github.com/user-attachments/assets/0d3ebe02-93bb-476c-8981-153e2a9e3d4a" />

<img width="479" height="645" alt="image" src="https://github.com/user-attachments/assets/861c7f35-a75c-4a8a-935e-c9109fbcf651" />





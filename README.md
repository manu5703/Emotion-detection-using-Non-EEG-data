# Emotion Detection Using Non-EEG Physiological Signals

This project focuses on detecting emotional states (`calm` vs `stress`) using **non-invasive biosignals** collected from wearable sensors. The dataset is derived from wrist-worn devices that capture signals like electrodermal activity (EDA), heart rate (HR), temperature, and acceleration.

---

## Dataset

**Source**: [PhysioNet - Non-EEG Dataset for Assessment of Neurological Status](https://physionet.org/)  
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

## Methods

### 1. Data Loading
- Loaded `.dat`, `.hea`, and `.atr` files using the `wfdb` library.
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

### 5. Final Dataset
- Created a structured `X_df` containing features + labels
- Also returned `y_series` and `all_data_df` for downstream tasks

---

## Visualization

- Plotted **EDA signal (first 500 samples)** for calm vs stress across subjects.
```python
plt.plot(calm_sub['EDA'][:500], label='Calm')
plt.plot(stress_sub['EDA'][:500], label='Stress')

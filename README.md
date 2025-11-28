# Predictive Maintenance for Hydraulic Systems

## Project Overview
This project aims to develop a predictive maintenance system for a hydraulic test rig using machine learning techniques. By analyzing sensor data (pressure, temperature, vibration, etc.), the system predicts the health status of various components (Cooler, Valve, Pump, Accumulator) to enable proactive maintenance and reduce downtime.

## Dataset
The dataset consists of sensor readings from a hydraulic test rig, collected under various operating conditions.
- **Source**: [UCI Machine Learning Repository - Condition Monitoring of Hydraulic Systems](https://archive.ics.uci.edu/ml/datasets/Condition+monitoring+of+hydraulic+systems)
- **Sensors**: 14 physical sensors (Pressure, Motor Power, Volume Flow, Temperature, Vibration, Efficiency, Cooling Efficiency).
- **Targets**: 4 component conditions (Cooler, Valve, Pump, Accumulator) and 1 stable flag.
- **Sampling Rate**: Sensors are sampled at different rates (1Hz, 10Hz, 100Hz).

## Methodology

### 1. Data Preprocessing
- **Resampling**: All sensor data is resampled to a common frequency (1Hz) to align timestamps.
- **Stable Flag Filtering**: Only data collected during stable operating conditions (`Stable_Flag = 1`) is used for training to ensure data quality and remove transient noise.
- **Feature Engineering**: Statistical features (Mean, Std, Min, Max, Skewness, Kurtosis) are extracted from sensor cycles.
- **Data Cleaning**: Missing values and NaNs generated during feature extraction (e.g., skewness of constant signals) are filled with 0.

### 2. Feature Selection
- **Virtual Sensors Exclusion**: Virtual sensors (CE, CP, SE) are excluded from the input features as they are derived from the target variables and would cause data leakage.
- **Physical Sensors**: Only the 14 physical sensors (PS1-PS6, EPS1, FS1-FS2, TS1-TS4, VS1) are used.

### 3. Model Development
- **Handling Imbalance**: SMOTE (Synthetic Minority Over-sampling Technique) is applied to the training data to address class imbalance in the target variables.
- **Scaling**: `StandardScaler` is used to normalize features. It is fit on the training set and applied to the test set to prevent data leakage.
- **Algorithm**: Logistic Regression (One-vs-Rest) is used as the baseline model for multi-class classification.

## Results
The current implementation focuses on predicting **Internal Pump Leakage**. The model achieves high accuracy in classifying the pump's condition into three states:
- **0**: No leakage
- **1**: Weak leakage
- **2**: Severe leakage

*Note: The dataset contains labels for other components (Cooler, Valve, Accumulator), but these are left for future work.*

## Usage
1. **Run Notebook**: Open `Predictive-Maintenance-for-Hydraulic-Systems-NEW.ipynb` in Google Colab and run the cells.
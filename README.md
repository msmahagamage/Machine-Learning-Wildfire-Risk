# Comparative Analysis of Wildfire Prediction Models

## 1. Project Overview

This repository contains a Python script that trains, evaluates, and compares four different machine learning models for the task of wildfire classification. Using a dataset of environmental and geospatial variables, the script determines whether a location is likely to experience a fire.

The models implemented are:
1.  **Logistic Regression**
2.  **Decision Tree (DT)**
3.  **Random Forest (RF)**
4.  **Support Vector Machine (SVM)**

The script automates the entire workflow from data loading and preprocessing to model training, evaluation, and visualization of the results.

---

## 2. Dataset

The script is designed to work with a single Excel file (`FireDataset_Modify3.xlsx`) which should contain the following features and a target variable. 

* **Predictor Features:** `temperatureMean`, `ndviMean`, `slope`, `elevation`, `Dis_Water`, `Dis_Road`, `population`, `windspeed`, `evaporation`, `precipitation`.
1.  **Raw Fire History Data**: The initial vector data for historical fire perimeters in California was downloaded from the **Fire and Resource Assessment Program (FRAP)**.
    * **Source**: [FRAP GIS Data Page](https://frap.fire.ca.gov/mapping/gis-data/)

2.  **Geospatial Feature Extraction**: The raw fire data, along with a corresponding set of non-fire locations, was processed using a custom Google Earth Engine (GEE) script. This script sampled various raster datasets to extract all the environmental, climatic, and topographic variables (e.g., NDVI, LST, precipitation, elevation). The GEE script and its methodology can be found in the following repository:
    * **GEE Script Repository**: [GEE-extract_fire_variables](https://github.com/msmahagamage/GEE-extract_fire_variables.git)

* **Target Variable:** `fire` (a categorical label indicating the class, e.g., 0 for 'No Fire' and 1 for 'Fire').

---

## 3. Methodology

The script follows a standard machine learning pipeline:

1.  **Data Loading:** Reads the dataset from an Excel file using `pandas`.
2.  **Exploratory Data Analysis (EDA):** Generates a boxplot to visualize the distribution of the input features.
3.  **Preprocessing:**
    * **Stratified Train-Test Split:** The data is split into training (70%) and testing (30%) sets while preserving the original ratio of fire/non-fire samples.
    * **Feature Scaling:** The features are standardized using `StandardScaler` to ensure all variables contribute equally to model performance.
4.  **Model Training & Evaluation:** Each of the four models is trained on the scaled training data.
5.  **Performance Analysis:** The performance of each trained model is evaluated on the unseen test data using a comprehensive set of metrics:
    * Overall Accuracy, Cohen's Kappa, and F1-Score.
    * A detailed Classification Report (Precision, Recall, F1-Score per class).
    * A visualized Confusion Matrix.
    * Feature Importance scores to understand which variables are most influential.

---

## 4. How to Use This Script

### Requirements
You need Python 3 installed, along with the following libraries. You can install them all by running:
`pip install pandas scikit-learn matplotlib seaborn openpyxl`

### Setup & Execution
1.  Place your Excel dataset (e.g., `FireDataset_Modify3.xlsx`) in the same directory as the Python script.
2.  **Modify the script** to load the file directly, instead of using a hardcoded absolute path.
    * **Change this line:**
        ```python
        file = r'C:\Users\Madusha.MahaGamage\Downloads\Fire Dataset\FireDataset_Modify3.xlsx'
        ```
    * **To this:**
        ```python
        file = 'FireDataset_Modify3.xlsx'
        ```
3.  Run the script from your terminal:
    ```bash
    python train_models.py
    ```
4.  The script will print all the evaluation metrics and display the plots for each model.

---

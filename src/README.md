# 🌾 AgriPak – Low-Yield Risk Prediction Using Machine Learning

## 📌 Project Overview

AgriPak is a machine learning-based project designed to identify the risk of relatively low agricultural crop yield using historical agricultural data.

The project analyzes crop type, geographical location, agricultural season, cultivated area, and historical yield information to develop a classification model that predicts whether an agricultural record belongs to the low-yield-risk category.

Three machine learning algorithms are implemented and compared: Logistic Regression, Random Forest, and XGBoost.

The selected XGBoost model achieved **78.67% accuracy and 56.56% F1-score** on the 2025 test dataset.

## 🎯 Objectives

- Collect and analyze agricultural data.
- Perform data preprocessing and cleaning.
- Identify relatively low-yield records using crop-specific thresholds.
- Develop machine learning classification models.
- Compare different algorithms.
- Tune the classification threshold.
- Evaluate the selected model using unseen test data.
- Visualize the results using graphs.

## 📂 Dataset Description

The dataset contains **140,000 records and 8 columns**.

### Dataset Features

| Feature | Description |
|---|---|
| state | State name |
| lga | Local Government Area |
| crop | Crop type |
| season | Agricultural season and year |
| area_ha | Cultivated area in hectares |
| yield_t_ha | Crop yield in tonnes per hectare |
| production_t | Total crop production |
| quality_grade | Crop quality category |

### Crop Types

- Yam
- Cassava
- Sorghum
- Rice
- Oil Palm
- Cocoa
- Millet
- Maize

### Target Variable

The project creates a binary target called `low_yield_risk`.

- `0` – No Low Yield Risk
- `1` – Low Yield Risk

A separate 25th-percentile yield threshold is calculated for each crop using training-period data. This defines relative low yield within each crop, rather than an official agricultural risk standard.

## ⚙️ Technologies Used

- Python 3.11
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Matplotlib
- Seaborn
- Joblib
- Git and GitHub
- Visual Studio Code

## 🧹 Data Preprocessing

The following preprocessing steps are performed:

1. Load the agricultural dataset.
2. Check missing values and data types.
3. Extract the year from the season column.
4. Extract the season type (wet or dry).
5. Calculate crop-specific low-yield thresholds using training data.
6. Create the `low_yield_risk` target variable.
7. Select relevant input features.
8. Exclude harvest outcome variables from model inputs to reduce data leakage.
9. Split the data according to year.

### Selected Input Features

- State
- LGA
- Crop
- Season Type
- Year
- Cultivated Area

## 🧠 Machine Learning Algorithms

### 1. Logistic Regression

A supervised classification algorithm used to estimate the probability of low-yield risk.

### 2. Random Forest

An ensemble learning algorithm that combines multiple decision trees to improve classification performance.

### 3. XGBoost

A gradient-boosting algorithm that builds decision trees sequentially to improve prediction performance.

## 🔬 Methodology

The project follows these stages:

1. Dataset Collection
2. Data Loading and Understanding
3. Data Preprocessing
4. Target Variable Creation
5. Feature Selection
6. Time-Based Data Splitting
7. Model Training
8. Model Comparison
9. Threshold Tuning
10. Final Model Evaluation
11. Result Visualization

### Dataset Splitting

| Dataset | Year | Records |
|---|---|---:|
| Training | 2022–2023 | 80,052 |
| Validation | 2024 | 39,807 |
| Testing | 2025 | 20,141 |
| **Total** | | **140,000** |

Note: The 2025 test dataset contains wet-season records only.

## 📊 Model Comparison

The following table shows the best validation results after threshold tuning.

| Algorithm | Accuracy | Precision | Recall | F1-score |
|---|---:|---:|---:|---:|
| Logistic Regression | 78.04% | 56.79% | 55.28% | 56.03% |
| Random Forest | 78.80% | 59.34% | 51.61% | 55.20% |
| XGBoost | 78.26% | 57.31% | 55.18% | **56.23%** |

**Selected Model: XGBoost**

**Selected Threshold: 0.30**

XGBoost achieved the highest validation F1-score among the evaluated models and was selected for final testing.

## 🏆 Final Test Results

The selected XGBoost model was evaluated on the 2025 test dataset.

| Evaluation Metric | Score |
|---|---:|
| Accuracy | 78.67% |
| Precision | 57.66% |
| Recall | 55.51% |
| F1-score | 56.56% |

### Confusion Matrix

| | Predicted No Risk | Predicted Low Risk |
|---|---:|---:|
| Actual No Risk | 13,048 | 2,054 |
| Actual Low Risk | 2,242 | 2,797 |

### Result Interpretation

- Correctly classified 13,048 no-risk records.
- Correctly identified 2,797 low-yield-risk records.
- Incorrectly identified 2,054 no-risk records as low risk.
- Missed 2,242 actual low-yield-risk records.

## 📈 Project Visualizations

The project generates three graphs:

1. Model Comparison
2. Final XGBoost Performance
3. Confusion Matrix

All graphs are saved in:

`reports/figures/`

### Graph Files

- `model_comparison.png`
- `final_performance.png`
- `confusion_matrix.png`

## 📁 Project Structure

```text
AgriPak-Low-Yield-Risk-Prediction/
│
├── data/
│   ├── raw/
│   │   └── nigerian_agriculture_seasonal_crop_yields.csv
│   │
│   └── processed/
│       ├── train.csv
│       ├── validation.csv
│       ├── test.csv
│       ├── best_model_config.json
│       ├── test_predictions.csv
│       └── final_evaluation_metrics.json
│
├── src/
│   ├── data_loading.py
│   ├── prepare_data.py
│   ├── leakage_check.py
│   ├── baseline.py
│   ├── random_forest.py
│   ├── xgboost_model.py
│   ├── threshold_tuning.py
│   ├── final_evaluation.py
│   └── create_visualizations.py
│
├── reports/
│   └── figures/
│       ├── model_comparison.png
│       ├── final_performance.png
│       └── confusion_matrix.png
│
├── notebooks/
│
├── requirements.txt
├── .gitignore
└── README.md
```

*Note: This is the intended project structure. Some generated files may be excluded from Git using `.gitignore`.*

## 💻 Installation and Execution

### Step 1: Clone the Repository

```bash
git clone https://github.com/Shaikalfiya548/AgriPak-Low-Yield-Risk-Prediction.git
```

### Step 2: Open the Project Folder

```bash
cd AgriPak-Low-Yield-Risk-Prediction
```

### Step 3: Install Required Libraries

```bash
python -m pip install -r requirements.txt
```

### Step 4: Prepare the Dataset

Ensure the original CSV dataset is placed inside:

```text
data/raw/
```

Run:

```bash
python src/data_loading.py
python src/prepare_data.py
```

### Step 5: Train the Models

```bash
python src/baseline.py
python src/random_forest.py
python src/xgboost_model.py
```

### Step 6: Tune the Classification Threshold

```bash
python src/threshold_tuning.py
```

### Step 7: Perform Final Evaluation

```bash
python src/final_evaluation.py
```

### Step 8: Generate Graphs

```bash
python src/create_visualizations.py
```

## ⚠️ Limitations

- The dataset does not contain weather conditions such as rainfall and temperature.
- Soil properties and irrigation information are not available.
- The low-yield target is defined using crop-specific historical yield thresholds.
- The 2025 test dataset contains only wet-season records.
- The model is an experimental classification system and should not be treated as a validated real-world agricultural forecasting service.

## 🚀 Future Scope

- Include rainfall and temperature data.
- Add soil moisture and soil pH information.
- Include fertilizer and irrigation details.
- Collect more historical agricultural records.
- Evaluate performance across more years and seasons.
- Develop a user-friendly web application.
- Improve prediction performance using additional features and model tuning.

## 🎓 Conclusion

AgriPak demonstrates how machine learning can be used to analyze historical agricultural data and classify records according to their relative low-yield risk.

Three machine learning algorithms were implemented and compared. XGBoost achieved the highest validation F1-score and was selected for final evaluation.

The final test results show 78.67% accuracy and a 56.56% F1-score on 2025 data.

This project provides a foundation for further research into agricultural risk classification using machine learning.

## 👩‍💻 Author

**Shaik Iqra Alfiya**

Computer Science and Engineering Graduate

GitHub: [Shaikalfiya548](https://github.com/Shaikalfiya548)

---

⭐ If you find this project useful, consider giving the repository a star!
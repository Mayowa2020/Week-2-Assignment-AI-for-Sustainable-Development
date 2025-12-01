# Integrating Machine Learning with the United Nations SDGs

## 🦠 Disease Outbreak Predictor (SDG 3 — Good Health & Well-Being)

### 🎯 Project Overview

This project demonstrates how machine learning can contribute to the United Nations Sustainable Development Goal 3 (SDG 3) — Good Health and Well-Being.
It implements a supervised learning model that predicts the number of dengue cases based on historical and environmental data. Early predictions can help health authorities allocate resources effectively, enabling timely interventions to prevent widespread outbreaks.

### 📘 Table of Contents

1. Background

2. Objectives

3. Dataset

4. Project Structure

5. Methodology

6. Model Development

7. Evaluation Metrics

8. Ethical Considerations

9. Results & Visualization

10. How to Run Locally

11. Technologies Used

12. Future Enhancements

13. References

### 1. Background

Vector-borne diseases such as dengue fever cause major public health challenges in tropical regions. Predicting potential outbreaks before they occur can enable governments and NGOs to deploy preventive measures and save lives.

This project uses historical climate and epidemiological data to predict weekly dengue case counts for regions such as San Juan and Iquitos.

### 2. Objectives

Develop a supervised regression model to predict upcoming dengue cases.

Demonstrate the role of AI in advancing SDG 3: Good Health & Well-Being.

Build an interpretable model using open-source datasets.

Evaluate model performance with meaningful metrics and visualizations.

### 3. Dataset

Recommended open datasets to use (download separately):

Kaggle — Dengue Disease Prediction Dataset

(DengAI: Predicting Disease Spread

Links shown below:

<https://www.kaggle.com/code/klmsathishkumar/dengai-predicting-disease-spread/input?select=dengue_features_train.csv>

<https://www.kaggle.com/code/klmsathishkumar/dengai-predicting-disease-spread/input?select=dengue_labels_train.csv>

)

📂 The datasets includes variables include features such as temperature, rainfall, humidity, NDVI vegetation indices, and weekly case counts for locations like San Juan and Iquitos. (Use dengue_features_train.csv and dengue_labels_train.csv when available.)

### 4. Project Structure

📁 dengue-disease-outbreak-predictor
│
├── data/
│   ├── dengue_features_train.csv
│   └── dengue_labels_train.csv
│
├── dengue_disease_outbreak_predictor.ipynb  # Main Jupyter Notebook (Model & Analysis)
├── dengue_disease_outbreak_predictor.py     # Standalone script version (optimized)
├── rf_disease_model.joblib                  # Trained Random Forest model
├── README.md                                # Project documentation
├── PERFORMANCE_OPTIMIZATIONS.md             # Performance improvements guide
├── article.md                               # Project article
└── .gitignore                               # Git ignore patterns

### 5. Methodology

        1. Data Preprocessing
       
           - Steps included in the script:

            Import CSV files (dengue_features_train.csv, dengue_labels_train.csv).

           - Merge features and labels on region and week/date.  
           - Handle missing values: impute numeric columns with median and categorical with mode; where appropriate, use forward‑fill for time series features per region.
           - Create lag features for previous dengue case counts.
           - Generate time-based (sin/cos) seasonal features.
         
        2. Feature Engineering

           - Combine meteorological, NDVI, and lag features:
           Lag features for previous 1, 2, 4, 8 weeks of case counts.
           - Rolling statistics: mean, std of prior N weeks.
           - Temporal features: week of year, month.
           - Interaction features: rainfall × temperature, NDVI lag.

        3. Model Training

            - Baseline: Linear Regression, Decision Tree.

            - Final Model: Random Forest Regressor (with tuned hyperparameters).

        4. Model Evaluation

           - Split data chronologically (train on earlier weeks, test on later ones).

           - Train/test split:
           Time‑aware split (train on earlier dates, test on later dates) to avoid leakage.

           - Scaling: not required for tree models; used if employing linear or neural models.

           - Evaluate using MAE, RMSE, and R² Score.

### 6. Model Development

The primary model is a Random Forest Regressor trained on weekly aggregated data.
Tree-based methods were chosen for their robustness, non-linear feature handling, and interpretability.

Example hyperparameters:

RandomForestRegressor(
    n_estimators=200,
    max_depth=12,
    random_state=42,
    n_jobs=-1
)

### 7.

| Metric       | Description                  | Purpose                                     |
| ------------ | ---------------------------- | ------------------------------------------- |
| **MAE**      | Mean Absolute Error          | Measures average prediction error magnitude |
| **RMSE**     | Root Mean Squared Error      | Penalizes larger deviations                 |
| **R² Score** | Coefficient of Determination | Explains variance captured by the model     |

### 8. Ethical Considerations

Data Bias: Incomplete or under-reported cases may bias predictions in low-resource regions.

Fairness: Model should complement, not replace, expert epidemiological judgment.

Privacy: All data used is aggregated and publicly available.

Sustainability: The lightweight model can be deployed on modest computing resources.

### 9. Results & Visualization

Visualizations include:

Actual vs. Predicted dengue case plots

Feature importance rankings

Example output:

MAE: 6.28
RMSE: 9.73
R²: 0.86

The model successfully captures outbreak patterns with strong predictive accuracy.

### 9.1 Performance Optimizations

The codebase has been optimized for better performance and efficiency:

- **90%+ faster startup**: Removed runtime pip install overhead
- **70-80% faster data preprocessing**: Vectorized median imputation
- **40-50% faster feature engineering**: Optimized lag feature creation
- **33% overall execution time reduction**: From ~30s to under 3s

For detailed information about the optimizations, see [PERFORMANCE_OPTIMIZATIONS.md](PERFORMANCE_OPTIMIZATIONS.md).

### 10. How to Run Locally

🧩 Prerequisites

Ensure Python 3.9+ is installed.

⚙️ Setup Instructions

```bash
# Clone this repository
git clone https://github.com/Mayowa2020/Week-2-Assignment-AI-for-Sustainable-Development.git
cd Week-2-Assignment-AI-for-Sustainable-Development

# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # (Windows: venv\\Scripts\\activate)

# Install dependencies
pip install pandas numpy scikit-learn matplotlib joblib

# Run the optimized script
python dengue_disease_outbreak_predictor.py
```

**Note:** The script has been optimized for performance. Dependencies are no longer installed at runtime, improving startup time by 90%+.

### 11. Technologies Used

Python

pandas, NumPy — Data processing

scikit-learn — Machine learning algorithms

matplotlib — Visualization

joblib — Model serialization

### 12. Recent Improvements

✅ **Performance Optimizations** — Vectorized operations reduce execution time by 33%

✅ **Code Quality** — Removed runtime overhead and unused imports

✅ **Portability** — Fixed file paths for cross-platform compatibility

✅ **Documentation** — Added comprehensive performance optimization guide

### 13. Future Enhancements

🔹 Integrate LightGBM/XGBoost for better performance.

🔹 Add real-time data ingestion using APIs or IoT devices.

🔹 Build a Streamlit dashboard for interactive visualization.

🔹 Extend to multi-disease modeling (e.g., malaria, chikungunya).

🔹 Include quantile regression for uncertainty estimation.

### 14. Reference

Kaggle — DengAI: Predicting Disease Spread

✨ Acknowledgements

Developed as part of an academic assignment exploring AI for Sustainable Development, demonstrating the power of machine learning to enhance global health outcomes.

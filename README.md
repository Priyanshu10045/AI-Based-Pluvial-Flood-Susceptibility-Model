# AI-Based Pluvial Flood Susceptibility Model

## Overview

This project presents an AI-based model for assessing pluvial (inland) flood susceptibility, leveraging various geospatial and hydrological features. The primary goal is to demonstrate a robust methodology for flood risk assessment, highlighting critical steps such as data cleaning, feature engineering, and spatial cross-validation. A key aspect of this project is the diagnostic analysis of label quality, simulating real-world scenarios where observed flood data might be noisy or derived from an index.

## Features

- **Comprehensive Data Preprocessing:** Handles `NoData` sentinels, imputes missing values, and prepares features for machine learning.
- **Advanced Feature Engineering:** Creates new features like `log_FA`, `aspect_sin/cos`, `slope_twi`, and `curv_abs` to capture complex spatial relationships.
- **Label Quality Diagnosis:** Critically examines the nature of susceptibility labels, revealing potential issues (e.g., deterministically derived indices vs. observed data).
- **Realistic Label Simulation:** Introduces controlled noise to labels to simulate real-world data imperfections and provide more honest performance estimates.
- **Spatial Block Cross-Validation:** Employs a rigorous spatial cross-validation strategy to prevent geographic data leakage and ensure model generalization.
- **Multiple Model Benchmarking:** Compares the performance of various machine learning algorithms, including RandomForest, GradientBoosting, LogisticRegression, and XGBoost.
- **Detailed Evaluation Metrics:** Provides accuracy, F1-score (macro), confusion matrices, and feature importance analysis.
- **Interactive Visualizations:** Generates plots for class distribution, F1-score comparison, confusion matrix, feature importance, and missing data.
- **SHAP Interpretability (Optional):** Includes SHAP (SHapley Additive exPlanations) for model interpretability, if the `shap` library is installed.
- **Prediction Export:** Exports model predictions and probabilities to a CSV file for further analysis or integration.

## Dataset

The model is trained on the "Pluvial Flood Dataset" which contains various environmental factors (`Slope`, `Curvature`, `Aspect`, `TWI`, `FA`, `Drainage`, `Rainfall`) and a `SUSCEP` (Susceptibility) index.

**Note on `SUSCEP` labels:** The initial analysis reveals that the `SUSCEP` index is deterministically derived from the `Drainage` feature, leading to artificially high model performance. This notebook simulates realistic noisy labels (`target_noisy`) to provide a more truthful evaluation of predictive power in a real-world context.

## Setup and Installation

To run this project, you'll need Python and the following libraries. It's recommended to use a virtual environment.

```bash
# Clone the repository (once uploaded to GitHub)
# git clone <your-repo-link>
# cd <your-repo-name>

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

# Install the required packages
pip install numpy pandas scikit-learn matplotlib seaborn xgboost shap openpyxl
```

## Usage

Download the Dataset: Place the Pluvial_Flood_Dataset.xlsx file in the project's root directory or update the DATA_PATH variable in the notebook.
Run the Jupyter/Colab Notebook: Execute the cells sequentially in the pluvial_flood_prediction.ipynb notebook (or similar name).
Explore Results: The notebook will generate several plots (flood_model_evaluation.png, flood_shap_importance.png) and a CSV file (flood_predictions.csv) containing the model's predictions.

## Key Steps in the Notebook:

- STEP 1: Load and inspect data.
- STEP 2: Diagnose label quality (identifying the deterministic nature of SUSCEP).
- STEP 3: Clean NoData values.
- STEP 4: Perform feature engineering.
- STEP 5: Create a realistic noisy label simulation.
- STEP 6: Set up spatial block cross-validation.
- STEP 7: Train and evaluate models with original and noisy labels.
- STEP 8: Train a final model on a geographic holdout fold.
- STEP 9: Generate comprehensive evaluation plots.
- STEP 10: (Optional) Generate SHAP feature importance plots.
- STEP 11: Save predictions.

## Results and Insights

Models achieve near-perfect accuracy with the original SUSCEP labels due to their deterministic nature.
With simulated realistic (noisy) labels, the best models achieve approximately 78-79% accuracy and macro-F1 scores, providing a more reliable estimate of real-world performance.
Spatial cross-validation is crucial for models dealing with spatially autocorrelated data to avoid overly optimistic performance estimates.
Feature engineering significantly enhances model performance.

## Future Work

Integrate actual observed flood event data instead of a susceptibility index.
Explore advanced deep learning architectures for geospatial data.
Incorporate additional features such as soil type, land cover, and detailed elevation derivatives.
Expand spatial cross-validation to 10 folds for even more robust evaluation.

## Contributing

Contributions are welcome! Please feel free to open issues or submit pull requests.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgements

Kaggle community for the original dataset and inspiration.
Scikit-learn, Pandas, NumPy, Matplotlib, Seaborn, XGBoost, and SHAP libraries for providing essential tools.

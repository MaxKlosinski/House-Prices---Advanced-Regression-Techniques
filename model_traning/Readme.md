# 🏠 House Prices Prediction - Model Training Pipeline

## 1. Project Overview

This module is responsible for training the regression model (XGBoost) to predict real estate prices. The process relies on data previously processed in the *Feature Engineering* module. The main goal is to minimize the RMSE (Root Mean Squared Error) on values that have been normalized using the logarithmic method through hyperparameter optimization.

## 2. Technologies Used

**Model Engine:** XGBoost (Extreme Gradient Boosting)

  – Selected for its high performance on the data.
  – It is a popular library, which allowed me to find the necessary learning materials more quickly 
 
**Optimization:** Optuna – a framework for automatic hyperparameter tuning.

**Validation:** Scikit-learn (KFold, train_test_split, metrics).

**Analysis:** Pandas, NumPy, Seaborn.

## 3. Validation and Training Strategy

To ensure a reliable evaluation of the model and avoid overfitting on a small dataset, I used the following techniques:

### A. Data Type Processing

Before training, a final data type conversion takes place:

* Categorical variables are cast to the `category` type to take advantage of XGBoost’s native support for data encoding (`enable_categorical=True`).

    * Thanks to XGBoost’s automatic encoding, I didn’t have to perform simple encodings that would have taken up my time without teaching me anything else.

* Specific numeric columns, such as `MSSubClass`, are treated as categorical because their numerical values represent class codes rather than continuous values. This is how the column was described in the document detailing the table data.


### B. Cross-Validation

The **K-Fold Cross-Validation** method was used, dividing the data into 5 parts ().

* **Objective:** Each data sample is used for both training and validation.

**Application:** Within Optune’s objective function, the RMSE error is averaged across the 5 folds, resulting in a more stable metric than a single train/test split.

## 4. Hyperparameter Optimization (Optuna)

The model is fine-tuned using the Optuna library with an SQLite database to store the history of trials. The optimized objective function minimizes the mean RMSE error.

**Key parameters subject to optimization:**

**Tree structure:** `max_depth`, `max_leaves`, `min_child_weight` – control of model complexity.

**Training:** `learning_rate`, `n_estimators` – learning rate and number of trees.

**Regularization:** `reg_alpha` (L1), `reg_lambda` (L2), `gamma` – preventing overfitting.

**Boosting method:** Testing the `gbtree` and `dart` variants.

## 5. Results and Model Interpretation

After optimization is complete, the final model is trained on the full dataset using the best parameters found.

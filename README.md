# House Prices: Advanced Regression Techniques
## I used a dataset from the Kaggle competition: House Prices - Advanced Regression Techniques
## Project Overview
The goal of this project is to create a machine learning model that predicts real estate prices based on a set of diverse features. The project serves as a practical application of regression techniques and feature engineering in Python.

The main challenge was handling a large number of diverse variables (both numerical and categorical) and identifying the key factors influencing a home’s market value.

# Technologies and Tools
The following data science libraries were used in the project:
* Pandas / NumPy: Data manipulation, cleaning, and operations on data frames.
* Scikit-learn: Building regression models, data preprocessing, and validation.
* Matplotlib / Seaborn: Data visualization to understand correlations.
* Jupyter Notebook: A working environment divided into modules to maintain code readability.

# Architecture and Processing Workflow
The project structure was divided into logical stages to facilitate code management:
1. Data Analysis: Analysis of the distribution of the target variable (SalePrice) and checking for skewness in the data. Identification and visualization of correlations between features and price. Detection and removal of outliers that could negatively impact the model.
2. Variable Transformation: Logarithmizing skewed variables to bring their distribution closer to normal.
3. Encoding Categorical Variables: Applying techniques such as One-Hot Encoding or Label Encoding for text data.
4. Creating New Features: Aggregating existing data.
5. Modeling, evaluation, and testing of various regression algorithms. Use of cross-validation to avoid overfitting. Tuning model hyperparameters to optimize the error (minimizing RMSE—Root Mean Squared Error).

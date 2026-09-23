## Loan Approval Prediction
## Project Overview

This project focuses on predicting loan approval decisions using machine learning. The goal was to help loan officers make a more consistent first-stage assessment of loan applications.

I used the CRISP-DM approach to structure the project:

Business Understanding
Data Understanding
Data Preparation
Modelling
Evaluation
Interpretability and Risk

1. Business Understanding

The main objective was to develop a machine learning model that could support the first stage assessment of loan applications.

The project considered different costs for incorrect decisions:

False approval: $50,000
False denial: $8,000

Because the cost of a false approval is higher than the cost of a false denial, I did not rely on accuracy alone when evaluating the models.

The main evaluation metrics were:

Accuracy
Precision
Recall
F1-score
ROC-AUC
Cost-sensitive measure

The target variable, Loan_Approved, is binary because an application is either approved or not approved.

Therefore, classification was used as the main modelling approach, while regression models were also tested as classroom baseline models.

2. Data Understanding

I first explored the dataset to understand its structure, quality, and target variable.

Dataset Summary
20,000 rows
35 columns
0 duplicate rows
2,804 missing values
Target Distribution

The Loan_Approved variable was not evenly distributed:

15,220 not-approved cases (76.1%)
4,780 approved cases (23.9%)

This shows that the dataset has a class imbalance, with more not-approved applications than approved applications.

Exploratory Analysis

I examined:

Numerical variable distributions
Categorical variables and their relationship with the target
Correlations between numerical variables
Pairwise relationships
Statistical associations between variables

This helped me identify patterns in the data and issues that needed to be considered during preprocessing and modelling.

3. Data Preparation

I prepared the data for modelling by cleaning the variables and creating a preprocessing workflow.

The main steps were:

Cleaned the Annual_Income variable.
Separated the predictor variables (X) from the target variable (y).
I dropped variables that are causing data leakage, Risk_Score, Interest_Rate, Base_Interest_Rate and Monthly_Loan_Payment
Created three new financial ratios.
Split the data into 80% training and 20% testing using stratification.
Used median imputation for missing numerical values.
Scaled the numerical variables.
Imputed missing categorical values.
Used one-hot encoding for categorical variables.
Used ColumnTransformer and Pipeline to organize the preprocessing steps and help prevent data leakage.

I also compared mean and median imputation using cross-validation. The results were very similar, so I selected median imputation for the final workflow.

4. Modelling

I tested different machine learning models to determine which models could effectively predict loan approval.

The models included:

2 regression models as baseline models
8 classification models for the main prediction task

The classification models generally performed strongly during cross-validation.

I selected Random Forest for further tuning because:

It can capture non-linear relationships in the data.
It provides feature importance information.
Its individual decision trees can be inspected to better understand the model.

After comparing the models, I used the tuned Random Forest model for the final evaluation.

5. Evaluation
I selected the tuned Logistic Regression  because it is easier to understand than the Random Forest.It performed well on the test data and had a lower estimated business cost than the other strategies.Its performance was fairly consistent across different customer groups.The important features, such as debt-to-income ratio, income, and credit history, also make sense for loan approval.


7. Main Limitation

The model predicts past loan approval decisions, not actual loan defaults.The $8,000 and $50,000 costs are estimates used in this project.The model should be tested with real loan default data before being used.It should also be checked for fairness and possible bias.

Tools and Technologies
Python
Pandas
NumPy
Matplotlib
Seaborn
Scikit-learn
XGBoost
Jupyter Notebook
GitHub

## Conclusion

This project gave me practical experience applying the CRISP-DM process to a classification problem. I worked through data understanding, preprocessing, feature engineering, model comparison, hyperparameter tuning, evaluation, and model interpretation.

The project also showed me the importance of considering class imbalance, business costs, interpretability, and target variable limitations when developing machine learning models.

The tuned Logistic Regression model is  the best performing model in my study, achieving 93.3% accuracy, preession = 87.5% , recall = 83.9% ,  F1-score, = 95.6% and 97.9% ROC-AUC on the test set.

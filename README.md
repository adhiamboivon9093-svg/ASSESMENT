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

The main objective was to develop a machine learning model that could support the first-stage assessment of loan applications.

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

The tuned Random Forest model was evaluated on an unseen test set of 4,000 rows.

Test Set Results
Metric	Result
Accuracy	0.988
Precision	0.966
Recall	0.983
F1-score	0.975
ROC-AUC	0.999
Confusion Matrix

	
Actual Not Approved	3,011	33
Actual Approved	16	940

This means the model made relatively few incorrect predictions on the test data.

Cost-Sensitive Analysis

Using the cost proxy provided in the assignment:

Scenario	Calculated Cost
Random Forest	$1,778,000
Always deny	$7,648,000
Always approve	$152,200,000

These dollar values are scenario-based business-cost proxies and should not be interpreted as actual realised financial losses.

6. Interpretability and Risk

I also examined the feature importance from the Random Forest model to understand which variables were most useful to the model.

Most Important Features
Feature	Importance
Risk_Score	0.377
Loan_To_Annual_Income	0.134
Monthly_Income	0.093
Total_Debt_To_Income_Ratio	0.093
Annual_Income	0.082
Payment_To_Monthly_Income	0.061

These values show how much the model relied on each variable when making predictions. However, feature importance does not mean that a variable causes the loan approval decision.

I also considered differences in model performance across different employment and income groups. Some groups had smaller sample sizes, so subgroup results need to be interpreted carefully.

7. Main Limitation

The most important limitation of this project is the definition of the target variable.

The model predicts historical loan approval decisions, rather than whether a borrower actually defaulted on a loan.

This means:

The model is learning from historical approval decisions.
The $8,000 and $50,000 values are business-cost proxies from the assignment.
These amounts should not be treated as actual financial losses.
The model should not be described as a fully validated loan default-risk model because the dataset does not contain a true loan default outcome.

Therefore, the results should be interpreted as a model for predicting historical loan approval decisions, rather than predicting actual future loan defaults.

Outcome

After comparing and tuning the models, the Random Forest model was selected for the final evaluation.

On the unseen test set, it achieved:

98.8% accuracy
96.6% precision
98.3% recall
97.5% F1-score
99.9% ROC-AUC

The results show strong predictive performance on this dataset. However, the target limitation should be considered when interpreting the model for real-world lending or default-risk applications.

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

The project also showed me the importance of considering class imbalance, business costs, interpretability, and target-variable limitations when developing machine learning models.

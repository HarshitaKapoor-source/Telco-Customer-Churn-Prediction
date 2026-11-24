## Telco Customer Churn Prediction

# Introduction

This project uses a telecommunications customer dataset to predict whether a customer will churn. I compare Logistic Regression and Random Forest, then evaluate their performance on a held-out test set. 

# Dataset

The dataset used in this project is a Kaggle dataset:
 kaggle kernels pull lukhilaksh/telco-customer-88-beats

- **File:** `synthetic_customer_churn_100k.csv`
- **Size:** 100,000 customers and 9 columns
- **Target:** `Churn` (Yes / No). About 1 in 3 customers churn.

# Project Objectives

1. **Churn Prediction**: Build machine learning models that predict which customers are likely to churn.
2. **Data Analysis**: Use exploratory data analysis (EDA) to understand customer behavior and the factors linked to churn.
3. **Model Building**: Train and compare Logistic Regression (baseline) and Random Forest.
4. **Model Evaluation**: Measure the models using accuracy, precision, recall, F1-score and confusion matrices.
5. **Recommendations**: Turn the findings into simple actions the business can take to reduce churn.

# Data Preprocessing

- **Data Quality Checks**: Checked shape, data types, missing values and duplicates. No missing values or duplicates were found.
- **Cleaning**: Removed rows with negative `TotalCharges`, because a bill cannot be negative.
- **Encoding Categorical Variables**: `Gender`, `Contract`, `PaymentMethod` and `Churn` were converted to numbers with label encoding.
- **Dropping Identifiers**: `CustomerID` was removed because it does not help prediction.
- **Train/Test Split**: 80% training and 20% testing, stratified so both parts have the same churn rate.
- **Scaling Numerical Features**: Features were standardized for Logistic Regression. The scaler was fit on training data only to avoid data leakage.

# Exploratory Data Analysis (EDA)

- **Churn Distribution**: How many customers stay versus leave.
- **Numerical Features**: Histograms, box plots and violin plots for age, tenure, monthly charges and total charges, split by churn.
- **Categorical Features**: Churn counts by gender, contract type and payment method.
- **Relationships**: Scatter plots between tenure, charges and churn.

# Model Building

Two models were trained on the same train/test split:

- **Logistic Regression**: A simple, fast baseline model.
- **Random Forest**: An ensemble of decision trees (200 trees) that can learn more complex patterns.

No hyperparameter tuning was done yet.

# Model Evaluation

The models were compared on the 20% test set using accuracy, precision, recall, F1-score and confusion matrices.

| Model | Accuracy | Precision | Recall | F1 |
| Always guess "No churn" (baseline)| 66.93% | | | | 
| Logistic Regression | 72.68% | 0.620 | 0.448 | 0.520 |
| Random Forest | **73.74%** | **0.629** | **0.502** | **0.558** |

Precision, recall and F1 are for the churn class.

- **Accuracy**: how often the model is right overall.
- **Precision**: when the model predicts churn, how often it is correct.
- **Recall**: out of all customers who really churned, how many the model caught.

# Conclusion

- Random Forest performed better than Logistic Regression, but both are only slightly better than always guessing "No churn".
- Both models still miss about half of the customers who actually leave.
- The most important features were **monthly charges, tenure and contract type**. Longer contracts and longer tenure lower the chance of churn, while higher monthly charges raise it.
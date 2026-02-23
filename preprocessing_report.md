Customer Churn Dataset – Preprocessing Report
1. Dataset Overview

Dataset Size: 500 rows × 9 columns

Target Variable: Churn

Feature Types:

Numerical Features

Categorical Features

Binary Features

2. Data Cleaning
2.1 Handling Missing Values

TotalCharges converted to numeric using:

pd.to_numeric(errors='coerce')

Missing values handled using:

Median imputation (numerical features)

Most frequent imputation (categorical features)

2.2 Outlier Detection

Outliers were detected using the IQR (Interquartile Range) method on MonthlyCharges.

Formula Used:
IQR = Q3 - Q1
Lower Bound = Q1 - 1.5 * IQR
Upper Bound = Q3 + 1.5 * IQR

Rows outside this range were removed.

3. Feature Engineering (5+ Features Created)

The following new features were engineered:

Feature Name	Description
AvgMonthlySpend	TotalCharges / (Tenure + 1)
ChargesDifference	TotalCharges − (MonthlyCharges × Tenure)
IsLongTermCustomer	1 if Tenure > 24 months
HighMonthlyCharges	1 if MonthlyCharges > median
SeniorCitizenTenureInteraction	SeniorCitizen × Tenure

These features help improve model learning by capturing behavioral and interaction patterns.

4. Encoding Techniques (3 Methods Applied)
4.1 Label Encoding

Applied on target variable Churn

Converts Yes/No into 1/0

4.2 One-Hot Encoding

Applied to:

PaymentMethod

PaperlessBilling

Prevents ordinal relationship between categories

4.3 Ordinal Encoding

Applied to:

Contract

Logical order used:

Month-to-month < One year < Two year
5. Feature Scaling (2 Techniques Applied)
5.1 StandardScaler

Applied to:

MonthlyCharges

Engineered numerical features

Purpose:

Centers data (mean = 0)

Scales to unit variance

5.2 MinMaxScaler

Applied to:

Tenure

TotalCharges

Purpose:

Scales values between 0 and 1

Preserves distribution shape

6. Preprocessing Pipeline

A complete preprocessing pipeline was built using:

ColumnTransformer

Pipeline

SimpleImputer

StandardScaler

MinMaxScaler

OneHotEncoder

OrdinalEncoder

Pipeline Structure:
Preprocessing Pipeline
│
├── Numerical (StandardScaler)
├── Numerical (MinMaxScaler)
├── OneHot Encoding
└── Ordinal Encoding
7. Final Processed Output

Final processed feature matrix size: (500, 15)

Fully ready for:

Logistic Regression

Random Forest

Gradient Boosting

Any ML model

8. Summary

✔ Missing values handled
✔ Outliers removed
✔ 5+ features engineered
✔ 3 encoding techniques applied
✔ 2 scaling techniques applied
✔ Complete preprocessing pipeline built

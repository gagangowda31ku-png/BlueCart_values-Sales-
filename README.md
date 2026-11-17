BlueCart Values -- Sales Prediction
Project Overview
BlueCart Values -- Sales Prediction is a retail analytics and
machine learning project built around an Excel workbook containing
transaction, customer, marketing, and inventory data. The primary
objective is to explore historical transaction records, prepare the data
for analysis, and develop a regression model that predicts sales values.

The project focuses on an end-to-end workflow: data understanding, data
quality assessment, preprocessing, exploratory data analysis (EDA),
feature engineering, model development, and evaluation.
Target variable: Total_Sales from the Transactions_Raw sheet.

Dataset Description
The source workbook is employability.xlsx. It contains four
worksheets:
  Worksheet                          Records Columns            Description
  Transactions_Raw                     300 Order_ID,        Order-level
Customer_ID,     transaction
Order_Date,      information and
Total_Sales      the sales target

  Customers_Raw                        205 Cust_ID,         Customer details
Customer_Name,   and location
Email, State   

  Marketing_Raw                        150 Campaign_ID,     Marketing
Channel, Date, campaign
Reach, CTR (%) information
Inventory_Raw                        100 SKU,             Product and
Product_Name,    inventory
Stock,           information
Unit_Price
The record counts above exclude each worksheet's header row.
Project Objectives
- Understand the structure and quality of the four datasets.
- Clean missing, inconsistent, and invalid values.
- Standardize date, currency, percentage, and identifier formats where
  appropriate.
- Explore sales distributions and transaction patterns.
- Engineer useful features from transaction data.
- Train regression models to estimate Total_Sales.
- Compare models using appropriate regression metrics.
Data Quality Observations
The original workbook contains data-quality issues that should be
investigated before modeling:
- Transactions_Raw has 67 missing Customer_ID values and 97
  missing Order_Date values.
- Total_Sales contains 36 negative values and 39 zero values. These
  should be investigated as possible returns, adjustments,
  cancellations, or invalid records rather than automatically deleted.
- Transaction dates use inconsistent formats, and examples such as
  2025-13-01 are not valid calendar dates.
- Customers_Raw has 112 missing email values and inconsistent
  capitalization in some state values.
- Marketing_Raw has missing campaign IDs, dates, reach values, and
  CTR values. CTR values also use mixed representations, such as
  percentages and decimals.
- Inventory_Raw has 20 missing SKU values, negative stock values,
  and unit prices represented with different currency symbols and
  formats.
- The customer ID header is written as Cust_ID with a trailing
  space; normalize column names before referencing it in code.
These are observations from the raw workbook, not claims that all issues
have already been corrected.
Sales Prediction Workflow
1. Load the workbook -- Read the required worksheet using Pandas.
2. Inspect the data -- Check dimensions, data types, missing
   values, duplicates, and summary statistics.
3. Clean the data -- Resolve invalid dates, inconsistent formats,
   and missing values using documented business rules.
4. Investigate unusual sales values -- Determine what negative and
   zero sales represent before deciding how to handle them.
5. Perform EDA -- Study the target distribution and sales patterns
   over time where reliable dates are available.
6. Feature engineering -- Derive suitable date features (for
   example, year, month, and day) after validating dates. Use only
   features that would be available at prediction time.
7. Prepare model inputs -- Separate features from Total_Sales,
   split the data into training and test sets, and build preprocessing
   pipelines where needed.
8. Train regression models -- Establish a baseline and compare
   suitable algorithms.
9. Evaluate and interpret -- Compare test-set performance and
   inspect prediction errors.
Suggested Machine Learning Models
The following models are candidates to evaluate; no model performance is
claimed in this README:
- Linear Regression
- Decision Tree Regressor
- Random Forest Regressor
- Extra Trees Regressor
- Gradient Boosting Regressor
- HistGradientBoosting Regressor
- XGBoost or CatBoost, if installed and appropriate
Use cross-validation and hyperparameter tuning only after establishing a
reliable preprocessing and evaluation pipeline.
Evaluation Metrics
- MAE (Mean Absolute Error): Average absolute prediction error.
- MSE (Mean Squared Error): Average squared prediction error.
- RMSE (Root Mean Squared Error): Error measure in the target's
  units.
- R² Score: Proportion of target variance explained by the model.
Compare models on the same held-out test set. Avoid data leakage by
fitting preprocessing steps only on training data.
Technologies
- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- XGBoost / CatBoost (optional)
Getting Started
1. Clone the repository
git clone <your-repository-url>
cd <your-repository-folder>
2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl jupyter
Optional model libraries:
pip install xgboost catboost
3. Place the dataset
Place employability.xlsx in the project data directory, or update the
notebook's file path to match its location.
4. Load the transaction data

import pandas as pd

file_path = "employability.xlsx"

transactions = pd.read_excel(
    file_path,
    sheet_name="Transactions_Raw"
)

print(transactions.head())
print(transactions.info())
print(transactions.isnull().sum())


Important Modeling Considerations
- Total_Sales is the target variable; do not use it as an input
  feature.
- Order_ID is an identifier and should not automatically be treated
  as a predictive feature.
- Missing customer IDs and dates need an explicit strategy. Do not
  invent customer or date values.
- Negative and zero sales may have valid business meaning. Investigate
  them before filtering.
- The four worksheets should not be merged merely because they belong
  to the same workbook. Confirm valid join keys and relationships
  first.
- The transaction sheet alone contains the stated sales target.
  Marketing and inventory information should only be incorporated if a
  valid relationship to each transaction can be established and the
  features would be available at prediction time.
Expected Outcome
The intended outcome is a reproducible sales-prediction workflow that
documents data-quality decisions, explores transaction patterns, and
compares regression models for predicting Total_Sales. Actual model
results should be added after training and evaluation.
Project Status
Dataset inspection and project planning: Started
Data cleaning, EDA, model training, and evaluation: To be completed
and documented as the project progresses.

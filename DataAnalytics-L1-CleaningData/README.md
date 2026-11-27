# Customer Sales Data Cleaning

## Project Overview
This project focuses on cleaning and preparing a messy customer sales dataset using Python and Pandas. The goal is to improve data quality by handling missing values, duplicates, inconsistent data, invalid entries, and incorrect data types.

## Dataset Information
- Original Dataset: `Dataset/messy_customer_sales_data.csv`
- Original Rows: 10,200
- Total Columns: 12

## Data Cleaning Steps
- Inspected the dataset structure and data types.
- Identified and handled missing values.
- Standardized Gender, City, and Country columns.
- Converted Age into numeric format and handled invalid values.
- Filled missing Age, Purchase_Amount, and Feedback_Score values using median imputation.
- Converted Signup_Date and Last_Purchase_Date into datetime format.
- Validated phone numbers and handled invalid entries.
- Handled negative purchase amounts and extreme outliers.
- Removed duplicate records.
- Performed final data quality checks.

## Cleaning Results

| Metric | Before Cleaning | After Cleaning |
|---|---:|---:|
| Total Rows | 10,200 | 10,014 |
| Total Columns | 12 | 12 |
| Missing Values | 7,804 | 3,050 |
| Duplicate Rows | 15 | 0 |

## Final Output
The cleaned dataset is saved as:

`Cleaned_Customer_Sales_Data.csv`

## Tools & Technologies
- Python
- Pandas
- NumPy
- Jupyter Notebook

## Project Files
- `OIBSIP_Task3_Data_Cleaning.ipynb` – Data cleaning notebook
- `Dataset/messy_customer_sales_data.csv` – Original dataset
- `Cleaned_Customer_Sales_Data.csv` – Cleaned dataset
- `README.md` – Project documentation

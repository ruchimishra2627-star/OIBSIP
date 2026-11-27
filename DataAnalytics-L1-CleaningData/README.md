# customer-sales-data-cleaning
Data cleaning & preprocessing pipeline for a messy customer sales dataset — built in a Jupyter notebook using pandas, numpy, matplotlib/seaborn, and scipy.


---

## 📌 Overview

Raw customer sales data is rarely ready for analysis. This project takes a synthetic, deliberately "messy" customer sales dataset — full of missing values, inconsistent text formatting, duplicate records, and invalid numeric entries — and runs it through a full cleaning pipeline to produce a reliable, analysis-ready dataset.

---

## 🗂️ Dataset

12 columns describing customer demographics and purchase behavior:

- **Identifiers/contact:** Customer_ID, Name, Email, Phone_Number
- **Demographics:** Gender, Age, City, Country
- **Dates:** Signup_Date, Last_Purchase_Date
- **Behavioral:** Purchase_Amount, Feedback_Score

## 🧹 Data Quality Issues Found

| Issue | Description |
|---|---|
| Missing values | 8 of 12 columns, ~700–1,025 nulls each (out of 10,200 rows) |
| Inconsistent Age formatting | Mixed strings like "52.0", "51.0 years", "nan years", plus implausible ages ("250", "3") |
| Invalid Purchase_Amount | Negative values (min = -500) and an extreme outlier (max = 9,999,999) |
| Inconsistent Gender labels | 8 variants for 2 categories: m, M, f, F, male, MALE, female, FEMALE |
| Inconsistent City labels | 18 variants of 6 real cities (case + whitespace) |
| Inconsistent Country labels | India, india, InDia, IND → one value |
| Duplicate rows | 15 exact duplicates initially; 163 more revealed after normalization |
| Duplicate customers | Same Customer_ID twice with cosmetic formatting differences |

## 🔧 Pipeline

1. **Missing data**
   - Dropped rows with missing Customer_ID (primary key, not imputable)
   - Age` — extracted numeric values via regex, filled unrecoverable values with the median
   - Purchase_Amount — median imputation
   - Feedback_Score, Gender, City, Country — mode imputation
   - Last_Purchase_Date — forward-fill
2. **Standardizing formatting**
   - Gender → lowercase + strip + map m/f → male/female
   - City → lowercase + strip
   - Country → lowercase + map ind → india
   - Cast Age to int64; Signup_Date / Last_Purchase_Date to datetime
3. **Duplicate removal**
   - Exact-row duplicates dropped with drop_duplicates()
   - Entity-level duplicates dropped with drop_duplicates(subset=['Customer_ID'], keep='first')
4. **Outlier detection**
   - Boxplots for Age, Purchase_Amount, Feedback_Score
   - Z-score filtering (|z| > 3) on Age and Purchase_Amount

## 📊 Results

| Stage | Rows | Columns | Notes |
|---|---|---|---|
| Raw data | 10,200 | 12 | Nulls, mixed types, inconsistent labels |
| After dropping missing Customer_ID | 9,177 | 12 | Primary-key rows with no ID discarded |
| After missing-value imputation | 9,177 | 12 | Zero nulls remaining |
| After removing full-row duplicates | 9,014 | 12 | 163 duplicate rows dropped |
| After de-duplicating by Customer_ID| 9,000 | 12 | Repeat customers collapsed |
| After Z-score outlier removal | **8,989** | **12** | 11 statistical outliers removed |

Overall, **~11.9%** of raw rows were removed across the pipeline, mainly due to missing primary keys and duplicate customer records.


### requirements.txt

pandas
numpy
matplotlib
seaborn
scipy



## 🔑 Key Findings

- ~10% of rows had a missing Customer_ID, pointing to an upstream data-capture issue
- Categorical inconsistencies were purely formatting (case/whitespace), not real category differences
- Purchase_Amount - contained clear data-entry errors at both extremes
- Duplicate detection required two passes — exact-row, then entity-level — since normalization revealed hidden duplicates

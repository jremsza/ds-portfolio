---
title: Data Cleaning and Preparation of LA Traffic Data with Python
seo_title: Portfolio Project 3
summary:  This project demonstrates a complete data cleaning and preparation workflow using Python's pandas library. Starting with a raw, messy dataset of over 500,000 traffic collision records from the City of Los Angeles, this project methodically cleans, transforms, and restructures the data into an analysis-ready format.
description: This project is a demonstration of my skills in data cleaning and preperation for analysis. The project was performed in my database and data preperation course utilizing a Los Angeles crime dataset.
slug: portfolio-project-la-crime-data-cleaning
author: Jake Remsza

draft: false
date: 2022-02-20T03:52:30-05:00
lastmod: 
expiryDate: 
publishDate: 

#feature_image: py.png
#feature_image_alt: py.png

tags:
  - Python
  - Pandas
  - EDA
  - Data Cleaning
  - Data Wrangling

categories:
  - Data Preparation with Python

project types: 
  - Academic

techstack:
  - Python 
  - Pandas
  - Numpy

#live_url: https://hugo-liftoff.netlify.app
source_url: https://github.com/jremsza/data_clean-LATrafficData.git
---

## 🧹 Project Summary

This project focuses on the foundational, yet most critical, stage of the data science lifecycle: data cleaning and preparation. The objective is to take a raw dataset of over 500,000 traffic collision records from Los Angeles and transform it into a clean, well-structured, and reliable format suitable for future analysis and modeling.

The process involves a systematic approach to handling missing values, correcting data types, cleaning categorical variables, feature engineering, and restructuring the data for usability.


## 🔍 Background & Initial Inspection

The project utilizes the "Traffic Collision Data from 2010 to Present" dataset from the official City of Los Angeles open data portal. An initial inspection using `.info()` and `.head()` revealed several key issues that needed to be addressed:

- **Redundant Data:** Several columns contained the same value for every record (e.g., `Crime Code Description` was always 'TRAFFIC COLLISION').

- **Incorrect Data Types:** Dates and times were stored as string objects, and numerical columns like `Victim Age` were floats with missing values.

- **Dirty Categorical Data:** Fields like `Victim Sex` and `Victim Descent `contained inconsistent or erroneous codes.

- **Complex Fields:** Location data was packed into a single string, and `MO Codes` contained multiple values in one field.

- **Duplicates:** The dataset contained thousands of duplicate rows.

## 🧼 Part 1: Structural Cleaning

The first phase of cleaning focused on high-level structural issues to reduce noise and create a solid foundation.

**Dropping Redundant Columns & Duplicates**

**Action:** Columns that provided no analytical value were removed, including `Date Reported`, `Area ID`, `Crime Code`, `Crime Code Description`, `Premise Code`, and `Premise Description`. Additionally, over 2,600 duplicate rows were identified and dropped.

**Impact:** This initial step immediately streamlined the dataset, reducing it from 19 to 11 columns and ensuring each record was unique.

```
# Shape before cleaning
(569389, 19)

# --- Cleaning operations performed here ---

# Shape after dropping unneeded columns and duplicates
(559577, 11)
```

## 🔧 Part 2: Feature Cleaning & Transformation

This phase involved a deep dive into individual columns to correct errors, handle missing data, and standardize values.

**Cleaning Victim Age**
The `Victim Age` column required special attention due to outliers, missing values, and invalid entries.

![alt text](/images/proj-3/image-11.png)

Insight: The boxplot and a `.value_counts()` analysis revealed a significant number of records where the age was listed as 99, which appeared to be a placeholder for unknown data. There were also ages recorded below the legal driving age.

**Actions Taken:**

1. **Outlier Removal:** All records with Victim Age of 99 were removed.

2. **Imputation**: A new boolean column imputeAge was created to track which age values were imputed. The NaN values were then filled with the mean age of the dataset.

3. **Filtering:** Records with ages below 16 were dropped as they are not valid for drivers.

4. **Type Conversion:** The column was converted from a float to an integer for clean, final storage.

**Standardizing Categorical Features**

The `Victim Sex` and `Victim Descent` columns contained messy, inconsistent codes.

**Action** (`Victim Sex`): Records with invalid codes ('H', 'N', `null`) were filtered out. The remaining codes were mapped to more descriptive values: 'M' → 'Male', 'F' → 'Female', and 'X' → 'Other'.

**Action** (`Victim Descent`): Following research guidelines, numerous specific descent codes were consolidated into broader categories (e.g., 'C', 'F', 'V', 'K', etc., were all mapped to 'Asian'). Nulls and dashes were mapped to 'Unknown'. This transformed a noisy feature into a clean, interpretable one.

## 🏗️ Part 3: Feature Engineering & Final Structuring

The final phase focused on creating new, more useful features and restructuring complex data for relational analysis.

**Engineering Date, Time, and Location Features**

**Action:** To make the data more useful for time-series analysis, new features were engineered:

- `Month`, `Day`, and `Year` were extracted from the `Date Occurred` string.

- `Hour` was extracted from the `Time Occurred` integer value.

- The messy `Location` string `'(Lat, Long)'` was split into two clean numeric columns: Latitude and Longitude.

**Restructuring** `MO_Codes`

**Insight:** The `MO Codes `(Modus Operandi) field contained multiple codes in a single string (e.g., '3004 3030 5002'), making direct analysis impossible.

**Action:** This column was "exploded" into a separate, tidy DataFrame. The new mo_df table contains a row for each individual code, linked back to the original incident by its DR_Number. This normalizes the data, making it suitable for relational database use and analysis of specific incident characteristics.

```
# mo_df after exploding the MO_Codes
   DR_Number MO_Codes
0  190326475     0100
0  190326475     3030
1  191122295     0100
2  200106535     0100
3  200107229     0100
3  200107229     3004
3  200107229     3030
```

## ✅ Project Outcome

The project successfully transformed a raw, complex dataset into two clean, analysis-ready CSV files:

1. Final Traffic.csv: The main dataset containing cleaned incident records with well-defined, properly typed columns.

2. MO per accident.csv: A normalized lookup table connecting each incident (DR_Number) to its individual Modus Operandi codes.

These deliverables are now fully prepared for exploratory data analysis, data visualization, or predictive modeling tasks.

## 🧰 Tools Used

- **Python**

- **Pandas:** Used for all core data loading, manipulation, and cleaning operations.

- **Numpy:** Utilized for numerical operations and handling of imputed values.

- **Techniques:** Data Cleaning, Data Wrangling, Feature Engineering, Outlier Detection, and Data Restructuring.
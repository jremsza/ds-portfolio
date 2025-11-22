---
title: SQL and Python Analysis of Los Angeles Traffic Data
seo_title: Portfolio Project 5
summary: This project is an extension of the previous data cleaning exercise. The cleaned LA traffic collision dataset was loaded into an SQLite database to perform an in-depth exploratory analysis using SQL. The analysis answers key questions about incident types, demographic trends, and temporal patterns.
description:  This project is an extension of the data cleaning exercise from project 4. The cleaned LA traffic dataset was used for the analysis of project.
slug: portfolio-project-la-traffic-sql-analysis
author: Jake Remsza

draft: false
date: 2021-02-20T03:52:30-05:00
lastmod: 
expiryDate: 
publishDate: 

#feature_image: 
#feature_image_alt: 


tags:
  - Python
  - SQL
  - SQLite
  - EDA
  - Data Visualization

categories:
  - Data Analysis with SQL

project types: 
    - Academic

techstack:
    - Python
    - SQL
    - Pandas
    - SQLite
    - SQLAlchemy
    - Matplotlib
    - Seaborn

#live_url: https://hugo-liftoff.netlify.app
source_url: https://github.com/jremsza/LATrafficData-V2.git
---

## 🔎 Project Summary
This project takes the cleaned and prepared Los Angeles traffic collision data from the previous stage and loads it into an SQLite database for analysis. The primary goal is to demonstrate proficiency in SQL by querying the database to answer specific analytical questions.

The analysis explores the most common types of traffic incidents, investigates demographic patterns between different age groups, analyzes trends over time, and visualizes the geographic distribution of collisions.

## 🗄️ Background: From CSV to Database
Before analysis could begin, the two clean datasets (Final Traffic.csv and MO per accident.csv) were loaded into a new SQLite database named LAtraffic.db. The SQLAlchemy library in Python was used to create a database engine and populate three tables: traffic, MO_accident, and MO_master. This database structure allows for efficient and powerful relational querying.

## 📊 Part 1: Foundational Analysis with SQL
The first step was to use SQL JOINs and aggregate functions to understand the fundamental characteristics of the data.

What are the most common types of traffic incidents?
A query was written to `JOIN ` the `MO_accident` table (incident-specific codes) with the MO_master table (code descriptions) and then `GROUP BY` the description to get a count of each incident type.

```SQL

SELECT
    m.Description,
    count(*) AS Count
FROM MO_accident a
JOIN MO_master m
    ON a.MO_Codes = m.Codes
GROUP BY m.Description
ORDER BY Count DESC;
```

![alt text](/images/proj-1/image-7.png)
 
**Insight** 📈: The results clearly show that **"T/C - Hit and Run Misd"** (Misdemeanor Traffic Collision Hit and Run) is by far the most common type of reported incident, occurring over 120,000 times in the dataset. This immediately identifies a key area of concern for traffic safety in Los Angeles.

## 🎯 Part 2: Answering Key Questions with Targeted Queries

With a foundational understanding, more specific questions were investigated using targeted `WHERE` clauses and further aggregations.

**Which police divisions see the most incidents?**

A simple `GROUP BY` query on the `traffic` table reveals the distribution of accidents by police division.

![alt text](/images/proj-4/image-17.png)

**Insight**📍: The **77th Street, Southwest, and Southeast divisions** report the highest number of traffic incidents. This kind of geographic analysis is crucial for resource allocation and targeted enforcement.

**How do accidents differ between teenage and elderly drivers?**

A SQL query was used to select drivers aged 16-19 and those over 80. The results were then analyzed in Python to compare the demographic breakdown.

![alt text](/images/proj-4/image-20.png)

**Insight**👵🏼🧒🏽: There are distinct demographic differences between the two groups. For instance, accidents involving drivers of Hispanic descent are far more prevalent in the teenage group, whereas accidents involving White drivers are more prevalent in the elderly group. This suggests different risk profiles and demographic contexts for accidents across age spectrums.

**Have hit-and-run accidents increased over time?**

A query was performed to count hit-and-run incidents (**MO_Codes** 3029 or 3030) for each year and division. The results were then visualized as a line plot.

![Line plot of hit-and-run accidents by year and division](/images/proj-4/image-27.png)

**Insight** 📉: The data shows a clear **increasing trend** in hit-and-run accidents from 2012 to 2019 across most divisions. There is a sharp drop in 2020, which is very likely attributable to reduced traffic during the COVID-19 pandemic. The data for 2010 and 2011 appears incomplete and should be excluded from trend analysis, demonstrating the importance of critically evaluating data quality.


## 🗺️ Part 3: Geospatial Analysis
To validate the location data and visualize incident hotspots, SQL was first used to filter for records with valid latitude and longitude coordinates within the bounds of Los Angeles. The resulting data was then plotted using Python's seaborn library.

![Scatter plot of accidents by latitude and longitude, colored by division](/images/proj-4/image-22.png)

Insight 🗺️: The plot creates a clear map of Los Angeles based on traffic collision locations, confirming the overall quality of the geographic data. The visualization also highlights the density of incidents, with heavier concentrations in the central and southern divisions, aligning with the findings from the SQL query in Part 2.

## ✅ Conclusion
By loading the cleaned data into a database and analyzing it with SQL, several key insights were uncovered:

- **Hit-and-runs** are the most significant category of traffic incidents.

- Accident hotspots are concentrated in the **77th Street, Southwest, and Southeast** divisions.

- The number of hit-and-run incidents was on an **upward trend** before the 2020 pandemic.

- There are **clear demographic differences** in accident profiles between the youngest and oldest drivers.

## 🧰 Tools Used

- **SQL:** For all data querying, aggregation, joining, and filtering.

- **SQLite:** The database engine used to store and manage the data.

- **Python:** Used as the primary environment to connect to the database and orchestrate the analysis.

- **SQLAlchemy:** Python library used to create and connect to the SQLite database engine.

- **Pandas:** Used to structure the results of SQL queries into DataFrames.

- **Matplotlib & Seaborn:** Used for data visualization, including the time-series line plot and the geospatial scatter plot.

---
title: 'COVID-19 in Europe: An R-Based Analysis of Cases, Fatalities, and Economic Factors'
seo_title: Portfolio Project 3
summary: Investigated the spread of COVID-19 across European nations using R. This project involved exploratory data analysis (EDA), hypothesis testing to compare fatality rates between countries, and the development of a linear regression model to predict total cases based on population and economic indicators.
description: This project analyzes daily COVID-19 case and death data from the European Union/European Economic Area. The goal was to uncover trends over time, compare national fatality rates, and determine if a country's total cases could be predicted by its population, density, and economic output (GDP). The analysis was conducted entirely in R, utilizing packages like dplyr, ggplot2, and tidyr.
slug: portfolio-project-covid-analysis
author: Jake Remsza

draft: false
date: 2023-02-20T03:52:30-05:00
lastmod: 
expiryDate: 
publishDate: 

#feature_image: r_image.jpg
#feature_image_alt: Web design

tags:
  - R
  - EDA
  - Hypothesis Testing
  - Regression
  - Data Visualization

categories:
  - Statistics with R
  - Data Analysis

project types: 
  - Academic

techstack:
  - R 
  
#live_url: https://hugo-liftoff.netlify.app
source_url: https://github.com/jremsza/covid_analysis-MSDS401
---

## 🦠 Project Summary 

This project performs a comprehensive analysis of COVID-19 data from the European Union (EU) and European Economic Area (EEA). The goal is to uncover trends, compare national outcomes, and model the factors driving the spread of the virus. The analysis is structured into four key parts:

- **Part 1:** Exploratory Data Analysis (EDA) to visualize trends and distributions.

- **Part 2:** Inferential Statistics to formally compare fatality rates between countries.

- **Part 3:** Correlation Analysis to investigate the relationship between case and fatality rates.

- **Part 4:** Predictive Modeling to explain total cases using demographic and economic indicators.

## 🔍 Background

The dataset contains daily new COVID-19 cases and deaths for each country in the EU/EEA. To standardize comparisons, the raw counts of cases and deaths were converted into two key metrics for the analysis:

Incidence Rate: New daily cases per 100,000 people.

Fatality Rate: New daily deaths per 100,000 people.

This project leverages these metrics to move beyond simple counts and understand the pandemic's impact relative to each country's population, providing a more equitable basis for comparison and modeling.

## 📊 Part 1: Exploratory Data Analysis

![COVID-19 cases over time for all European countries](/images/proj-2/image_1.png)

Visualizing the Pandemic's Trajectory
Insight: This plot visualizes the waves of infection across Europe. It immediately reveals that countries experienced peak infection periods at different times and with vastly different magnitudes. The density of points highlights periods of widespread, high-case counts across the continent.

![Total fatalities vs. total cases for each country in the EU](/images/proj-2/image-3.png)

**Insight:** This visualization provides a high-level view of the pandemic's overall toll. There is a clear positive linear relationship: countries with higher total cases also experienced higher total deaths. However, the scatter also shows variation, suggesting that the case-to-fatality ratio was not uniform across all nations. Countries like France and Germany stand out due to their large populations and correspondingly high cumulative totals.
 

## 🔬 Part 2: Inferential Statistics - A Tale of Two Countries

Comparing Fatality Rates: Portugal vs. Sweden
To investigate whether differences in pandemic responses led to different outcomes, a two-sample t-test was conducted between the fatality rates of Portugal and Sweden, two countries with similar populations.

Null Hypothesis (H_0): There is no statistically significant difference between the mean daily fatality rates of Portugal and Sweden.

![Histograms of fatality rates in Portugal and Sweden](/images/proj-2/image-4.png)


![Fatality rate over time comparing Portugal and Sweden](/images/proj-2/image-5.png)

**Insight:** A Welch Two Sample t-test was chosen because the goal is to compare the means of two independent groups. While the underlying data is not normally distributed, the large sample size for each country allows us to rely on the Central Limit Theorem, making the t-test a robust choice. The test returned a p-value of 0.0001474, which is well below the alpha level of 0.05.

**Conclusion:** We reject the null hypothesis. The results indicate a statistically significant difference in the mean fatality rates between the two countries, with Portugal's average rate being higher. The visualization supports this, showing that while both countries experienced waves, Portugal endured periods with significantly higher fatality rate peaks.

## 📈 Part 3: Modeling & Insights

Correlation: The Link Between Cases and Fatalities

![Histograms of daily incidence and fatality rates for all data](/images/proj-2/image-6.png)

![Scatter plot of daily fatality rates vs. daily incidence rates](/images/proj-2/image-7.png)

**Insight:** The Kendall correlation coefficient was selected as the most appropriate measure for this relationship. Unlike Pearson's correlation, Kendall's is non-parametric and robust to outliers and non-normal distributions, both of which are evident in the data. The analysis yielded a Kendall's Tau of 0.42, indicating a moderate positive relationship between daily incidence rates and daily fatality rates. This statistically confirms the logical expectation: days with more reported cases tend to be associated with more reported deaths.

Multiple Linear Regression Model
A linear model was built to determine if country-level indicators could predict the total number of COVID-19 cases.

```
lm(formula = total_cases ~ pop + pop_dens + gdp_pps, data = model_df)
```

#### Output
```
## Coefficients:
##               Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -3.875e+06  2.787e+06  -1.390   0.183    
## pop          4.285e-01  3.676e-02  11.658 3.13e-09 ***
## pop_dens     6.502e+02  2.432e+03   0.267   0.793    
## gdp_pps      2.834e+04  2.559e+04   1.108   0.284    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Multiple R-squared:  0.8963, Adjusted R-squared:  0.8769
```

#### Key Insights from the Model

**Insight 1: Population is Paramount** 🌍
The model's most significant finding is the overwhelming predictive power of a country's population. The pop variable is highly statistically significant ($p \< 0.001$), and the model's Adjusted R-squared of 0.8769 indicates that nearly 88% of the variation in total cases can be explained by this single factor. This confirms the intuitive idea that, all else being equal, more people lead to more cases.

**Insight 2: Economic & Density Factors Are Not Significant** 🤔
Contrary to initial hypotheses, neither population density (pop_dens) nor GDP per capita (gdp_pps) were found to be statistically significant predictors in this model. Their high p-values suggest that their effects are negligible after accounting for population. This is a critical insight, suggesting that a simpler model focusing solely on population would be more effective and appropriate.

**Insight 3: Model Performance on New Data Is Mixed** 📉
When used to predict outcomes for countries outside the training set (Luxembourg and the Netherlands), the model's performance was inconsistent. It accurately predicted the total cases for the Netherlands but vastly over-predicted cases for Luxembourg by more than tenfold. This highlights a key limitation: while the model captures a strong general trend, it is not robust enough to account for the unique circumstances of every country, especially smaller ones like Luxembourg.

 
## 📌 Conclusions

- **EDA reveals clear patterns:** Visualizations effectively show the distinct waves of the pandemic and the strong relationship between a country's cumulative cases and deaths.

- **National outcomes differed significantly:** Hypothesis testing confirmed that even between countries with similar populations, there were statistically significant differences in COVID-19 fatality rates.

- **Population is the dominant driver of total cases:** A linear regression model demonstrated that a country's population is the single most powerful predictor of its total case count, explaining approximately 88% of the variance. Other factors like population density and GDP were not significant in this context.

- **The model has predictive limitations:** While powerful in explaining the existing data, the model's performance on new, unseen countries was mixed, indicating that it serves better as an explanatory tool than a universal predictive one.
 Definitions:


## 🧰 Tools Used

- **R** (dplyr, ggplot2, lubridate, Hmisc)

- **Data Cleaning & Feature Engineering:** Calculated incidence_rate and fatality_rate to normalize data for meaningful comparisons.

- **Statistical Analysis:**

  - Hypothesis Testing: Performed a two-sample t-test to compare population means.

  - Correlation Analysis: Utilized Kendall's correlation coefficient for non-parametric data.

  - Linear Regression: Built and interpreted a multiple linear regression model to identify significant predictors of total cases.

  - Data Visualization (ggplot2, gridExtra):

  - Exploratory Analysis: Created time-series plots, scatter plots, and histograms to uncover initial patterns and distributions.

  - Comparative Analysis: Plotted data for specific country subsets to support hypothesis testing.




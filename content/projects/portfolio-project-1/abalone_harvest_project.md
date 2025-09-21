---
title: Exploring Abalone Data with R - Unveiling Insights for Sustainable Harvesting Practices
seo_title: Portfolio Project 1
summary: This project was an assignment performed in my statistics with R course. Exploratory data analysis was done and statistical modeling was performed to gain insights on abalone harvesting.
description: Portfolio Project 1 is my first portfolio project.
slug: portfolio-project-1
author: Jake Remsza

draft: false
date: 2019-02-20T03:52:30-05:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

tags:
  - R
  - EDA
  - Regression

categories:
  - Statistics with R
  - Math
  - EDA

project types: 
  - Academic
  - Personal
techstack:
    - R 
#live_url: https://hugo-liftoff.netlify.app
source_url: https://github.com/jremsza/abolone_harvest_project

---

---

## 🐚 Project Summary

This graduate-level project explores sustainable harvesting strategies for abalone using data-driven methods in R. The analysis spans two parts:

- Part 1: Exploratory Data Analysis and variable relationships
- Part 2: Predictive modeling and harvest classification

---

## 🔍 Background

Abalone are marine mollusks valued for their meat and shells, but overfishing threatens their population. The assignment data are derived from an observational study of abalones. The intent of the investigators was to predict the age of abalone from physical measurements thus avoiding the necessity of counting growth rings for aging. Ideally, a growth ring is produced each year of age. Currently, age is determined by drilling the shell and counting the number of shell rings using a microscope. This is a difficult and time consuming process and Ring clarity can be an issue. At the completion of the breeding season sexing abalone can be difficult. Similar difficulties are experienced when trying to determine the sex of immature abalone. This study leverages biological data to investigate indicators for sustainability of harvesting using regression models and data visualization techniques.

---

## 📊 Part 1: Exploratory Data Analysis

### Data Overview

The dataset includes biological metrics:

- Length, Diameter, Height
- Whole weight, Shucked weight, Volume
- Rings <br>
> The goal is to accuratly predict the age with these metrics without harm to the animal 

###	Visualizations


#### Scatter Plot Matrix

![Scatterplot matrix of abalone measurements](/images/image-1.png)

**Insight:** A scatter plot matrix was created to understand the relationships between the physical measurements. The plot supports strong linear correlations among all size and weight variables.

![alt text](/images/proj-1/image-6.png)

**Insight:** These plots provide the perfect justification for a linear regression model. They visually confirm that as RINGS increases, so do the weight and volume of the abalone. This is the exact relationship that is modeled in part 2.

---

## 📈 Part 2: Modeling and Insights

### Multiple Linear Regression Model

```
mod1 <- lm(L_SHUCK ~ L_VOLUME + CLASS + TYPE, data = mydata)
summary(mod1)
```

### Regression Model Results

```
## 
## Call:
## lm(formula = L_SHUCK ~ L_VOLUME + CLASS + TYPE, data = mydata)
## 
## Residuals:
##       Min        1Q    Median        3Q       Max 
## -0.270634 -0.054287  0.000159  0.055986  0.309718 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -0.796418   0.021718 -36.672  < 2e-16 ***
## L_VOLUME     0.999303   0.010262  97.377  < 2e-16 ***
## CLASSA2     -0.018005   0.011005  -1.636 0.102124    
## CLASSA3     -0.047310   0.012474  -3.793 0.000158 ***
## CLASSA4     -0.075782   0.014056  -5.391 8.67e-08 ***
## CLASSA5     -0.117119   0.014131  -8.288 3.56e-16 ***
## TYPEI       -0.021093   0.007688  -2.744 0.006180 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.08297 on 1029 degrees of freedom
## Multiple R-squared:  0.9504, Adjusted R-squared:  0.9501 
## F-statistic:  3287 on 6 and 1029 DF,  p-value: < 2.2e-16
```
**Visualization:**&#x20;
![alt text](/images/proj-1/image-4.png)

These diagnostic plots validate the core statistical assumptions of the linear regression model. The histogram reveals that the model's residuals are approximately normally distributed, a finding that is strongly confirmed by the Normal Q-Q plot, where the data points align closely with the diagonal line. This confirms that the model is well-specified, ensuring the reliability of the statistical inferences, such as p-values and confidence intervals

### Key Insights from the Model

**Insight 1:** Volume is King (An Almost Perfect Relationship) 👑
The most striking result is the performance of the L_VOLUME variable and the overall R-squared.

The Finding: The Adjusted R-squared is 0.9501, meaning the model accounts for 95% of the variability in the abalone's shuck weight. The L_VOLUME coefficient is 0.999303 (essentially 1.0) and is astronomically significant (p-value is < 2e-16).

The Insight: This isn't just a correlation; it's practically a physical law. A coefficient of ~1.0 in a log-log model like this implies a direct, proportional relationship. In short the model has confirmed that an abalone's edible meat content (Shuck Weight) is an almost perfect, constant fraction of its overall volume. This is the primary driver of the relationship.

**Insight 2:** 'CLASS' as a Yield Modifier 📉
This is a more subtle and impressive finding that uncovers secondary effects.

The Finding: The coefficients for CLASSA3, CLASSA4, and CLASSA5 are statistically significant and increasingly negative. For example, being in CLASSA5 has a coefficient of -0.117.

The Insight: This means that for a given volume, an abalone in a "higher" class (A3-A5) has a systematically lower shuck weight than an abalone in class A1 (the baseline). This suggests that as abalone progress through these classes (perhaps as they age), their physical composition changes. They might develop a thicker shell or more viscera relative to their meat content. This is a non-obvious insight that would be very valuable for optimizing a harvest.

**Insight 3:** The 'Infant' Factor 👶
The TYPE variable adds another layer of nuance.

The Finding: The coefficient for TYPEI (infant) is -0.021 and is statistically significant.

The Insight: Even after accounting for volume and class, the model found that infants have a slightly lower shuck weight than adults of the very same size. This quantifies a fundamental biological difference and further refines the prediction.

### Model Evaluation

ROC curves used to evaluate classification accuracy.

![alt text](/images/proj-1/image-9.png)

**Insight:**TThe true power of this visual is that it bridges the gap between data science and real-world operations. A fishery manager doesn't work with logistic regression coefficients; they work with physical size limits. This plot shows exactly how a simple, measurable rule like "only harvest abalone with a volume greater than X" translates into a specific trade-off between profit and conservation.

For example, the point labeled "Median Adult Vol = 384.6" represents a clear business strategy. By setting the minimum harvest volume to this level, the model predicts we would:

Successfully harvest about 85% of the adult population (the y-axis value, or True Positive Rate).

At the cost of accidentally harvesting about 30% of the protected infant population (the x-axis value, or False Positive Rate).

This plot proves there is no single "perfect" answer, only a series of strategic choices.

A conservation-focused strategy might choose a lower volume threshold (a point to the left on the curve), accepting a smaller adult harvest to ensure almost no infants are harmed.

A more yield-focused strategy might select a higher threshold (a point to the right), risking more infants to maximize the adult catch.


![alt text](/images/proj-1/image-8.png)

**Insights** While the ROC curve is great for data scientists, this ECDF plot is arguably better for communicating with stakeholders. It directly answers the most important practical question: "If we set a minimum harvest volume of 'X', what happens?"

Each vertical line on the plot represents a potential business rule, and its intersection with the two curves reveals the outcome:

Intersection with the 'Infants' curve (teal): Shows the infant protection rate—the percentage of the vulnerable population that will be saved.

Intersection with the 'Adults' curve (red): Shows the adult harvest loss rate—the percentage of the target population that will be forgone.

The goal is to find a threshold that keeps the infant protection rate high (teal curve is high) while keeping the adult harvest loss rate low (red curve is low).

####
---

## 📌 Conclusions

- The linear model was highly predictive, explaining 95% of the variance in shuck weight. It revealed that while volume is the dominant predictor, factors like 'CLASS' and 'TYPE' act as subtle but significant modifiers on meat yield, suggesting biological changes that impact harvest potential.

- A classification model was developed that successfully translates statistical outputs into a strategic business tool. The ROC and ECDF plots provide a clear framework for decision-makers, allowing them to visualize the direct trade-offs between harvest yield and conservation when setting a size limit.

- This project serves as a complete, end-to-end example of data-driven policy making. It moves from raw data to exploratory analysis, to building and rigorously validating two distinct statistical models, and finally, to creating an actionable framework that can directly inform sustainable fishery management.

---

## 🧰 Tools Used

- **R** (RMarkdown, ggplot2, dplyr, caret)
- Performed **feature engineering** by creating log-transformed variables to improve model performance and satisfy statistical assumptions.
- Statistical Modeling & Evaluation: **Linear Regression** model to predict abalone physical attributes, validated using residual analysis and Q-Q plots.
- **Logistic Regression:** Developed a classification model to determine harvest sustainability.
- **Model Evaluation:** Assessed classifier performance using ROC curves and calculated the AUC (Area Under the Curve) to quantify its predictive power.
- **Data Visualization** (ggplot2):
**Exploratory Analysis:** Pairs plots, histograms, and scatter plots to uncover initial insights.
**Model Interpretation:** Plotted ECDF (Empirical Cumulative Distribution Function) curves to translate model outputs into an intuitive business simulation tool for stakeholders.

---

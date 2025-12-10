---
title: "Optimizing Public Safety: Chicago Crime Geospatial Analysis"
date: 2023-11-25
summary: "A geospatial intelligence project quantifying the relationship between police station locations and violent crime hotspots using PostGIS and Python."
weight: 2

tags:
  - Geospatial Analysis
  - PostGIS
  - SQL
  - Python
  - Folium
  - Data Visualization

categories:
  - Public Safety
  - Spatial Analytics

techstack:
    - PostgreSQL (PostGIS)
    - Python (Folium, Pandas)
    - GeoPandas
    - Jupyter

Source: 
---

## 🗺️ Project Overview

In urban environments, the physical distance between law enforcement infrastructure and crime hotspots is a critical factor in response times and community safety. This project utilizes **PostgreSQL with PostGIS extensions** to perform advanced spatial queries on Chicago's crime data, determining which neighborhoods are underserved based on their distance from police stations.

### 🔍 The Challenge
Chicago faces significant disparities in crime rates across different districts. The goal of this analysis was to:
1.  **Map Crime Density:** Visualize the concentration of gun-related offenses.
2.  **Evaluate Accessibility:** Calculate the distance between high-crime blocks and the nearest police station to identify coverage gaps.
3.  **Analyze Reporting Patterns:** Investigate temporal correlations between different types of violent crimes (Battery vs. Assault).

---

## 🛠️ Tools & Methodology

This project moves beyond simple plotting by pushing the geospatial computation to the database layer using **PostGIS**, which is more efficient for handling large geometric datasets than client-side Python processing.

* **PostGIS & SQL:** Used for spatial joins (`ST_Distance`, `ST_DWithin`) to calculate proximity between crime locations and police districts.
* **Folium:** Generated interactive Choropleth maps to visualize crime density per district.
* **Pandas:** Used for temporal analysis of crime reporting trends over 24-hour cycles.

---

## 💡 Key Insights & Results

### 1. Spatial Distribution of Gun Violence
By filtering for gun-related incidents and performing spatial joins with police district boundaries, I created a Choropleth map that highlights specific districts as significant outliers in terms of violence per capita. This visual output serves as a direct tool for stakeholders to prioritize patrol routes.

![crime counts](/images/chi-crime/crime-district.png)

Figure 1: Choropleth map of Chicago Police Districts colored by density of gun-related incidents. Darker regions indicate higher violent crime rates per capita.

### 2. The "Distance Gap"
Using PostGIS distance queries, I identified specific city blocks that experienced gun-related arrests while being the **furthest distance** from their assigned police station. These "max distance" blocks represent high-risk zones where response times may be compromised, suggesting a need for forward-deployed resources or community policing centers.

![gun-crime-distance](/images/chi-crime/gun-crime-distance.png)

Figure 2: Spatial analysis highlighting blocks (red markers) with gun-related arrests that exceed the median response distance from the nearest police station.

### 3. Data Integrity in Crime Reporting
An analysis of hourly crime trends revealed a near-perfect temporal correlation between Battery and Assault cases. While Battery occurs more frequently, both crimes react identically to temporal factors. This suggests:
* These crimes are likely reported interchangeably by officers or dispatchers.
* Predictive models should treat these categories as correlated features rather than independent events to avoid collinearity issues.


![crime-counts](/images/chi-crime/crime-counts.png)
Figure 3: Temporal analysis showing the near-identical hourly reporting trends of Battery vs. Assault cases, suggesting potential interchangeability in police reporting.

---

## 🚀 Future Scope
To further enhance this analysis for deployment:
* **Time-Series Animation:** Implementing `Folium.TimestampedGeoJson` to visualize how crime hotspots migrate depending on the time of day or season.
* **K-Means Clustering:** Applying unsupervised learning to suggest optimal locations for new emergency response units based on incident density rather than static district boundaries.
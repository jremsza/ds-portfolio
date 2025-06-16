
---
title: "Chicago Crime Analysis with PostGIS"
date: 2025-06-12
summary: "A geospatial data project analyzing Chicago crime incidents using SQL and PostGIS. Includes choropleth maps of gun-related crimes, spatial joins, and distance metrics between crime locations and police stations."
tags: ["PostGIS", "SQL", "Geospatial Analysis", "Crime Data", "Choropleth Map"]
categories: ["Geospatial Projects", "Portfolio Projects"]
---

## 🚨 Chicago Crime Analysis with PostGIS

**Category:** Geospatial Analysis, SQL, Data Visualization  
**Tools:** PostgreSQL, PostGIS, Python, Folium, Pandas  
**Skills:** Geospatial querying, choropleth mapping, spatial joins, distance calculations, SQL analytics

---

### 🔍 Problem Statement

This project explored crime and police activity data in the city of Chicago using geospatial analysis tools. The main objective was to understand patterns of gun-related crimes in relation to the locations of police stations, and to visualize this data using choropleth maps for actionable insights.

---

### 🧭 Datasets Used

- **Chicago Crime Dataset**: Includes crime type, date, and location  
- **Chicago Police Stations**: Locations of police stations across city districts

---

### 🗺️ Geospatial Analysis Objectives

- **Spatial Joins** between crimes and police stations  
- **Filtering** of gun-related crimes (with and without arrests)  
- **Choropleth Maps** by district for:
  - Number of total crimes  
  - Gun-related incidents  
  - Arrest ratios  
- **Max Distance Query**: Identifying blocks with gun crimes farthest from a police station

---

### 🧠 Tools & Techniques

- **PostGIS** extensions in PostgreSQL for spatial querying  
- **SQL Aggregations** by district  
- **Spatial Filtering** using geometry-based conditions  
- **Folium** and **GeoPandas** for map rendering  
- **Custom metrics** like arrest rates by district

---

### 📈 Results

- Created layered choropleth maps showing spatial distribution of crime  
- Found neighborhoods farthest from police with gun-related arrests  
- Enabled comparison of arrest patterns across districts  
- Demonstrated use of spatial queries for real-world policy analysis

---

### 📌 Reflection

This project showcased the power of geospatial queries in policy and public safety contexts. It demonstrated how to join disparate datasets (crimes + stations) spatially, and how to visually represent complex data using Python.

**Future extensions:**
- Add time-based animation (crimes over months/years)  
- Apply clustering to identify emergent hotspots  
- Integrate socioeconomic data for deeper insights

---
title: Data Preperation and Cleaning with Python
seo_title: Portfolio Project 4
summary: This project is a demonstration of my skills in data cleaning and preperation for analysis. The project was performed in my database and data preperation course utilizing a Los Angeles crime dataset.
description: This project is a demonstration of my skills in data cleaning and preperation for analysis. The project was performed in my database and data preperation course utilizing a Los Angeles crime dataset.
slug: portfolio-project-4
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

categories:
  - EDA
  - Data Cleaning

project types: 
  - Academic
  - Personal

techstack:
  - Python 

#live_url: https://hugo-liftoff.netlify.app
source_url: https://github.com/wjh18/hugo-liftoff
---

### Objectives:  
 - Load the data from a CSV file and into a dataframe object.  
 - Inspect the data.  
 - Clean the data.  
 - Prepare the data for analysis.  

### Description:  

Many states, counties and cities in the U.S. have web sites where they make data available. The data used for this project was retrieved from the Los Angeles city link provided below. <br>

https://data.lacity.org/Public-Safety/Traffic-Collision-Data-from-2010-to-Present/d5tf-ez2w

#### Data Dictionary - fields available in the csv file

![alt text](image.png)

#### Import Libraries and Load the Dataset
```
# load libraries
import pandas as pd
import numpy as np

# set up notebook to display multiple output in one cell
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"

df = pd.read_csv("Traffic_Collision_Data.csv")

# look at the first 5 records
df.head()
```

![alt text](image-1.png)  

```
# look at the fields and data types
df.info()
```

![alt text](image-2.png)

```
# see null count
df.isnull().count()
```

![alt text](image-3.png)

##### Observations from first five records and .info()
- DR Number should be unique
- Date Reported and Date Occurred are mm/dd/yyyy - not Date fields, but Objects
- Is Crime Code all 997?
- Is Crime Code Description all TRAFFIC COLLISION?
- MO Codes are more than one in the field separated by a space. What do they mean?
- Victim age is a float and there are nulls
- Victim Descent is one character code 
- Are Premise code and Premise Description all the same?
- Location has lat/long in same field separated by comma 

```
# view data without a scroll bar
print(df.head())
```

![alt text](image-4.png)


```
# Are there any duplicates
df['DR Number'].nunique()

# comparing rows to each other shows there are duplicates
df.duplicated().sum()
```

**OUTPUT:**  
566747

2642

```
# Isolate year to see what is included in the data
# Note that we are creating a new column in the dataframe
df['Year'] = pd.to_datetime(df['Date Occurred']).dt.year

# sort by year
df['Year'].value_counts().sort_index(ascending = True)
```

**OUTPUT:**  

![alt text](image-5.png)

```
# Area Name looks good - not sure about Reporting District
df['Area Name'].value_counts()

# Over 1000 different reporting districts
df['Reporting District'].nunique()
df['Reporting District'].value_counts()
```

**Value Counts: Area Name**  
![alt text](image-6.png)

**nunique & value counts: Districts**  
![alt text](image-7.png)


```
# all the same, we can drop these columns later
df['Crime Code'].value_counts()
df['Crime Code Description'].value_counts()
```
![alt text](image-8.png)

```
#  null ages and there is some dirty data in ages
df['Victim Age'].value_counts(dropna = False) #will show NaN too

# ten year old driver!
df['Victim Age'].describe()

df['Victim Age'].hist()
```

![alt text](image-9.png)

![alt text](image-10.png)

```
# visually look at data
df.boxplot(column = 'Victim Age')
```

![alt text](image-11.png)

##### Victim Age analysis

- The histogram shows a blip near 100
- The boxplot shows potential outliers at the higher end of age
- After running the cell below, you can see that the age of 99 appears to be dirty data.  Since there are 39 people that are 98 years old, there are bound to be valid 99 years olds, but we don't know which ones, so we will eliminate 99 year olds from our data.


```
# create a subset of data to check out the ages
temp = df[df['Victim Age'] > 90]
len(temp)
temp['Victim Age'].value_counts()
```

![alt text](image-12.png)

```
# show data before delete of 7218 records
df.shape

# eliminate records
df = df[df['Victim Age'] != 99]

# check shape after elimination
df.shape
```

**OUTPUT**
(569389, 19)  

(562171, 19)

```
# look at victim gender values
df['Victim Sex'].value_counts(dropna = False)

# what is the precentage breakdown? Use normalize = True
df['Victim Sex'].value_counts(normalize = True, dropna = False)

# X is Unknown
# H and N are dirty data
```

![alt text](image-13.png)

#### LA Census Data:  
![alt text](image-16.png)

```
# look at descent by percent
df['Victim Descent'].value_counts(normalize = True, dropna = False)

# and by counts
df['Victim Descent'].value_counts()
```

![alt text](image-14.png)![alt text](image-15.png)

```
# since the majority are the same, we can drop these columns later
df['Premise Code'].value_counts()
df['Premise Description'].value_counts()
```

![alt text](image-17.png)

```
# have some null locations. Lat and Long are separated by a comma.
df['Location'].value_counts()
```

![alt text](image-18.png)

Dropped all unneeded columns: Date Reported, Area ID, Crime Code, Crime Code Description, Premise Code, Premise Description, Address and Cross Street.  
Showed the dataframe shape before deleting columns and after deleting columns.<br>

```
#dataframe before del
df.shape
```
**OUTPUT**  
(562171, 19)

```
#dataframe after del
df.drop(columns = ["Date Reported", "Area ID", "Crime Code",  "Crime Code Description", "Premise Code", "Premise Description",  "Address", "Cross Street"], inplace = True)
df.shape
```
**OUTPUT**  

(562171, 11)

Dropped duplicates - Show before and after shape.

```
#before drop na
df.shape

#after na drop
df.drop_duplicates(inplace=True)
df.shape
```

**OUTPUT**  

(562171, 11)  

(559577, 11)


##### Renamed columns to make them more clear and to prepare them for being loaded into a SQL database:<br>
    
1. Rename DR Number to DR_Number
2. Date Occurred to Date
3. Area Name to Division
4. Victim Age to Age
5. Victim Sex to Gender
6. Victim Descent to Descent
7. MO Codes to MO_Codes
8. Reporting District to Reporting_District
    
Displayed the dataframe with .info() to show the changes.

```
df.rename(columns = {"DR Number" : "DR_Number", "Date Occurred" : "Date", "Area Name" : "Divsion", "Victim Age" : "Age", "Victim Sex" : "Gender", "Victim Descent" : "Descent", "MO Codes" : "MO_Codes", "Reporting District" : "Reporting_District"}, inplace = True)

df.info()
```
![alt text](image-19.png)

##### Created new columns into the dataframe:<br>
    
1. Create a month field from Date field
2. Create a day field from Date field
3. Create an hour field from Time Occurred (can handle mathematically or as a string)
4. Drop Time Occured field
5. We will keep the Date field as it might be useful in our analysis later.

Showed the dataframe with .info() and .head()

```
#Create a month field
df["Month"] = df["Date"].apply(lambda num: num.split("/")[0])

#Create a day field
df["Day"] = df["Date"].apply(lambda num: num.split("/")[1])

#Create a hour field from Time Occurred
df["Hour"] = df["Time Occurred"].apply(lambda num: num // 100)

#Drop Time Occurred
df.drop(columns = ["Time Occurred"], inplace = True)

df.head()
df.shape
```

![alt text](image-20.png)

##### Fixed the victim Age. 
    
1. Show your dataframe before any changes with .info()
2. Replace the nulls with the mean of Age    
3. The ages should be valid driving ages of 16 and over; drop any ages under 16.
4. Convert Age to an integer.
4. Show the Age column with .describe()

```
# created a new field in the dataframe that will track imputed ages
# changed the dataframe name to match the current dataframe

# if the Age is over 9 then imputeAge will be False, otherwise it will be True
df['imputeAge'] = np.where(pd.isna(df['Age']), True, False)
df.head()
df.info()
```

![alt text](image-21.png)

```
#Replace the nulls with the mean of Age
df['Age'] = df['Age'].fillna(df['Age'].mean())

#drop any ages under 16.
df = df.drop(index=df[df['Age'] < 16].index)

#Convert age to int
df['Age'] = df['Age'].astype(int)

df.head()
df.describe()
df.info()
```

![alt text](image-22.png)

![alt text](image-23.png)


##### Fixed the Gender field. 
    
1. The values should be M, F and X so remove the rows with H, N and null values. 
2. Rename M to Male, F to Female and X to Other.
3. Show value counts for Gender column after the data has been cleaned using 'dropna = False'.

```
#Remove Values with H, N and na
df = df[(df.Gender == "M") | (df.Gender == 'F') | (df.Gender == 'X')]

#Rename Gender ids
df['Gender'] = df['Gender'].replace({'M': 'Male', 'F' : 'Female', 'X' : 'Other'})
#gender_map = {'M': 'Male', 'F': 'Female', 'X': 'Other'}
#df['Gender'] = df['Gender'].replace(gender_map)

gender_counts = df['Gender'].value_counts(dropna=False)
print(gender_counts)
```
![alt text](image-24.png)

For cleaning the Victim Descent, follow the guidelines of Pew Research. 

1. Include C (Chinese), Z (Asian Indian), F (Filipino), V (Vietnamese), K (Korean), J (Japanese), D (Cambodian), L (Laotion) into **A (Asian)**
2. Change the I, U, G, S, and P into O (Other)
3. Change the - (2 records with a dash) and the NaN into X (Unknown)
4. Rename the values in this column: H is Hispanic, W is White, O is Other, B is Black, X is Unknown and A is Asian
5. Do a values_count() on the Descent field to show the new breakdown using 'dropna = False'.

```
# 1.
df['Descent'] = df['Descent'].replace({'C': 'Chinese', 'Z' : 'Asian Indian', 'F' : 'Filipino', 'V' : 'Vietnamese', 'K' : 'Korean', 'J' : 'Japanese', 'D' : 'Cambodian', 'L' : 'Laotion', 'A': 'Asian' })
#2.
df['Descent'] = df['Descent'].replace(['I', 'U', 'G', 'S', 'P'], 'O')
#3.
df['Descent'] = df['Descent'].fillna('X').replace('-', 'X')
#4
df['Descent'] = df['Descent'].replace({'H': 'Hispanic', 'W' : 'White', 'O' : 'Other', 'B' : 'Black', 'X' : 'Unknown'})
#5.
df['Descent'].value_counts()
```

![alt text](image-25.png)


##### The Location field contains Latitude and Longitude separated by a comma. 
    
1. Create two new fields in the your dataframe - one for Latitude and one for Longitude. Neither of these fields should contain a parenthesis or comma from the original field. 
2. Once you have these two new columns, drop the Location field.
3. Drop the rows that have 0.0 for both Latitude and Longitudes.  You can do this before or after you split the field.
4. Show your dataframe with .info to show the new columns.
5. Run .head() on your dataframe to show the values in the new columns.

```
# Create two new fields - one for Latitude and one for Longitude
df['Latitude'] = df['Location'].apply(lambda x: x.strip('()').split(', -')[0])
df['Longitude'] = df['Location'].apply(lambda x: x.strip('()').split('-')[-1])

#Drop lacation field
df.drop(columns = ["Location"], inplace = True)

#Drop Rows that have 0.0 for both columns
df.drop(df[(df['Latitude'] == 0.0) & (df['Longitude'] == 0.0)].index, inplace=True)

df.info()
df.head()
```

![alt text](image-26.png)

![alt text](image-27.png)

##### Split out MO_Codes into its own dataframe with only two fields: DR_Number and MO_Codes.

```
# looking at MO codes shows many codes per incident
# let's separate these out and put into a separate dataframe for later use
df['MO_Codes'].head(10)
```

![alt text](image-28.png)

```
# use pandas explode to separate field: 
# https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.explode.html
mo = df[['DR_Number','MO_Codes']]
mo.shape
mo = mo.dropna()
mo.shape

mo["MO_Codes"] = mo["MO_Codes"].str.split()
mo_df = mo.explode("MO_Codes")
mo_df.head(10)
mo_df["MO_Codes"].value_counts()
mo_df.info()

(550202, 2)

(465652, 2)
```

![alt text](image-29.png)

##### Dropped MO_Codes from the original dataframe. Show the final main dataframe with .info().

```
df.drop(columns = ['MO_Codes'], inplace = True)
df.info()
```

![alt text](image-30.png)


##### Save clean files to new csv files for later use

```
# write out the clean file to be used in Ex 2 Introduction to SQL
df.to_csv('Final Traffic.csv', index = False)
```

```
# write out the clean file to be used in Ex 2 Introduction to SQL
mo_df.to_csv('MO per accident.csv', index = False)
```
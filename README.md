# 120-YEARS-OF-OLYMPIC-HISTORY-PROJECT
Analyzed 120 years of Olympic history using Python, exploring athlete participation, gender representation, Summer vs Winter Games, and country-level participation and medal trends through data cleaning, EDA, and visualization.

Historical data on the modern Olympic Games, from Athens 1896 to Rio 2016. Each row corresponds to an individual athlete competing in an individual event, including the athlete's name, sex, age, height, weight, country, and medal, and the event's name, sport, games, year, and city.

## Table of Content

-	Project Overview
-	Project Objectives
-	Dataset Description and Data Dictionary
-	Data Cleaning and Preprocessing
-	Exploratory Data Analysis (EDA)
-	Analysis Questions, Python Code and Results
-	Visualizations and Interpretations
-	Key Findings
-	Conclusion and Recommendations


## **1. Project Overview**

### Project Description

The 120 Years of Olympic History project involves the exploration and analysis of historical Olympic athlete participation data using Python.
The dataset covers the modern Olympic Games from Athens 1896 to Rio 2016. It contains athlete-level records, including demographic information, National Olympic Committee (NOC), sport, event, Olympic season, year, and medal achievements.
The project focuses on understanding participation patterns, examining differences between the Summer and Winter Olympic Games, and identifying country-level participation and medal trends over time.


### Project Purpose

The purpose of this project is to apply data analytics techniques to a historical Olympic dataset to uncover meaningful patterns and insights about athlete participation, gender representation, and country performance.
Python libraries, including Pandas and Matplotlib, are used to clean, process, analyze, and visualize the data.


### Project Objectives

The main objectives are to:

1.	Examine female athlete participation and visualize how the percentage of female athletes has changed over time.
2.	Compare the Summer and Winter Olympic Games based on athlete participation, participating countries (NOCs), and events.
3.	Identify the countries (NOCs) with the highest athlete participation records.
4.	Compare participation records with medal records to examine whether the most represented NOCs also achieve the highest medal counts.
5.	Analyze and visualize historical country-level participation and medal trends.

   
### Scope of the Project

The analysis covers Olympic athlete participation records from 1896 to 2016, including both Summer and Winter Olympic Games.
The project includes data inspection, data cleaning, missing-value treatment, exploratory data analysis, statistical calculations, and data visualization.
The analysis is limited to the information available in the supplied dataset. Country-level comparisons use National Olympic Committee (NOC) codes, which may represent historical Olympic delegations rather than today's sovereign countries.

## 2. Dataset Overview

### Dataset Description

The dataset used for this project is titled 120 Years of Olympic History. It contains historical records of athletes who participated in the modern Olympic Games from Athens 1896 to Rio 2016. Each row represents an athlete's participation in a particular Olympic event. An athlete may therefore appear in multiple rows if they participated in several events or Olympic editions. The dataset contains demographic information about athletes, their National Olympic Committee (NOC), the Olympic Games they participated in, their sports and events, and their medal achievements.

### Dataset Structure

The original dataset contained 271,116 rows and 15 columns.

After data inspection, duplicate removal, missing-value treatment, and the creation of an additional classification column, the cleaned dataset contained 269,731 rows and 16 columns.

| Dataset Information | Details |
|---|---:|
| Original Rows | 271,116 |
| Original Columns | 15 |
| Cleaned Rows | 269,731 |
| Cleaned Columns | 16 |
| Unique Athletes | 135,571 |
| Olympic Games Editions | 51 |
| Sports | 66 |
| Events (Distinct Event Values) | 765 |
| National Olympic Committee Codes | 230 |

### Data Dictionary

The dataset contains the following columns:

| Column | Description |
|---|---|
| ID | Unique identification number assigned to each athlete. |
| Name | Full name of the athlete. |
| Sex | Gender of the athlete (M = Male, F = Female). |
| Age | Age of the athlete at the time of the Olympic event. |
| Height | Athlete's height measured in centimetres. |
| Weight | Athlete's weight measured in kilograms. |
| Team | Name of the team or delegation represented by the athlete. |
| NOC | Three-letter National Olympic Committee code representing the Olympic delegation. |
| Games | Olympic edition, identified by year and season. |
| Year | Year in which the Olympic Games took place. |
| Season | Olympic season (Summer or Winter). |
| City | Host city of the Olympic Games. |
| Sport | Sport in which the athlete participated. |
| Event | Specific event in which the athlete competed. |
| Medal | Medal awarded to the athlete (Gold, Silver, Bronze, or missing if no medal was recorded). |
| Medal_Status | Additional column created during data cleaning to classify records as Gold, Silver, Bronze, or No Medal. |


#### Important Dataset Considerations

-	The ID column identifies individual athletes, but an athlete can have multiple participation records.
-	Repeated athlete IDs do not automatically indicate duplicate records.
-	NOC represents National Olympic Committee codes. These codes may reflect historical Olympic delegations and should not always be interpreted as modern country names.
-	Missing values in the Medal column indicate that no medal was recorded for that participation. These values were retained and classified using the Medal_Status column.
-	Medal records in this project represent athlete-event records with medals, not necessarily the number of distinct physical medals awarded.
  

## 3. Data Cleaning and Preprocessing

Data cleaning was performed using Python in Google Colab, with the Pandas library.

The objective was to ensure that the dataset was consistent, reliable, and suitable for exploratory data analysis.

### 3.1 Importing the Required Libraries

The following Python libraries were imported:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

#### Purpose of the Libraries

| Library | Purpose |
|---|---|
| Pandas | Data loading, manipulation, cleaning, and analysis. |
| NumPy | Numerical operations and handling missing values. |
| Matplotlib | Creating charts and visualizations. |


### 3.2 Loading and Inspecting the Dataset

The original dataset was loaded into Google Colab and stored in a Pandas DataFrame.

The following inspection methods were used:

```python
Data.head()
Data.shape
Data.info()
Data.describe()
```

#### Inspection results:

-	Original dataset size: 271,116 rows and 15 columns.
-	The dataset contained 10 object columns, 3 float columns, and 2 integer columns.
-	The Age, Height, Weight, and Medal columns contained missing values.
-	The remaining columns had no missing values at the initial inspection stage.
  
The head() method was used to preview the first five records, while shape, info(), and describe() helped examine the dataset structure and numerical distributions.

### 3.3 Identifying and Removing Duplicate Records

Duplicate records were investigated using:

```python
Data.duplicated().sum()
```

The initial inspection identified 1,385 duplicate rows. These were exact duplicate records, meaning the same complete record appeared more than once.

To remove them, the following code was used:

```python
Data = Data.drop_duplicates()
```

The dataset was checked again:

```python
Data.duplicated().sum()
```

**Important decision:**

Repeated athlete IDs were not removed because they represent athletes who participated in multiple events or Olympic editions. The cleaning process targeted exact duplicate rows rather than repeated athlete identities.


### 3.4 Checking Missing Values

Missing values were investigated using:

```python
Data.isnull().sum()
```
The following missing values were identified after duplicate removal:

Result: 0 duplicate rows remained.

After removing duplicates, the dataset contained 269,731 rows.

### Missing Values Summary

| Column | Missing Values |
|---|---:|
| Age | 9,315 |
| Height | 58,814 |
| Weight | 61,527 |
| Medal | 229,959 |
| Other Columns | 0 |

The percentage of missing values was also calculated:

```python
Data.isnull().sum() / len(df)) * 100
```

### Missing Values Percentage

| Column | Missing Percentage |
|---|---:|
| Age | 3.45% |
| Height | 21.80% |
| Weight | 22.81% |
| Medal | 85.25% |


### Observation:

-	Age had a relatively small percentage of missing values.
-	Height and Weight had higher percentages of missing values.
-	Medal had the highest percentage of missing values because most athlete participation records did not result in a medal.

  
## 3.5 Investigating Age Outliers

The Age column was examined to identify unusually high values.

The descriptive statistics showed:

-	Minimum age: 10
-	Median age: 24
-	Maximum age: 97
  
The Interquartile Range (IQR) method was used to investigate potential outliers.
The calculated upper boundary was 38.5 years. Values above this boundary were flagged for further investigation.
Rather than automatically deleting these records, athletes aged 80 and above were examined.
Seven historical records were identified, including athletes involved in Art Competitions.

Examples included:

### Age Outlier Investigation

| Athlete | Age | Olympic Year |
|---|---:|---:|
| John Quincy Adams Ward | 97 | 1928 |
| Winslow Homer | 96 | 1932 |
| Thomas Cowperthwait Eakins | 88 | 1932 |
| George Denholm Armour | 84 | 1948 |
| Robert Tait McKenzie | 81 | 1948 |
| Louis Tauzin | 81 | 1924 |
| Max Liebermann | 80 | 1928 |

#### Cleaning decision:

The high-age records were retained because the investigation did not establish that they were incorrect. Their presence was associated with historical Art Competitions rather than necessarily representing data-entry errors.
This prevented the unnecessary removal of potentially valid historical records.

## 3.6 Handling Missing Values in Age, Height, and Weight

After investigating the missing values and examining the numerical distributions, median imputation was selected to fill the missing numerical values.

The median was preferred because it is less affected by extreme values than the mean.

- Age
  
The overall median age was calculated as 24 years.

Missing Age values were filled using:

```python
Data["Age"] = Data["Age"].fillna(Data["Age"].median())
```

- Height
  
Height was filled using the median grouped by Sex and Sport. This approach helped account for differences in typical height across athlete groups.
Where the group median was unavailable, the overall Height median of 175 cm was used as a fallback.

- Weight
  
Weight was also filled using the median grouped by Sex and Sport.
Where the group median was unavailable, the overall Weight median of 70 kg was used as a fallback.

The following approach was used for both Height and Weight:

```python
Data["Height"] = Data["Height"].fillna(
    Data.groupby(["Sex", "Sport"])["Height"].transform("median")
)
```

```python
Data["Height"] = Data["Height"].fillna(175.0)
```

```python
Data["Weight"] = Data["Weight"].fillna(
    Data.groupby(["Sex", "Sport"])["Weight"].transform("median")
)
```

```python
Data["Weight"] = df["Weight"].fillna(70.0)
```


### Final Missing Values After Cleaning

| Column | Missing Values After Cleaning |
|---|---:|
| Age | 0 |
| Height | 0 |
| Weight | 0 |

This ensured that the three numerical columns had no remaining missing values.


## 3.7 Creating the Medal_Status Column

The original Medal column contained 229,959 missing values.
These missing values were retained because they represented athlete participation records without a recorded medal.

To make medal classification easier during analysis, a new column called Medal_Status was created.

```python
Data["Medal_Status"] = Data["Medal"].fillna("No Medal")
```

The resulting classification was:

### Medal Status Distribution

| Medal Status | Number of Records |
|---|---:|
| No Medal | 229,959 |
| Gold | 13,369 |
| Bronze | 13,295 |
| Silver | 13,108 |
| **Total** | **269,731** |

#### Cleaning decision:

The original Medal column was preserved, while the new Medal_Status column was added to distinguish medal-winning records from participation records without medals.
This made it easier to analyze medal achievements without incorrectly treating missing medal values as data errors.


## 3.8 Final Dataset Validation

After completing the cleaning process, the cleaned dataset was stored in a new DataFrame:

```python
Data_clean = Data.copy()
```

The final dataset was checked to confirm its structure and quality.

### Final Data Validation Results

| Validation | Result |
|---|---:|
| Total Rows | 269,731 |
| Total Columns | 16 |
| Unique Athletes | 135,571 |
| Remaining Exact Duplicate Rows | 0 |
| Missing Age Values | 0 |
| Missing Height Values | 0 |
| Missing Weight Values | 0 |
| Missing Medal Values | 229,959 |
| Missing Medal_Status Values | 0 |

Note: The 229,959 missing Medal values were intentionally retained because they represent athletes who did not win a medal.


## 3.9 Data Cleaning Summary

The cleaning process improved the dataset by removing exact duplicate records, addressing missing numerical values, investigating unusual age values, and introducing a new medal classification column.

The final cleaned dataset contained 269,731 rows and 16 columns, with no remaining exact duplicate rows and no missing values in the numerical columns used for analysis.
The dataset was therefore prepared for Exploratory Data Analysis (EDA).

## 4. Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) was performed to understand the structure of the cleaned dataset, identify important patterns, and generate insights before drawing conclusions.
The analysis was conducted using Pandas for calculations and Matplotlib for data visualization.

## 4.1 High-Level Key Performance Indicators (KPIs)

The first stage of the analysis focused on extracting key metrics that provide an overview of Olympic participation and achievements across the dataset.

The following KPIs were calculated:

### Total Participation Records
  
```python
total_participation_records = len(Data_clean)
print("Total Participation Records:", total_participation_records)
```

### Unique Athletes

```python
unique_athletes = Data_clean["ID"].nunique()
print("Unique Athletes:", unique_athletes)
```

### Olympic Games Editions

```python
olympic_games_editions = Data_clean["Games"].nunique()
print("Olympic Games Editions:", olympic_games_editions)
```

### Number of Sports

```python
number_of_sports = Data_clean["Sport"].nunique()
print("Number of Sports:", number_of_sports)
```

### Number of Events

```python
number_of_events = Data_clean["Event"].nunique()
print("Number of Events:", number_of_events)
```

### National Olympic Committee Codes

```python
number_of_nocs = Data_clean["NOC"].nunique()
print("National Olympic Committee Codes:", number_of_nocs)
```

### Total Medal Records

```python
total_medal_records = Data_clean["Medal"].notna().sum()
print("Total Medal Records:", total_medal_records)
```

### Key Performance Indicators (KPIs)

| KPI | Result |
|---|---:|
| Total Participation Records | 269,731 |
| Unique Athletes | 135,571 |
| Olympic Games Editions | 51 |
| Number of Sports | 66 |
| Number of Events (Distinct Event Values) | 765 |
| National Olympic Committee Codes | 230 |
| Total Medal Records | 39,772 |


### Key Observations:

-	The cleaned dataset contains 269,731 athlete-event participation records.
-	These records represent 135,571 unique athletes, showing that many athletes participated in multiple events or Olympic editions.
-	The dataset covers 51 Olympic Games editions across the Summer and Winter seasons.
-	A total of 66 sports and 765 distinct Event values were identified.
-	The dataset contains 230 distinct NOC codes across its historical coverage.
-	There are 39,772 athlete-event records with an awarded medal.
  
### Interpretation:

These KPIs provide an overview of the scale and coverage of the dataset. They establish a foundation for examining gender representation, seasonal differences, and country-level participation and medal trends.


## 4.2 Gender Participation Analysis

The objective of this analysis was to understand gender representation in the Olympic Games and examine how female athlete participation has evolved over time.

#### 4.2.1 Overall Participation by Gender

The cleaned dataset was grouped by the Sex column to calculate the number of male and female participation records.

Results:

### Athlete Participation by Gender

| Gender | Participation Records | Percentage |
|---|---:|---:|
| Male | 195,353 | 72.43% |
| Female | 74,378 | 27.57% |
| **Total** | **269,731** | **100%** |

### Interpretation:

Male athletes accounted for approximately 72.43% of all participation records, while female athletes accounted for 27.57%.
This indicates that male participation was considerably higher across the historical Olympic records covered by the dataset.

## 4.2.2 Female Participation Over Time

The next analysis examined how the percentage of female participation changed across Olympic years.
The percentage was calculated by dividing the number of female participation records in each year by the total participation records for that year, then multiplying by 100.

Formula:

```python
Female Participation Percentage = (Female Participation Records / Total Participation Records) × 100
```

### Female Participation Over Time

| Olympic Year | Female Participation |
|---|---:|
| 1900 | 1.74% |
| 1952 | 17.97% |
| 1996 | 36.34% |
| 2000 | 39.30% |
| 2008 | 42.76% |
| 2016 | 45.46% |

#### Key Findings:

-	Female participation was very low in the early Olympic editions.
-	In 1900, female athletes accounted for only 1.74% of participation records.
-	By 2016, the percentage had increased to 45.46%.
-	This represents an increase of 43.72 percentage points between 1900 and 2016.
  
#### Interpretation:

The results indicate a substantial increase in female representation in the Olympic Games over time. Although male participation remained higher across the dataset, the growing percentage of female participation reflects a major change in gender representation throughout Olympic history.

### 4.2.3 Visualization

A line chart was used to illustrate the percentage of female participation across Olympic years.

- Chart type: Line Chart
- Reason for selection: A line chart is suitable for displaying changes over time and makes it easier to identify the overall direction and pattern of female participation.

##### Female Olympic Participation Over Time


![Female Olympic Participation Over Time](Female_Olympic_Participation_Over_Time.png)


### 4.3 Summer vs Winter Olympic Games Comparison

The objective of this analysis was to identify differences between the Summer and Winter Olympic Games in terms of athlete participation, participating National Olympic Committees (NOCs), and the variety of events offered.


### 4.3.1 Athlete Participation Comparison

The first comparison examined the number of athlete participation records and unique athletes across the two Olympic seasons.
Results:

| Olympic Season | Participation Records | Unique Athletes |
|---|---:|---:|
| Summer | 221,167 | 116,776 |
| Winter | 48,564 | 18,958 |

### Key Findings:
•	The Summer Olympics recorded 221,167 participation records.
•	The Winter Olympics recorded 48,564 participation records.
•	The Summer Games had approximately 4.55 times as many participation records as the Winter Games.
•	The Summer Games also recorded a higher number of unique athletes.

### Interpretation:
The Summer Olympics had substantially higher athlete participation than the Winter Olympics throughout the dataset's historical coverage. This difference is reflected in both the total participation records and the number of unique athletes.

Visualization:
A bar chart was used to compare the participation records and unique athlete counts between the two Olympic seasons.
![Summer vs Winter Olympic Participation](

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

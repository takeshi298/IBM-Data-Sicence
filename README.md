# SpaceX Falcon-9 Success Landing Prediction
# Outline
* [1.SpaceX-Complete the Data Collection API Lab](https://github.com/takeshi298/IBM-Data-Sicence/blob/main/1.SpaceX-Complete%20the%20Data%20Collection%20API%20Lab.ipynb)
* [2.SpaceX - Web scraping Falcon 9 and Falcon Heavy Launches Records from Wikipedia](https://github.com/takeshi298/IBM-Data-Sicence/blob/main/2.SpaceX%20-%20Web%20scraping%20Falcon%209%20and%20Falcon%20Heavy%20Launches%20Records%20from%20Wikipedia.ipynb)
* [3.SpaceX - Data wrangling](https://github.com/takeshi298/IBM-Data-Sicence/blob/main/3.SpaceX%20-%20Data%20wrangling.ipynb)
* [4.SpaceX - Complete the EDA with SQL](https://github.com/takeshi298/IBM-Data-Sicence/blob/main/4.SpaceX%20-%20Complete%20the%20EDA%20with%20SQL.ipynb)
* [5.SpaceX - EDA with Visualization Lab](https://github.com/takeshi298/IBM-Data-Sicence/blob/main/5.SpaceX%20-%20EDA%20with%20Visualization%20Lab.ipynb)
* [6.SpaceX - Interactive Visual Analytics withFolium lab](https://github.com/takeshi298/IBM-Data-Sicence/blob/main/6.SpaceX%20-%20Interactive%20Visual%20Analytics%20withFolium%20lab.ipynb)
* [7.SpaceX - Build an Interactive Dashboard with Ploty Dash](https://github.com/takeshi298/IBM-Data-Sicence/blob/main/7.SpaceX%20-%20%20Build%20an%20Interactive%20Dashboard%20with%20Ploty%20Dash.ipynb.py)
* [8.SpaceX - Machine Learning Prediction](https://github.com/takeshi298/IBM-Data-Sicence/blob/main/8.SpaceX%20-%20Machine%20Learning%20Prediction.ipynb)

## Project Overview

SpaceX, a leader in the space industry, has revolutionized space travel with its reusable rockets, significantly reducing the cost of launches. This project aims to predict the success of rocket landings using public data and machine learning models, which could be valuable for understanding SpaceX's operations and for competitors looking to bid against them.

## Table of Contents

- [Project Overview](#project-overview)
- [Background](#background)
- [Explore](#explore)
- [Executive Summary](#executive-summary)
- [Methodology](#methodology)
  - [Data Collection - API](#data-collection---api)
  - [Data Collection - Web Scraping](#data-collection---web-scraping)
  - [Data Wrangling](#data-wrangling)
  - [Exploratory Data Analysis with Visualization](#exploratory-data-analysis-with-visualization)
  - [Exploratory Data Analysis with SQL](#exploratory-data-analysis-with-sql)
  - [Maps with Folium](#maps-with-folium)
  - [Predictive Analytics](#predictive-analytics)
- [Conclusion](#conclusion)
- [Additional Considerations](#additional-considerations)

## Background

SpaceX, known for its innovative reusable rockets, offers rocket launches at a fraction of the cost of other providers. By predicting the success of the first stage landing, this project aims to assess the cost-effectiveness of SpaceX launches and explore potential applications for competitors.

## Explore

- Investigate how payload mass, launch site, number of flights, and orbits influence first-stage landing success.
- Analyze the success rate trends over time.
- Identify the best predictive model for landing outcomes (binary classification).

## Executive Summary

This study aims to identify key factors influencing successful rocket landings through the following methodologies:
- **Collect:** Data via SpaceX API and web scraping.
- **Wrangle:** Data to create a binary success/fail outcome variable.
- **Explore:** Relationships through data visualization, focusing on payload, launch site, flight number, and trends.
- **Analyze:** Data using SQL to calculate statistics like total payload and success/fail counts.
- **Visualize:** Launch site success rates and their proximity to geographical markers.
- **Build Models:** Predict landing outcomes using logistic regression, SVM, decision tree, and KNN.

## Methodology

### Data Collection - API

```python
import requests
import pandas as pd

# Request data from SpaceX API
response = requests.get('https://api.spacexdata.com/v4/launches')
data = response.json()

# Convert to DataFrame
df = pd.json_normalize(data)

# Filter for Falcon 9 launches
df_falcon9 = df[df['rocket.name'] == 'Falcon 9']

# Handle missing values
df_falcon9['payload_mass_kg'] = df_falcon9['payload_mass_kg'].fillna(df_falcon9['payload_mass_kg'].mean())

# Export to CSV
df_falcon9.to_csv('falcon9_launch_data.csv', index=False)

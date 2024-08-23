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

## Introduction

SpaceX, a leader in the space industry, strives to make space travel affordable for everyone. Its accomplishments include sending spacecraft to the International Space Station, launching a satellite constellation that provides internet access, and sending manned missions to space. SpaceX achieves this through relatively inexpensive rocket launches, priced at $62 million per launch, thanks to its innovative reuse of the Falcon 9 rocket's first stage. Other providers, unable to reuse the first stage, charge upwards of $165 million per launch. By predicting whether the first stage will land successfully, we can estimate the launch cost. To achieve this, public data and machine learning models can be used to predict whether SpaceX—or a competing company—can reuse the first stage.

## Explore

This project explores the following key questions:

- How do payload mass, launch site, number of flights, and orbits affect first-stage landing success?
- What is the rate of successful landings over time?
- Which is the best predictive model for successful landing (binary classification)?

## Executive Summary

The research focuses on identifying the factors contributing to a successful rocket landing. The following methodologies were employed:

- **Collect** data using SpaceX REST API and web scraping techniques.
- **Wrangle** data to create success/fail outcome variables.
- **Explore** data with data visualization techniques, focusing on factors such as payload, launch site, flight number, and yearly trends.
- **Analyze** the data using SQL to calculate statistics like total payload, payload range for successful launches, and the total number of successful and failed outcomes.
- **Explore** launch site success rates and their proximity to geographical markers.
- **Visualize** the launch sites with the most success and successful payload ranges.
- **Build Models** to predict landing outcomes using logistic regression, support vector machine (SVM), decision tree, and K-nearest neighbor (KNN).

## Results

### Exploratory Data Analysis (EDA)

- **Launch Success:** Launch success has improved over time.
- **Launch Sites:** KSC LC-39A has the highest success rate among landing sites.
- **Orbits:** Orbits such as ES-L1, GEO, HEO, and SSO have a 100% success rate.

### Visualization / Analytics

- **Geography:** Most launch sites are near the equator, and all are close to the coast.

### Predictive Analytics

- **Model Performance:** All models performed similarly on the test set. The decision tree model slightly outperformed others when examining `.best_score_`.

## Methodology

### Data Collection - API

- **Request data** from the SpaceX API for rocket launch data.
- **Decode the response** using `.json()` and convert it to a DataFrame using `.json_normalize()`.
- **Request additional information** about the launches from the SpaceX API using custom functions.
- **Create a dictionary** from the data and **build a DataFrame** from this dictionary.
- **Filter the DataFrame** to include only Falcon 9 launches.
- **Replace missing values** in the Payload Mass column with the calculated mean.
- **Export data** to a CSV file.

### Data Collection - Web Scraping

- **Request data** for Falcon 9 launches from Wikipedia.
- **Create a BeautifulSoup object** from the HTML response.
- **Extract column names** from the HTML table header.
- **Collect data** by parsing HTML tables.
- **Create a dictionary** from the data and **build a DataFrame** from this dictionary.
- **Export data** to a CSV file.

### Data Wrangling

- **Convert outcomes** into binary values (1 for a successful landing and 0 for an unsuccessful landing).

### EDA with Visualization

- **Create charts** to analyze relationships and show comparisons among variables such as payload mass, launch site, and orbit type.

### EDA with SQL

- **Query the data** to gain insights and understand the relationships between different variables.

### Maps with Folium

- **Create maps** to visualize launch sites, view launch outcomes, and analyze their proximity to geographical features.

### Dashboard with Plotly Dash

- **Create an interactive dashboard** with the following features:
  - **Launch Site Dropdown**: Filter data based on the selected launch site.
  - **Success Pie Chart**: Dynamically render a pie chart of launch successes based on the selected site.
  - **Payload Range Slider**: Enable users to select and filter payload ranges.
  - **Success-Payload Scatter Plot**: Visualize the relationship between payload mass and launch success based on the selected payload range.

### Predictive Analytics

- **Create** a NumPy array from the Class column.
- **Standardize** the data using `StandardScaler`. Fit and transform the data.
- **Split** the data using `train_test_split`.
- **Create** a `GridSearchCV` object with `cv=10` for parameter optimization.
- **Apply** `GridSearchCV` on different algorithms: logistic regression (`LogisticRegression()`), support vector machine (`SVC()`), decision tree (`DecisionTreeClassifier()`), and K-nearest neighbor (`KNeighborsClassifier()`).
- **Calculate** accuracy on the test data using `.score()` for all models.
- **Assess** the confusion matrix for all models.
- **Identify** the best model using `Jaccard_Score`, `F1_Score`, and `Accuracy`.

## Conclusion

- **Model Performance:** The models performed similarly on the test set, with the decision tree model slightly outperforming the others.
- **Geographical Insights:** Most launch sites are near the equator, which provides a natural boost due to Earth's rotational speed, reducing the need for extra fuel and boosters. All launch sites are also close to the coast.
- **Launch Success:** Success rates have increased over time.
- **Top-Performing Launch Site:** KSC LC-39A has the highest success rate among launch sites, with a 100% success rate for launches under 5,500 kg.
- **Orbits:** Orbits such as ES-L1, GEO, HEO, and SSO have a 100% success rate.
- **Payload Mass:** Across all launch sites, higher payload mass (kg) is associated with higher success rates.

## Additional Considerations

- **Dataset Expansion:** A larger dataset would help improve the robustness of predictive analytics and determine if the findings can be generalized to a larger set.
- **Feature Analysis / PCA:** Additional feature analysis or principal component analysis should be conducted to see if accuracy can be further improved.
- **XGBoost:** This powerful model was not utilized in this study. Future work could explore whether XGBoost outperforms the other classification models.





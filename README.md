# Used-Car-Price-Prediction
In this application, I will explore a dataset from kaggle. The original dataset contained information on 3 million used cars. The provided dataset contains information on 426K cars to ensure speed of processing. Your goal is to understand what factors make a car more or less expensive. As a result of your analysis, you should provide clear recommendations to your client -- a used car dealership -- as to what consumers value in a used car.

# Business Understanding
The business goal of identifying key drivers for used car prices is reframed as a supervised machine learning problem. Specifically, it is a regression task where the objective is to predict the continuous target variable price of a used car. The features used for prediction include year, manufacturer, model, condition, odometer, fuel_type, transmission, and other relevant variables. 

# Data Understanding
Initial data exploration revealed several insights and quality issues:

price and odometer: High max values and large standard deviations suggest extreme outliers or data entry errors.
Missing Values: Columns like manufacturer, condition, cylinders, fuel, title_status, transmission, type, and paint_color have varying degrees of missing values.
Categorical Features: Many categorical features exist, requiring appropriate encoding.
Data Preparation
This phase involved several steps to clean and prepare the data for modeling:

Handling Outliers: Records with price = 0 were removed. Outliers in price were addressed by filtering the data to price > 100 and price < 70000.
Feature Engineering: The model column was cleaned to extract the first word. Inaccurate records (e.g., cars before 1948 with automatic transmission) were removed.
Missing Value Imputation: Missing values in year, manufacturer, model, condition, cylinders, fuel, odometer, title_status, and transmission were imputed using mode or mean.
Feature Dropping: Irrelevant columns like id, VIN, region, size, paint_color, and drive were dropped.
Duplicate Removal: Duplicate records were removed from the dataset.
Encoding Categorical Variables: Categorical features were handled using Target Encoding for regression models, which converts categorical variables into numerical representations based on the target variable.
Data Splitting: The dataset was split into training and testing sets (70% train, 30% test).

# Modeling
Several regression models were built and evaluated:
Simple Linear Regression with Target Encoding: A baseline model using target-encoded features.
Linear Regression with Polynomial Features and Target Encoding: A more complex model incorporating polynomial features for numerical variables.
Lasso Regression with Polynomial Features and Target Encoding: A regularized linear model to mitigate overfitting and perform feature selection.
Evaluation & Recommendations
Model Performance Summary:
Model	Test MSE	Test R2
simpleRegression	90190746.82	0.49
linearRegressionWithPF	59117526.43	0.67
lassoRegressionWithPF	69442033.23	0.61
Key Observations:
Linear Regression with Polynomial Features demonstrated the best performance with the lowest Test MSE (5.9 x 10^7) and highest Test R2 (0.67), indicating it is the most accurate model among those tested.
Lasso Regression with Polynomial Features performed better than simple regression but not as well as the unregularized linear model with polynomial features.
The similarity between train and test MSEs suggests that overfitting is not a significant issue for these models.

# Top Feature Importances (from Lasso Regression):
feature	importance
model	0.2812
odometer	0.1720
year	0.1505
fuel	0.0369
cylinders	0.0248
state	0.0100
type	0.0086
title_status	0.0050
condition	0.0031
manufacturer	0.0021

# Recommendations for the Used Car Dealership:
Prioritize Vehicle Age and Odometer Reading: year and odometer are highly influential. Newer cars and those with lower mileage command higher prices.
Focus on Manufacturer and Model Variety: manufacturer and model are significant drivers. Understanding the demand for specific brands and models is crucial.
Consider Fuel Type and Transmission: These factors also play an important role in pricing.
Geographic Pricing Strategy (State): Car prices vary by location, suggesting the need for region-specific pricing strategies.
Further Investigation: For more granular insights, consider deeper dives into specific manufacturers, models, and their interactions with other features.

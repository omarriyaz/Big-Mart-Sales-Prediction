# Sales Prediction Using Machine Learning

This project involves analyzing a dataset related to retail sales for BigMart stores, and building a machine learning model to predict sales.

The data scientists at BigMart have collected 2013 sales data for 1559 products across 10 stores in different cities. Also, certain attributes of each product and store have been defined. The aim for this project is to build a predictive model and predict the sales of each product at a particular outlet. Using this model, BigMart will try to understand the properties of products and outlets which play a key role in increasing sales.

## Project Overview

This project aims to:

- Understand the dataset and perform data cleaning.
- Visualize important features affecting the sales.
- Build and evaluate machine learning models to predict retail sales.

## Table of Contents

1. [Dataset Overview](#dataset-overview)
2. [Data Preprocessing](#data-preprocessing)
3. [Feature Cleaning and Engineering](#feature-cleaning-and-engineering)
4. [Handling Categorical Columns](#handling-categorical-columns)
5. [Model Building](#model-building)
6. [Model Evaluation](#model-evaluation)
7. [Conclusions](#conclusions)

## Dataset Overview

- Item_Identifier ---- Unique product ID
- Item_Weight ---- Weight of product
- Item_Fat_Content ---- Whether the product is low fat or not
- Item_Visibility ---- The % of the total display area of all products in a store allocated to the particular product
- Item_Type ---- The category to which the product belongs
- Item_MRP ---- Maximum Retail Price (list price) of the product
- Outlet_Identifier ---- Unique store ID
- Outlet_Establishment_Year ---- The year in which the store was established
- Outlet_Size ---- The size of the store in terms of ground area covered
- Outlet_Location_Type ---- The type of city in which the store is located
- \*Outlet_Type ---- Whether the outlet is just a grocery store or some sort of supermarket
- Item_Outlet_Sales ---- sales of the product in t particular store. This is the outcome variable to be predicted.

## Data Preprocessing

1. **Checking Dataset Dimensions**: The dataset consists of 8,523 rows and 12 columns.
2. **Understanding Data Types and Missing Values**:
   - Checked for missing values using `data.isnull().sum()`.
   - Found that the `Item_Weight` and `Outlet_Size` columns had missing values.
   - Item_weight Column has 1463 (17%) empty values, and Outlet_Size has 2410 (28%) empty values.
3. **Handling Missing Values**:
   - Imputed missing values for `Item_Weight` using linear interpolation.
   - Filled missing values for `Outlet_Size` based on the most frequent value for each `Outlet_Type`.
4. **Duplicate Rows**: There are no duplicate rows in the dataset.

## Feature Cleaning and Engineering

1. **Item_Fat_Content**:
   - The column has four categories, Low Fat, Regular, LF, reg and low fat but really only needs 2, as they are repeating. Thus we replace the values to only have two categories, Low Fat and Regular.
2. **Item_Visibility**:
   - The column has has zero vales, so we replaced the 0 values with NaN, as the Item_Visibility column cannot have 0 values, it is not possible for an item to have 0 visibility.
   - We then fill in NaN values using linear interpolation.
3. **Item_Identifier**:

- The first two letters of Item_Identifier values indicate the type of product, eg FD: Food, DR: Drinks, and NC: Non Consumables, thus we created a column with just those 2 letters.

3. **Outlet Age**
   - Created new features that could potentially improve model performance, Outlet Age, which is derived from the `Outlet_Establishment_Year`.

## Handling Categorical Columns

- Machine Learning algorithms can only understand numerical values, so categorical data needs to be tranformed into numerical data.
- Thus we do Categorical data encoding using ordinal encoding.
- We then store the independent and dependant variables into X and Y.

## Model Building

1. **Model Selection**:

   - Evaluated two models Random Forest Regressor and XGBoost.
   - Random forest regressor cross validation scores came up to <mark>0.5551321920224384</mark> while the XGBRFRegressor scores came to <mark>0.5954521443965901</mark>.
   - Selected XGBoost as its result was closer to 1, indicating that the XGBRF model is better.

2. **Feature Importance**:
   - Used feature importance on the XGBR model to find the 5 most important features.
   - Then dropped the remaining features, on new score was <mark>0.5964214495269795</mark>

## Model Evaluation

- Evaluated the model performance on the validation set using Mean Absolute Error (MAE).
- The MAE came to <mark>713.5643497364571</mark>
- This means on average the absolute difference between the predicted values and actual values is 713.56, this suggest that the model is off by 713.56 units from the actual value.
- We then predict the sales using unseen data, this prediction is in a range of +-MAE.

## Conclusions

The project successfully identified key factors affecting retail sales and built a robust predictive model using XGBoost, achieving a satisfactory MAE score.

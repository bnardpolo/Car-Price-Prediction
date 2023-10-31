# Car-Price-Prediction
Car Price Prediction
# Rusty Bargain Car Price Prediction

Rusty Bargain used car sales service is developing an app to attract new customers. In that app, you can quickly find out the market value of your car. You have access to historical data: technical specifications, trim versions, and prices. You need to build the model to determine the value.

## Project Description

Rusty Bargain is interested in:

- The quality of the prediction
- The speed of the prediction
- The time required for training

**Goal**: Build a few regression models, and compare their quality of prediction, speed of prediction, and time required to train. The best model will be used to predict the price of a car.

## Data Overview

- Each observation describes a model of a car; there are 354,369 cars and 16 features.
- The top 2 features with missing values are: NotRepaired (20%) and VehicleType (11%).
- 262 (0.07%) of the records are duplicated.
- Numerical summary shows outliers for Price, RegistrationYear, and Power. The NumberOfPictures feature has no data.

**Possible Fixes**:

1. Analyze Power: Cap the lower range to 100 HP and the higher end to 2000 HP.
2. Cap the lower end of Price to EUR 50.
3. For RegistrationYear, set the lower bound to 1900 and the upper bound to 2021.
4. Replace RegistrationMonth with the probability of occurrence of the other months.
5. Populate FuelType and VehicleType using a CatBoostClassifier model.

## Data Insights

1. RegistrationYear has a moderately strong positive correlation with Price.
2. Power has a moderately strong positive correlation with Price.
3. Mileage is negatively correlated with Price.
4. Among the categorical features, Brand and Model have a positive correlation.

## Data Preprocessing

1. Created new fields, including the number of days the ad appears on the site.
2. Populated missing categorical features based on the frequency distribution.
3. Removed duplicates and outliers.
4. Encoded categorical features for modeling.

## Model Training

1. Trained RandomForestRegressor and CatBoostRegressor using GridSearch with 5-fold cross-validation.
2. Only one hyperparameter (n_estimators/iterations) was tuned for efficiency.

**Results**:

- RandomForestRegressor took the longest training time (924 seconds) but had the best RMSE on the validation set (EUR 1719).
- CatBoostRegressor is fast (1.89 seconds) but slightly overfit, offering multiple hyperparameters for improvement.
- LinearRegression was the fastest but had a higher RMSE.

## Model Evaluation

1. Tested the best models on the test set.
2. Found that RandomForestRegressor had the best RMSE, but predictions took 280 milliseconds.
3. All models showed slight overfitting.

## Conclusion

Rusty Bargain needs to choose between a 7x increase in training time and a ±1.1x increase in RMSE when deciding between RandomForestRegressor and CatBoostRegressor. Considering its speed and the available hyperparameters, CatBoostRegressor is recommended for better evaluation metrics.

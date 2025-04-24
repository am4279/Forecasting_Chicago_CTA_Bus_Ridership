This file contains EDA and 6 models of the Chicago CTA "Ridership - Bus Routes - Monthly Day-Type Averages & Totals" dataset. These models forecast bus ridership using data from 2001 to 2020. The data sets are all split into train (1/1/2001 - 12/1/2015) and test (1/1/2016-11/01/2020).

Most of the models use only the Bus Route dataset with some feature engineering including the day of the week, quarter, month, year, day of the year, day of the month and week of the year. However, the multivariate vector autoregression (VAR) model merges the bus route data with temperature and average gas price data.

All data is finally merged with fare prices in order to calculate revenue and ultimately revenue lost during the pandemic.

About CTA ridership numbers
Ridership statistics are provided on a system-wide and bus route/station-level basis. Ridership is primarily counted as boardings, that is, customers boarding a transit vehicle (bus or rail). On the rail system, there is a distinction between station entries and total rides, or boardings. Datasets indicate such in their file name and description.

How people are counted on buses
Boardings are recorded using the bus farebox and farecard reader. In the uncommon situation when there is an operating error with the farebox and the onboard systems cannot determine on which route a given trip's boardings should be allocated, these boardings are tallied as Route 0 in some reports. Route 1001 are shuttle buses used for construction or other unforeseen events.

Datatype
Daytype fields in the data are coded as "W" for Weekday, "A" for Saturday and "U" for Sunday/Holidays. Note that New Year's Day, Memorial Day, Independence Day, Labor Day, Thanksgiving, and Christmas Day are considered as "Sundays" for the purposes of ridership reporting. All other holidays are reported as the type of day they fall on.

Both fare and average gas proces are measured in dollars, and temperature is measured in degrees farenheit.

Fare Prices
full = 2.50

reduced = 1.25

student = 0.75

Exploratory Data Analysis
I had a centralized EDA so much of that analysis is not included here but is included in other files. The sole EDA done in this file is checking for stationarity and differencing the data to achieve stationarity.

VAR Models
There are two VAR models. The first looks at the interaction between average gas prices and ridership. And the second looks at the interaction between temperature and ridership. The Granger Causality test is performed to determine causality and the Coint-Johansen test is performed to examine cointagration.

XGBoost Models
An XGBoost models is built as a base model using the features engineered discussed before. Then the feature importance is plotted and analyzed followed by a grid search for the best parameters. Finally, the model is run using the best parameters determined by the grid search.

Machine Learning Models
First, an program is run that calculates the r2 scores of 5 different SKLearn models: Linear Regression, Lasso regression, Random Forest, Decision Tree and KNN. The r2 scores for each are then compared to get a general sense for how well the models perform relative to each other. (Note: the r2 scores and other assessments calulated here are based on the models before reconverting the models back to their original units prior to differencing).

Second, an in depth analysis of each of the models is performed followed by a conversion of the results back to their original units. After that the models are assessed based on their RMSE, MSE, MAE, MAPE, and SMAPE. Then, the models are used to forecast both revenue based on 60-20-20 composition of riders. That is, 60% riders pay full price, 20% pay a reduced price and 20% pay the student price. Finally, I use the expected ridership to estimate the revenue lost due to the pandemic.

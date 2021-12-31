# Stock-Prediction-Time-Series-Data-Analysis

### Regression Model:

a. Assumptions:

The relationship between High, Low, Open, Volume together with Close is assumed to be linear, we also later proved this by calculating the correlation between all columns of the given dataset
Eventhough the columns High, Low, Open have a high correlation between each other, we are considering all of them to predict close value
We took multicollinearity into consideration while predicting only for Ridge and Lasso

b. Model Chosen with Rationale:

We tested Ridge regression, Lasso regression, XGBoost and Multiple Linear Regression. We chose Multiple Linear Regression as our model as:

This model did not overfit the data as much as the other models.
Gave the best estimation between coeffecients of the independent variables (as there is a strong linear relationship between close and Open, High and Low)
As there is a strong linear relationship between the independent varibales and dependent variable, multiple linear regression makes the most sense

c. Parameters

We made use of Pipeline along with StandardScaler and LinearRegression to train our model of the entire train dataset

### Time Series Model

a. Assumptions

We use the ARIMA (2,1,1) model for prediction which removes the trend component
We found that the dataset is not stationary having both a trend and seasonal component
We do not consider the seasonal component

b. Model Chosen with Rationale

With the help of acf and pacf plot, we found that p=1 and q=1
With the help of auto arima, we found the optimal model: ARIMA(2,1,1) for training the model
LSTM was also tested on the dataset as it was seen to be the best model during research for time series analysis

c. Parameters

p=2, d=1, q=1, m=0, P=0, D=0, Q=0

### Comparison between Regression and Time Series models

a. Based on validation performance metrics

We ended up choosing the MLR model (RMSE=1.68) as we got a lower RMSE value for the given test data when compared to the ARIMA(2,1,1) model (RMSE=32.4)

b. Which model is more suitable for the data? (account for not just best performance metrics, but handling of fluctuations of data as well)

Eventhough SARIMA seems like the better option to consider the seasonality and trend component during prediction, the RMSE values obtained by the Multiple Linear Regression model was much lesser than the ARIMA value. We obtained the values p=1 and q=1 from the PACF and ACF graphs respecively and used those as the base values for our model. As auto-ARIMA gives better and accurate results, we used the model generated from auto-ARIMA. The obtained ARIMA model was ARIMA(2,1,1) and this does not consider the seasonality changes, a very important factor. On performing seasonal decomposition on the given data set, we found that the time period for one seasonal cycle is 43-45 days (1 and a half months). When provided to the auto-ARIMA module, it still did not consider the seasonality of the data to perform predictions. When we tried changing P, D, Q and m values (m=45 or m=365), we got a system ran out of memory exception.

c. Reasoning for what model is chosen to predict test (hidden) data

According to our analysis, MLR gave better prediction and thus a lower RMSE value as fluctuations due to the seasonality component was captured well. The ARIMA model generated did not capture the seasonality component hence giving us a greater RMSE value as compared to the Multiple Linear Regression model. Since there was a high correlation between the Open, High, Low and Close values, we know a linear relationship exists between them. Hence, Multiple Linear Regression came out as the best model. We therefore followed the Occam's razor principle and decided on MLR.

RMSE FOR THIS MODEL WHEN SUBMITTED WAS 32.74 when we trained it for the entire training data to predict test data

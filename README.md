# Time Series Analysis and Forecasting of Household Energy Usage
## Summary and Objective
This project consists of analyzing the household energy usage and building different types of forecasting models to predict future usage. It is important to know the amount of household energy usage to strategically estasblish and adopt energy saving strategies. Energy saving strategies will overall reduce energy usage and lead to saving money. 

### Objective
The purpose of this project is to understand the amount of energy used over 2 years, find usage patterns, and select best forecasting model.

### Data Description
This data collected in San Jose using smart meters. Data consists of 8 columns:
    
    TYPE - This is an information column. The value is 'Electric usage' for all the observations.
    DATE - Date of electric consumption. There is no timestamp in this field.
    START TIME - Start time of the consumption.
    END TIME - End time of the consumption
    USAGE - Consumption in kWh
    UNITS - This column denotes measurement unit. It is kWh for all the observations.
    COST - Cost of consumption in $.
    NOTES
    
    The data can be accessed here: https://www.kaggle.com/datasets/jaganadhg/house-hold-energy-data

### Methods Used and Exploratory Analysis
The data is prepared by deleting irrelevant columns and checked for any missing values. The column of concentration is USAGE. The data is converted into time series by setting the index to datetime and frequency is changed to daily. Primarily, USAGE and COST columns are plotted to analyze their daily, monthly, and quarterly relationship. Furthermore, USAGE trend is inspected for trend/autocorellation, heteroscedasticity, and seasonality.

Next step requires to transform the USAGE to a stationary data. Three methods used to achieve the transformation include decomposition method, log transform, and differencing. Sequence plotting and ADF test is used to evaluate stationarity to select the data for forecasting. Note: Not every forecasting model will require stationary data to be used. ACF and PACF are plotted to find the orders of AR and MA.

The data is split into train and test subsets. Train subset is used fit into the four forecating models: including two ARIMA models, Triple Exponential Smoothing model, and Facebook Prophet model. The next 10 dates are predicted using each model and compared to the test subset with corresponding dates. The models are evaluated using sequence plotting and mean squared error. 

## Results

### Summary of the Models Used and Best Model
Total of four models are trained and analyzed using sequence plotting and MSE value. 

    Model 1: ARIMA model with order (3,0,3) as indicated by ACF and PACF plot is trained using stationary data. 
    Model 2: ARIMA model with order (3,0,0) resulted from auto arima module from import pmdarima library is trained using stationray data.
    Model 3. Triple Exponential Smoothing treated as additive and trained using non-stationary data. This model is used becaues data showed both trend and seasonality.
    Model 4. Prophet model trained using stationary data.
    
    Best Model: Arima, Auto Arima, and Prophet model were all similar in performance, but Arima model did perform a little better based on its MSE value. However, Triple Exponential captures the pattern of the test data better compared to other models even though its MSE value is much higher.
    

### Key Findings and Insight
 - The pattern of usage and energy cost follow a similar pattern, mean that when one increases the other increses as well. 
 - The energy usage peaks during months of January and drops to minimum during December. Further analysis can be conducted to understand the reason and provide insights on improvements to prevent over usage. 
 - The usage data contains both trend/autocorrelation, heteroscedasticity, and seaonality. These components are decomposed to obtain the residuals as the stationary data.
 - Arima model is best in performance based on MSE value but Triple Exponential is better at capturing the pattern of the test data.

### Recommendation/Next Steps:
 - The current project analyzed the data as a daily frequency, however, the original data was collected in fifteen minute intervals. This data can be analyzed to really undertand the hourly usage in different times of the day. This will provide more detail on customer activity. 
 - Current project concentrated on univarate analysis and forecasting, but multivarate analysis can be done to include multiple factors during forecasting. 
 - The current data ranges over two years but having data that ranges for multiple years can be better to train a forecasting model.
 - Using more sophisticated forecasting models or making the current models more complex (without overdifferencing and overfitting) can lead to better performance. 

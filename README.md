# Timeseries analysis using ARIMA model vs LSTM 

This project is evaluates the use of ARIMA model for time series analysis in comparison to LSTM machine learning technique. 

The dataset used is provided by the official Washington state open data portal, orginating from the research and analysis office in the Department of Licensing. This data includes historical electrical vehicle population counts form January 2017 through September 2024. There is a total of 7 years of data and 92 data points.

Variables: Date, Plug-In Hybrid Electric Vehicle (PHEV) count, Battery Electric Vehicle (BEV) Count, Electric Vehicle (EV) Total

Here is our plotted data. We can see that it looks non-linear and non stationary. 
![Raw Data](Images/plot_raw_data.png)


Time series models such as ARIMA and SARIMA require data to be stationary. We first take the log of the data to stabilize the variance and linearize the exponential growth. Then we take the difference of the data to remove trends and seasonality to try to acheive stationarity.
![Log-First Difference](Images/first_diff.png)

We run an augmented Dickey-Fuller test to check for stationarity.
Results:
ADF Statistic -2.816328149227266
p-value 0.05597899517932277
Critical Values {'1%': -3.506057133647011, '5%': -2.8946066061911946, '10%': -2.5844100201994697}

H0: The time series is non-stationary
HA: The times sereis is stationary
Our test statistic is greater than our critical value at 5% confidence level -2.816 > -2.894, the p-value is slightly creater than 0.05 at 0.056. We fail to reject he null hypothesis, however the time series is very close to stationary. At the 10% level it is considered stationary.

Since taking the log then differencing did not make is stationary, we take a second difference 



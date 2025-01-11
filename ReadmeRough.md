# Time Series Analysis of Louisiana's Gambling Revenue

## Table of Contents
- [Exploratory Analysis](#exploratory-analysis)
- [Data](#data)
- [Methodology](#methodology)
- [Model Evaluation](#model-evaluation)

## Introduction
The objective of this project is to evaluate and compare forecasting methods to achieve the highest accuracy forecast of the monthly revenue of Harrah’s casino located in New Orleans, Louisiana. The models considered are ARIMA, ARIMAX, ETS, and Meta’s Prophet. We will evaluate the model performance in forecasting revenue one month, 6 months, and 1 year out. 

This dataset posed an interesting problem as it contains two back-to-back outliers. One was a result of COVID lockdown in the spring of 2020 and the second was a result of Hurricane Ida the following year. 

****Insert summary of results

## Explorator Analysis 

Figure 1 is our dataset plotted across time. From visual inspection we can see a general downward trend, and we can see the effects of the pandemic lockdowns begining March of 2020 and the gradual return of revenue as the state slowly reopened. A stay-at-home order was implemented in March 23, 2020. As a result Harrah's monthly revenue in the March of 2020 was __% less than March of the previous year. Harrah's reported zero revenue for the months of April and May as the lockdowns continued to be in effect. Harrah's reopened when the state transistion to phase 2 of reopening on June 5th, 2020[wikipedia]. In the month of June, Harrah's reported a revenue that was 75% less than the same month in the previous year. From our data we can see that by the following March 2021, it had returned to pre-lockdown revenues until there was dramatic dip again starting August of 2021. This was likely due to hurricane Ida which caused widespread power outages, wind damage, localized flooding. Many residents decided to evacuate the area before the storm.

<p align="center">
<img src="Images/plot_raw.png" alt="Figure 1" width="600"><br>Figure 1
</p>

Seasonality is not obvious from visual inspection. I inspected for seasonality in figure 2 using a seasonal plot. It shows the monthly gaming revenue across the months by year. From visual inspection there is a lot of variability each month between the year, with no indication of seasonality. 

<p align = "center">
  <img src="Images/plot_raw_year.png" alt="Figure 2" width="600"><br>Figure 2
</p>

Seasonal trend decomposition with Loess, or STL, was then used on the imputed data to look for any underlying patterns. STL was chosen over other methods of decomposition such as X-11 for its flexibility. It is robust with missing values and outliers, and does not follow strict assumptions about periodicity. From figure 4 we can get a sense of whether the error, trend, and seasonality components are additive, multiplicative, or if a trend or seasonality is absent. When a component is additive it means that the components variation stays relatively the same over time, it is multiplicative when the variation scales with data. Whether these components are additive or multiplicative is particularly relevant to the ETS model as it accounts for how trend, seasonality, and error components combine to create the time series. 

<p align="center">
  <img src="Images/plot_stl.png" alt="Figure 2" width="600"><br>Figure 3
</p>  

## Data 

The dataset was created from the monthly revenue reports provided by the <a href="https://lgcb.dps.louisiana.gov/revenue_reports.htm" target="_blank">Louisiana Gaming Control Board</a>. The dataset is composed of the reported monthly gross gaming revenue from Harrah's casino spanning from January 2007 to September 2024, totaling 213 data points. 

Data Preprocessing
In dealing with the outliers data I considered a few options, the simplest being keeping the data points as is or imputation. The tsclean function from the forecast package in R was used to detect outliers. The tsclean function applies Loess smoothing method creating a smoothed version of the timeseries and flags observations as outliers based on the reisduals. After detection it then performs imputation using linear interpolation. The models were also trained using the non-imputated data and the resulting RMSE and MSE values were considerably better using the non-imputated data. 

An exogenous dummy variable was created for the ARIMAX model to account for COVID-19 lockdowns and Hurricane Ida. The dummy variable indicated April and May as Covid lockdown dates, and March of 2021 for Hurrican IDA. Prophet has feature that can treat shocks from events such as COVID-19 and hurricane Ida as one off Holidays that can account

The tsclean function flagged and imputated the two observations where zero revenue was reported in April and May. Figure 4 is the timeseries after imputation.

<p align = "center">
  <img src="Images/plot_imputed.png" alt="Figure 2" width="600"><br>Figure 4
</p>

An exogenous dummy variable was created for the ARIMAX model to account for COVID-19 lockdowns and Hurricane Ida. The dummy variable indicated April and May as Covid lockdown dates, and March of 2021 for Hurrican IDA. Prophet has a feature that can treat shocks from events such as COVID-19 and Hurrican Ida as one off Holidays without the creation of an exogenous variable. 

## Methodology

ARIMA and ARIMAX

In order to use the ARMA model the data needs to be stationary with a constant mean across time and constant variance. A Dickey-Fuller test was conducted on the imputed and logged data to check for stationarity. The following is the result of our ADF test. 
  
  | Dickey-Fuller | Lag Order | P-Value | 
  |---------------|-----------|---------|
  | -5.0204       | 5         | 0.01    |
  
Our test statistic tells us how far the data is from a unit root. A unit root is a stochastic trend in a time series that indicate that a value will be highly dependent on its past values, the presence of a unit root indicates that it is non-stationary. The negative number suggests that it further from a unit root and that our series is stationary.  Our alternative hypothesis is stationarity, our p-value is <0.05 so we can reject the null-hypothesis. 

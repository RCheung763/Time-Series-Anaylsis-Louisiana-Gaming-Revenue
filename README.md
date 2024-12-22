# Time Series Analysis of Louisiana's Gambling Revenue

## Table of Contents
- [Data](#data)
- [Methodology](#methodology)
- [Exploratory Analysis](#exploratory-analysis)
- [Modeling](#modeling)

## Introduction
The objective of this project is to identify and evaluate forecasting methods to achieve the highest accuracy in forecasting the monthly revenue of Harrah's casino located in New Orleans, Louisiana. The models considered were ARMA, GARCH, prophet, and a LSTM Network. 

## Data  
The dataset was created from the monthly revenue reports provided by the <a href="https://lgcb.dps.louisiana.gov/revenue_reports.htm" target="_blank">Louisiana Gaming Control Board</a>. The dataset is composed of the reported monthly gross gaming revenue from Harrah's casino spanning from January 2007 to September 2024, totaling 213 data points. 

Data Preprocessing

Two steps were taking for data preprocessing. First, imputation was required for observed outliers that resulted from two significant drops in revenue. First was the result of COVID lockdowns in 2020. A stay-at-home order was implemented in March 23, 2020 as a result Harrah's monthly revenue in the March of 2020 was __% less than March of the previous year. Harrah's reported zero revenue for the months of April and May after the lockdowns continued to be in effect. Harrah's reopened when the state transistion to phase 2 of reopening on June 5th, 2020[wikipedia]. In the month of June Harrah's reported a revenue that was 75% less than the same month in the previous year.

In dealing with COVID era data I considered a few options, the simplest being keeping the COVID era data or completely removing it. I also considered creating a dummy varaible for pre-COVID data and post-COVID data, but the difficulty in that was defining when post-COVID begins. Also, from our data we can see that by the following March 2021, it had returned to pre-lockdown revenues until there was dramatic dip again starting August of 2021. This was likely due to hurricane Ida which caused widespread power outages, wind damage, localized flooding. Many residents decided to evacuate the area before the storm. 

Rather than completely removing hurricane/covid era data points but in an effort to preserve the information provided by these significant events, linear interpolation was utilized to impute for the months of March, April, May, and June of 2020 and September of 2021. The result was a reduction in the magnitude of these outliers. After our exploratory analysis, the imputed data was tranformed using natural log to stabilize the variance prior to training the models. The Dickey-Fuller test done using the imputed and logged data. 



## Exploratory Analysis

Figure 1 is Harrah's month gross gaming revenue. From visual inspection we can see a general downward trend, and we can see the effects of the pandemic lockdowns begining March of 2020 and the gradual return of revenue as the state slowly reopened.  
<p align="center">
<img src="Images/plot_raw.png" alt="Figure 1" width="600">
</p>

Figure 1

Seasonality is not obvious in the time plot of our data. I inspected for seasonality in figure 2 using a seasonal plot. It shows the monthly gaming revenue across the months by year. From visual inspection there is a lot of variability each month between the year, with no indication of seasonality. 

<p align = "center">
  <img src="Images/plot_raw_year.png" alt="Figure 2" width="600">
</p>
Figure 2
Figure 3 shows the data after the largest outliers, revenue from April, May, and June of 2020 and September of 2021, was replaced using linear interpolation as described in the data section. 

<p align = "center">
  <img src="Images/plot_imputed.png" alt="Figure 2" width="600">
</p>
Figure 3
Seasonal trend decomposition with Loess, or STL, was then used on the imputed data to look for any underlying patterns. STL was chosen over other methods of decomposition such as X-11 for its flexibility. It is robust with missing values and outliers, and does not follow strict assumptions about periodicity. Figure 4 shows the data decomposed into trend, season, and residuals. From the trend panel we can see more clearly the extent of the decreasing trend. The seasonal panel shows that there is some seasonality to this data but it is not constant over time. In our remainder panel we can still see some of the dips and peaks in the remainder that are in our dataset, which means that some of the structure of the data is not captured by STL decomposition 
<p align="center">
  <img src="Images/plot_stl.png" alt="Figure 2" width="600">
</p>  

 Figure 4
## Methodology
In order to use the ARMA model the data needs to be stationary with a constant mean across time and constant variance. The GARCH model also requires that the mean is constant across time.
A Dickey-Fuller test was conducted on the imputed and logged data to check for stationarity. This is the result of our ADF test. 

  
  | Dickey-Fuller | Lag Order | P-Value | 
  |---------------|-----------|---------|
  | -4.7          | 5         | 0.01    |
  
Our test statistic tells us how far the data is from a unit root, a negative number points to stationarity. Our alternative hypothesis is stationarity, our p-value is <0.05. We can reject the null-hypothesis. An ACF plot however shows a more gradual decline to zero which suggests non-stationarity. When the data is differenced an ADF test still the ACF no longer suggests non-stationarity, however the PACF has several significant spikes as a result of the differencing 

## Modeling


















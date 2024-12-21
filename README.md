# Time Series Analysis of Louisiana's Gambling Revenue

## Table of Contents
- [Data](#data)
- [Methodology](#methodology)
- [Exploratory Analysis](#exploratory-analysis)
- [Modeling](#modeling)

## Introduction
<p> The objective of this project is to identify and evaluate forecasting methods to achieve the highest accuracy in forecasting the monthly revenue of Harrah's casino located in New Orleans, Louisiana. The models considered were ARIMA, exponential smoothing model, GARCH, and a LSTM Network. 

## Data  
<p>The dataset was created from the monthly revenue reports provided by the <a href="https://lgcb.dps.louisiana.gov/revenue_reports.htm" target="_blank">Louisiana Gaming Control Board</a>. The dataset is composed of the reported monthly gross gaming revenue from Harrah's casino spanning from January 2007 to September 2024, totaling 213 data points. 

Data Preprocessing

Two steps were taking during data preprocessing. First, imputation was required for observed outliers that resulted from COVID lockdowns in 2020. A stay-at-home order was implemented in March 23, 2020 as a result Harrah's monthly revenue in the March of 2020 was __% less than March of the previous year. Harrah's reported zero revenue for the months of April and May after the lockdowns continued to be in effect. Harrah's reopened when the state transistion to phase 2 of reopening on June 5th, 2020[wikipedia]. In the month of June Harrah's reported a revenue that was 75% less than the same month in the previous year. Completely removing this covid era and imputation of the covid era data was considered, but in an effort to preserve the information provided by this shock, linear extrapolation was utilized to impute fo the months of April, May, and June. The seccond step taken was transforming the data using natural log to stabilize the variance. 

</p>


## Exploratory Analysis

Figure 1 is Harrah's month gross gaming revenue. From visual inspection we can see a general downward trend, and we can see the increased period of volatility begining March of 2020 when the COVID-19 pandemic lockdowns went into effect.  

![Figure 1](Images/plot_raw.png)
Figure 1

We inspect further for seasonality in figure 2 using a seasonal plot. It shows the gaming revenue across the months by year. It shows us the monthly gaming revenue by year. From visual inspection there is a lot of variability each month between the year
![Figure 2](Images/plot_raw_year.png)

## Methodology

## Modeling


















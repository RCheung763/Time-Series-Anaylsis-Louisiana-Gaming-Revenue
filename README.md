# Time Series Analysis of Louisiana's Gambling Revenue

## Table of Contents
- [Data](#data)
- [Methodology](#methodology)
- [Exploratory Analysis](#exploratory-analysis)
- [Modeling](#modeling)

## Introduction
<p> The objective of this project is to identify and evaluate forecasting methods to achieve the highest accuracy in forecasting the monthly revenue of Harrah's casino located in New Orleans, Louisiana. In addition to that forecast this project will also utilize the available data to forecast and invesitage the potential relationship between the monthly revenue of sports betting and the revenue from fantasy sports. 

## Data  
<p>The data was acquired the <a href="https://lgcb.dps.louisiana.gov/revenue_reports.htm" target="_blank">Louisiana Gaming Control Board</a>. The first dataset is the reported monthly gross gaming revenue from Harrah's casino spanning from January 2007 to September 2024, totaling 213 data points. The operation for online casino gaming began in Louisiana on October 12th, 2021. The monthly revenue data for sports and fantasy sports betting spans November 2021 to September 2024. 

Data

As a result of the COVID-19 shutdown Harrah's monthly revenue dropped 61% between the months of Februrary and March of 2020 and reported zero revenue for the months of April and May. Harrah's reopened in the month of June reporting a revenue that was 75% less than the same month in the previous year. Completely removing this covid era and imputation of the covid era data was considered, but in an effort to preserve the information provided by this shock, linear extrapolation was utilized to impute fo the months of April, May, and June. This was the only pre-processing step necessary. </p>


## Exploratory Analysis

Figure 1 is Harrah's month gross gaming revenue. From visual inspection we can see a general downward trend, and we can see the increased period of volatility begining March of 2020 when the COVID-19 pandemic lockdowns went into effect.  
Figure 1
![Figure 1](Images/plot_raw.png)

We inspect further for seasonality in figure 2 using a seasonal plot. It shows the gaming revenue across the months by year. It shows us the monthly gaming revenue by year. From visual inspection there is a lot of variability 

## Methodology

## Modeling


















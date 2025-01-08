# Time Series Analysis of Louisiana's Gambling Revenue

## Table of Contents
- [Data](#data)
- [Methodology](#methodology)
- [Exploratory Analysis](#exploratory-analysis)
- [Model Evaluation](#model-evaluation)

## Introduction
The objective of this project is to evaluate and compare forecasting methods to achieve the highest accuracy forecast of the monthly revenue of Harrah’s casino located in New Orleans, Louisiana. The models considered are ARIMA, ETS, and Meta’s Prophet. We will evaluate the model performance in forecasting revenue one month, 6 months, and 1 year out. 

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

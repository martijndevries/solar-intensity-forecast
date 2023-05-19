# Project 4 - Solar Intensity Forecasting

By Andres Aguilar, Martijn de Vries, and William Lopez

## Problem Statement

One of the problems faced with integration of renewable energies into the power grid is the reliability of power output forecasting from sources such as wind and solar. As data scientists, we have been tasked by the energy company PG&E with creating reliable predictions for solar intensity, which directly correlates to solar power output.
Using weather data from the National Solar Radiation Database, we will build a predictive model to forecast the solar intensity in Los Angeles, one day in advance. We will use Mean Absolute Error to evaluate the success of our model, and compare them against a benchmark model of a solar intensity curve on an average day. Our predictive model can then be used to determine the amount of solar power that can be generated on a given day, such that other, non-renewable sources of energy production can be throttled or ramped up accordingly.

## Repository Overview
    
This repository consists of the following:

<ul>
   <li> The directory <code>./code</code> contains X notebooks that go through each of the steps of the analysis: 
   
   <ol>
    <li> In <b>data_collection.ipynb</b>, we collected 5 years of weather data from the NSRDB database </li>
    <li> In <b>EDA.ipynb</b> we look at the data and investigate seasonal trends. We also engineer several new features </li> 
    <li> .... </li>
   </ol>
  <li> The directory <code>./data</code> contains 1) the dataframe as collected from the NSRDB, and 2) the cleaned, feature engineered dataframe that is used for the various models.
   <li> The directory <code>./figures</code> contains all the figures that are saved during the analysis in the notebooks, in .png formats </li>
    <li> The slides for the project presentation are in the file <code>project4_solar.pdf</code> </li>
</ul>

## Background

Write here why solving this problem is important

## Data Dictionary


|Feature|Type|Dataset|Description|
|---|---|---|---|
|Dew Point| Numerical |NSDRB 
|Pressure| Numerical |NSDRB 
|Relative Humidity| Numerical |NSDRB 
|Temperature| Numerical |NSDRB 
|Wind_x| Numerical | NSDRB | X-component of wind velocity. Feature engineered from Wind direction and speed|
|Wind_y| Numerical | NSDRB | y-component of wind velocity. Feature engineered from Wind direction and speed|
|Day Seasonality | Numerical | NSDRB | Sinoid function that captures daily variance in the GHI. Feature engineered |
|Year Seasonality | Numerical | NSDRB | Sinoid function that captures yearly variance in the GHI. Feature engineered |
|Cloud Type | Categorical | NSDRB | Categorical variable indicating type of cloud. See notebook for more details |
|GHI| numerical| NSDRB| ***Target variable***- Global Horizontal Irradiance|


## Data Collection and EDA

To collect the data, we used

## Modeling

## Insights

## Conclusions

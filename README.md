# Project 4 - Solar Intensity Forecasting

By Andres Aguilar (insert email here)<br> 
Martijn de Vries (martijndevries91@gmail.com) <br>
and William Lopez (insert email here)

## Problem Statement

One of the problems faced with integration of renewable energies into the power grid is the reliability of power output forecasting from sources such as wind and solar. As data scientists, we have been tasked by the energy company PG&E with creating reliable predictions for solar intensity, which directly correlates to solar power output.

Using weather data from the National Solar Radiation Database, we will build a predictive model to forecast the solar intensity in Los Angeles, one day in advance. We will use the root mean squared error and the mean absolute error to evaluate the success of our model, and compare the model scores  against a benchmark model of a solar intensity curve on an average day. Our predictive model can then be used to determine the amount of solar power that can be generated on a given day, such that other, non-renewable sources of energy production can be throttled or ramped up accordingly.

## Repository Overview
    
This repository consists of the following:

<ul>
   <li> The directory <code>./code</code> contains 6 notebooks that go through each of the steps of the analysis: 
   
   <ol>
    <li> In <b>data_collection.ipynb</b>, we collected 5 years of weather data (2016 - 2020) from the NSRDB database </li>
    <li> In <b>EDA.ipynb</b> we look at the data and investigate seasonal trends. We also engineer several new features </li> 
    <li> In <b>RNN_model.ipynb</b>, we use a Recurrent Neural Network to forecast the GHI 1 day into the future, based on the weather data from the previous 4 days </li>
    <li> In <b>WaveNet_model.ipynb,</b> we apply a modified version of Google's generative WaveNet model to forecasting GHI 1 day in the future based on the weather conditions on the previous 10 days.   </li>
    <li> In <b>.....</b>, we .. </li>
    <li> Finally, in <b>modeling_insights.ipynb</b>, we </li>
   </ol>
  <li> The directory <code>./data</code> contains 1) the dataframe as collected from the NSRDB, and 2) the cleaned, feature engineered dataframe that is used for the various models.
   <li> The directory <code>./figures</code> contains all the figures that are saved during the analysis in the notebooks, in .png formats </li>
    <li> The slides for the project presentation are in the file <code>project4_solar.pdf</code> </li>
</ul>

## Background

As the world is slowly transitioning away from fossil fuels, the issue of how to integrate renewable sources energy into the power grid has become more and more relevant. Energy sources like wind and solar energy can vary on timescales of hours or even shorter, and thus a combination of increased energy storage and careful forecasting is becoming necessary in order to ensure that energy supply can meet demand. Reliably forecasting how much solar energy can be extracted in a given location can thus be a very valuable undertaking.

In this project, we will use the 'Global Horizontal Irradiance' (or GHI) as a proxy to model how much solar power can be generated in a given area. The GHI is a measurement of how much energy is received by a surface horizontal to the ground (for an overview, see eg. <a href=https://www.sciencedirect.com/topics/engineering/global-horizontal-irradiance>here</a>). This quantity in particular correlates well with how much energy can be extracted by photovoltaic systems, and is thus of particular interest.

For this project, we use data from the <a href=https://nsrdb.nrel.gov/>National Solar Radiation Database</a>, or NSRDB. The NSRDB is a freely available database that has weather data available at a 2x2km resolution at half-hour intervals. The data is collected from various satellites (more information <a href=https://nsrdb.nrel.gov/data-sets/us-data>here</a>). The collected weather data is then used to model solar irradiance parameters, such as the GHI and the DNI (Direct Normal Irradiance). 

In this project, we have used the NSRDB data in two different ways: Firstly, the GHI itself can be analysed as a time series, and used to forecast the GHI into the future. Although this is the easiest from a modeling perspective, it does require a GHI model, which may not always be available. The second approach is to use the time series of weather data to forecast GHI into the future. This approach is slightly more complex from a modeling perspective, but does mean that the GHI could be forecast with more 'fundamental' weather data. 

## Data Dictionary


|Feature|Type|Dataset|Description|
|---|---|---|---|
|Dew Point| Numerical |NSDRB | Defined as 'the temperature to which air must be cooled to become saturated with water vapor', in degrees Celsius |
|Pressure| Numerical |NSDRB | Air pressure in Millibar | 
|Relative Humidity| Numerical |NSDRB |Percentage of water vapor in the air |
|Temperature| Numerical |NSDRB | Air temperature in degrees Celsius | 
|Wind_x| Numerical | NSDRB | X-component of wind velocity. Feature engineered from Wind direction and speed|
|Wind_y| Numerical | NSDRB | y-component of wind velocity. Feature engineered from Wind direction and speed|
|Day Seasonality | Numerical | NSDRB | Sinoid function that captures daily variance in the GHI. Feature engineered |
|Year Seasonality | Numerical | NSDRB | Sinoid function that captures yearly variance in the GHI. Feature engineered |
|Cloud Type | Categorical | NSDRB | Categorical variable indicating type of cloud. See notebook for more details |
|GHI| numerical| NSDRB| ***Target variable***- Global Horizontal Irradiance in W/m2|


## Data Collection and EDA

To collect the data, we used the api available from the NSRDB to directly read to a csv using a url format. To run the data collection notebook, one needs an api token from the NSRDB that can be obtained [here](https://developer.nrel.gov/signup/).

We collected data from 2016 to the most recent available year of 2020, which resulted in a 5 year time period of 30 minute intervals. This data included sensor collected weather features, sensor collected Solar Iridiance values, such as DHI and DNI, and model predict GHI values from NSRDB algorithms.  


## Modeling

We decided to forecast out target variable, GHI, using 3 different models:

_RNN model_
- In this model

_WaveNet model_
- In our analysis, we used a modifidied version of the model described in this [paper](https://arxiv.org/pdf/1609.03499.pdf). The model described in the model is used as a generative model for audio signals.The main feature of the model is the use of _dilated_ convolutional layers for sequencing, as opposed to the conventional recurrent layers. We decided to use this model because it would be well suited for predictions of large sequences, which in our case would be a large amount of time steps. 
- Our approach had a couple changes to the model:
    - First, instead of a _sigmoid_ activation in the Gated Activation Layers, we used a _relu_ activation because this [paper](https://arxiv.org/pdf/1703.04691.pdf) on dilated convolutions suggests it is a more suited activation to a non-stationary time-series, which GHI is because of it's seasonality.
    - Secondly, a linear dense layer was used as the output to create predictions for each time step in the future according to the number of output neurons. 


## Insights

## Conclusions

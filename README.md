# wheat-price-prediction
## Introduction & Background ##
Food insecurity is a multi-fauceted and large issue in India, with at least an estimated 200 million people suffering from malnourishment and a lack of access to food. Weather events impacting scarcity of food, issues with bureaucracy and supply, along with ongoing world events can all impact how food-secure the population of India is at any given moment. In addition, predicting food securiy among regions is highly difficult as well because of the difficulty in collecting data in rural populations. This leaves the severity of food security in India highly contested, with huge ranges in estimates across multiple studies. A study from McKay, Sims, and Pligt find that food insecurity measures between the National Sample Survey (NSS), Food Insecurity Experience Scale (FIES), Comprehensive National Nutritution Survey (CNNS), or Household Food Insecurity Access Scale (HFIAS) were used in food security studies, and find variances from 32% of the population being insecure to 77.9%. In other populations less documented like children living in slums, food insecurity rate was found to be between 12% and 77%. The massive unpredictability in the data show that determining a true rate of food security in India is difficult. 

Some more quantitative solutions to predicting food security focus on modeling rare weather events, or drought probabiity to emphasize the importance of food (and more specifically, grain/plant) availability. The availability of data on Indian wheat supply, specifically Food Corporation of India (FCI) public data regarding the quantity of grains in storage also allows for the possibility of modeling the various factors influencing India's wheat supply. Following a similar line of thought, we can model food availability but in a different way, using food prices. Prices should reflect not only the supply of food produced, but also the economy and how affordable that food is. In particular, grain prices like wheat would be an ideal candidate, because they make up most of the Indian diet. 

Furthermore, forecasting the price of grains would be hugely beneficial in understanding which regions of India are most affected by outside events. Having an estimate of price increases after a season of drought can help us understand how fragile the food economy is for each region. This can be an important factor in determining food security as a whole in India.


## Methods ##

To reflect this principle, we can build a time series forecasting model to predict the price of wheat. We do so using data from an Indian market, providing daily prices on various wheat varieties, markets, and regions.

For this example, we focus on Etawah market in Uttar Pradesh, one of the most food insecure states in India. 

A LSTM and ARIMA model is trained to conduct time series forecasting on the modal price of wheat, with better results from the LSTM in accuracy. Training was done on a free Google Colab T4 GPU, later moved to a Nautilus Cluster with 2x RTX 3090 GPUs after Colab resources were exhausted. 

## Results ##
The price of wheat is represented in RS/quintal, where RS is an Indian rupee and quintal is 100kg. After cleaning the data and using linear interpolation to fill in missing days, a visualization of ~6600 daily price data shows a general trend of increase in price since 2005.


![image](https://github.com/anngo-1/wheat-pricing-prediction/assets/75955073/0fa7589d-72b5-4adf-9d63-826ddc899589)


Preliminary results of training a model consisting of a simple single layer LSTM show promise in predicting wheat prices. Mean squared error is high due to the model being trained to predict high time steps, which may disappear after adding more LSTM layers to the model, increasing model complexity.

Results in an ARIMA forecast are highly inaccurate because the data is not stationary. Differencing transformations remove much of the data's granularity. 

<p float="left">
  <img src="https://github.com/anngo-1/wheat-pricing-prediction/assets/75955073/f4d5dd14-df81-4b96-b490-8012f7278f8b" width="400" />
  <img src="https://github.com/anngo-1/wheat-pricing-prediction/assets/75955073/8f78496e-3e55-4f07-97b0-15bab0ab267f" width="385" />
</p>

<br>
<br>
Using the LSTM, we can predict wheat prices in the future. We predict the wheat price for the next 80 days:
<br>
<br>
<img src="https://github.com/anngo-1/wheat-pricing-prediction/assets/75955073/fecad770-5675-4858-b602-81d33eddafa1" width="900">

## Conclusion ##
Forecasting could be highly effective in understanding more about food insecurity. Highly accurate forecasts of 10-30 days could assist local govenments in understanding how weather events affect food availability through the lens of the consumer. Grains like wheat, which make up most of the Indian diet, would be great targets for forecasting.

## Note ##
Price data is sourced from [agmarknet.gov.in](https://agmarknet.gov.in/). To run the forecasting notebooks in this repository, download the file in the data directory and make sure it is presnet in the notebook directory. Alternatively, download your own raw data file from the link provided and clean it using clean.ipynb. 


## Sources ##
McKay, Fiona H., Alice Sims, and Paige van der Pligt. "Measuring Food Insecurity in India: A Systematic Review of the Current Evidence." Current Nutrition Reports 12.2 (2023): 358-367.

Brahmanand, P. S., et al. "Challenges to food security in India." Current Science (2013): 841-846.

Birthal, Pratap S., et al. "Impact of climate change on yields of major food crops in India: Implications for food security." Agricultural Economics Research Review 27.2 (2014): 145-155.

Headey, Derek D., and William J. Martin. "The impact of food prices on poverty and food security." Annual review of resource economics 8 (2016): 329-351.

Das, Bhabani S., et al. "Soil health and its relationship with food security and human health to meet the sustainable development goals in India." Soil Security (2022): 100071.


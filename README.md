# Analyzing Nepalese Produce Time-Series Data for Seasonality and Forecasting

## About the Dataset

  FROM KAGGLE: "This dataset contains official price information for major vegetables and fruits in Nepal from 2013 to 2021. The dataset includes daily price data for each vegetable and fruit, as well as the maximum, minimum, and average prices over the period. The prices are based on official figures and provide a valuable resource for anyone interested in analyzing the prices of agricultural commodities in Nepal."
  
  LINK: https://www.kaggle.com/datasets/ramkrijal/agriculture-vegetables-fruits-time-series-prices

## Data Analysis for Pricing Seasonality  

I first ran some SQL queries to get a basic understanding of the dataset. I then wrote more complex queries to derive three tables: one with general information on each item; one that identified each item's peak and low months and seasons; and one that calculated a seasonal variability factor (SVF) that quantified how much each item's price tended to vary bewtween peak and low months. Using these tables and the original dataset, I created a dashboard in Tableau that shows individual items' change in price over time, average price during various months, and more seasonal pricing information. You can find the dashboard here: https://public.tableau.com/app/profile/aj.arbuckle/viz/NepaleseProducePrices2/Dashboard1

## Forecasting 

I then set out to create forecasting models to predict future prices for 5 select items using XGBoost. I decided to use XGBoost for its high predictive accuracy; its feature importance scores; its ability to handle missing data; and its ability to capture non-linear patterns I expected to see in the data. I selected items based on a few criteria. First, the item had to have data spanning at least 4 years. This was because my plan was to predict prices for at least 1 year, and since I expected pricing trends of produce to vary by time of year, I wanted to have at least 3 full years of data to train the model with. Second, the item had to have data for at least 75% of all the days between its first and last recording dates. Of the remaining items, I chose the 5 with the highest SVF, as I expected these items to have the most clearly seasonal pricing patterns. I selected the items using the Python script in the main directory, and built the models in the scripts in the 'Models' folder. 

Overall, the models were only slightly better than a comparison model that was based solely on the averages for each month from the training data, being on average nearly 5% more accurate. This makes sense given that produce prices vary based on the time of year, and a month feature captures much of that variation. However, the models were able to predict slightly better, meaning that the other features (day of year, year, and day of week) contributed slightly to their accuracy. 


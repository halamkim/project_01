# Currency Pair Portfolio Strategy

This project uses two different methods to optimize the currency pair portfolio. One method is using the Simple Moving Average (SMA) strategy to trade whenever the slow SMA crosses the fast SMA to maximize the returns, with the purpose of determining possible returns for each pair and contrasting them with the general market (S&P 500) as a reference point.Additionally, we find the correlation between bond interest rate and the past currency pair prices to apply the correlation into our portfolio. We will examine the top 7 currency pairs: AUD/USD, EUR/CHF, EUR/JPY, EUR/USD, USD/CAD, USD/CHF, USD/JPY.

## Requirements
- python 3.7 or higher
- import required libraries
```
import pandas as pd
from pathlib import Path
from dotenv import load_dotenv
import alpaca_trade_api as tradeapi
import os
import requests
import numpy as np
%matplotlib inline
import hvplot.pandas
from sklearn.linear_model import LinearRegression
```

## 1. Currency Pair Analysis
- Concatenate each data using **pd.concat()** for all the closing prices
![This shows the first 10 rows of the concatenated dataframe of all currency pairs' closing prices](https://raw.githubusercontent.com/halamkim/project_01/7d414de71125870bb1ccfc9171c90ab3e9cd9fb3/Halam%20Kim/Screen%20Shot%202023-01-27%20at%207.31.04%20PM.png)
- In order to find the order of conservative to risky pairs, you calculate standard deviation and variance by first finding the percent change (**pct_change()**) and then using the **std()** and **var()** methods. 
```
pct_change = df.pct_change().dropna()
std = pct_change.std()
var = pct_change.var()
```
## 2. Applying SMA Trading Strategy
Our trading strategy is to trade when the fast SMA graph crosses the slow SMA graph to target the best opportunities to maximize the returns.
We used:
```
fast_sma = 10
slow_sma = 20
```
1. Using the rolling + mean() methods, create two new columns called "fast_sma" and "slow_sma."
2. Apply pct_change()
3. Apply cumprod()
4. Add a 'long/short' column that shows when to buy or sell the currency pair. This point is where the fast and slow SMA lines cross.
5. Plot cumulative returns! 

![Graph of all currency pairs' cumulative returns](https://raw.githubusercontent.com/halamkim/project_01/Halam-Kim/Screen%20Shot%202023-01-30%20at%208.47.36%20PM.png)

## 3. Forecasting with Linear Regression

Using the Linear Regression method for forecasting was unsuccessful and can be used for future projects.


The following library is a useful tool for back-testing models, but we did not get to the point of splitting data for back-testing. To use it, add the following code to your project:


```
from sklearn.model_selection import train_test_split
```

**Applying the Linear Regression method**

1. Import the data and plot it specifically for the AUD/USD currency pair.
2. Find the `x` variable by creating a numpy array of the 'HIGH', 'LOW', 'OPEN', and 'CLOSE' values from the AUD/USD data. `x` is the previous close price that we selected to forecast the target close `y`.
3. Find the `y` variable by creating a numpy array for the shifted AUD/USD data (by 1 day). `y` is the actual target (or close price) that we will predict using `x`.
4. Fit the linear regression model by creating a variable `model` equal to the linear regression function:
```
model = LinearRegression()
model.fit(x, y)
```

5. Calculate the coefficient of determination (R^2 value), the intercept (b0), and the slope (b1) using the following code:

```
r_sq = model.score(x, y)
print(f"coefficient of determination: {r_sq}")
print(f"intercept: {model.intercept_}")
print(f"slope: {model.coef_}")
```

6. Use the linear regression formula `f(x) = b0 + b1x` to predict values


**CONCLUSION**: Considering the result of the R^2 (0.99) and confirming results after analyzing both plots, the linear regression method shifted by one day (aiming to forecast the next day) is not an effective method to project price-action. This model is over-fitted and basically replicated previous information. Therefore, another method might be required to predict the trend or price-action in certain timeframes for the currency pairs.


## 4. Comparing Currency Pair with Bond Interest Rates

This analysis aims to study the impact of 10-year bond interest rates for the USD and EUR on the Forex market for relevant currency pairs. The analysis will start by importing and plotting the data for the 10-year bond price of the USD using hvplot.

We will then plot the USD-based currency pairs (AUD/USD, USD/CAD, USD/CHF, USD/JPY) against the 10-year bond rates to determine the relationship between interest rates and currency prices. The principle being tested is that if interest rates increase, the price of the currency should increase, and vice versa.

Similarly, the EUR-based currency pairs will be plotted against the respective 10-year bond rates, and we will also analyze the EUR/USD pair with both 10-year bonds. The results of this analysis will provide insights into the correlation between interest rates and currency prices.

It is important to note that while the visual analysis may suggest a correlation, there are multiple variables affecting currency prices, and a detailed correlation analysis between 10-year bond and currency pair prices would be useful for price-action forecasting.
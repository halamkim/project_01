# Currency Pair Portfolio Strategy

This project uses two different methods to optimize the currency pair portfolio. One method is using the Simple Moving Average (SMA) strategy to trade whenever the slow SMA crosses the fast SMA to maximize the returns, with the purpose of determining possible returns for each pair and contrasting them with the general market (S&P 500) as a reference point.Additionally, we find the correlation between interest rate and the past currency pair prices to apply the correlation into our portfolio. We will examine the top 7 currency pairs: AUD/USD, EUR/CHF, EUR/JPY, EUR/USD, USD/CAD, USD/CHF, USD/JPY.

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
```

## Currency Pair Analysis
- Concatenate each data using **pd.concat()** for all the closing prices
![This shows the first 10 rows of the concatenated dataframe of all currency pairs' closing prices](https://raw.githubusercontent.com/halamkim/project_01/7d414de71125870bb1ccfc9171c90ab3e9cd9fb3/Halam%20Kim/Screen%20Shot%202023-01-27%20at%207.31.04%20PM.png)
- In order to find the order of conservative to risky pairs, you calculate standard deviation and variance by first finding the percent change (**pct_change()**) and then using the **std()** and **var()** methods. 
```
pct_change = df.pct_change().dropna()
std = pct_change.std()
var = pct_change.var()
```
## SMA Trading Strategy
Our trading strategy is to trade when the fast SMA graph crosses the slow SMA graph to target the best opportunities to maximize the returns.
We used:
```
fast_sma = 7
slow_sma = 21
```
1. Using the rolling + mean() methods, create two new columns called "fast_sma" and "slow_sma."
2. Apply pct_change()
3. Apply cumprod()
4. Add a 'long/short' column that shows when to buy or sell the currency pair. This point is where the fast and slow SMA lines cross.
5. Plot cumulative returns! 

![Graph of all currency pairs' cumulative returns](https://raw.githubusercontent.com/halamkim/project_01/Halam-Kim/Screen%20Shot%202023-01-30%20at%208.47.36%20PM.png)




## Authors
- Mike Blanchette
- Soheil Gityforoze
- Halam Kim
- Francisco Franco Mesa




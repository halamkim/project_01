# Currency Pair SMA Strategy

This project uses the Simple Moving Average (SMA) method to examine the top 7 currency pairs, with the purpose of determining possible returns for each pair and contrasting them with the general market (S&P 500) as a reference point.

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
- Concatenate each data using pd.concat() for all the closing prices
![This shows a picture of the concatenated dataframe of all currency pairs' closing prices](https://raw.githubusercontent.com/halamkim/project_01/7d414de71125870bb1ccfc9171c90ab3e9cd9fb3/Halam%20Kim/Screen%20Shot%202023-01-27%20at%207.31.04%20PM.png)
- In order to find the order of conservative to risky pairs, you calculate standard deviation and variance by first finding the daily returns (**pct_change()**) and then using the **std()** and **var()** methods. 


## Authors
- Mike Blanchette
- Soheil Gityforoze
- Halam Kim
- Francisco Franco Mesa




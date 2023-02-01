# FOREX SMA strategy and analysis

This project uses the SMA (Small Moving Average) trading method to optimize the currency pair portfolio. This method is designed to trade whenever the slow SMA crosses the fast SMA to maximize the returns. The purpose is to determine possible returns for each pair and compare them with the general market (S&P 500) and a general index fund (Vanguard Index Fund) as a reference point. Additionally, we find the correlation between bond interest rate and the past currency pair prices to find the pattern and have it be a factor in our portfolio managing. We will examine the top 7 currency pairs: AUD/USD, EUR/CHF, EUR/JPY, EUR/USD, USD/CAD, USD/CHF, USD/JPY.

## Requirements
- python 3.7 or higher
- import required libraries
```
import pandas as pd
from pathlib import Path
import numpy as np
%matplotlib inline
import hvplot.pandas
from sklearn.linear_model import LinearRegression
import yfinance as yf
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
fast_sma = 50
slow_sma = 100
```
1. Using the rolling + mean() methods, create two new columns called "fast_sma" and "slow_sma."
2. Apply pct_change()
3. Apply cumprod()
4. Add a 'long/short' column that shows when to buy or sell the currency pair. This point is where the fast and slow SMA lines cross.
5. Plot cumulative returns! 

![Graph of all currency pairs' cumulative returns](https://raw.githubusercontent.com/halamkim/project_01/main/Screenshot%202023-01-31%20231837.png)

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

## 5. Performance Analysis
The data was obtained using the *yfinance* for the S&P 500 and and the VBTLX (Vanguard Index Fund) and manual upload for the EURJPY currency pair. The cumulative returns were calculated and plotted to visualize the performance over the 10-year period.

**Coding Order**
1. Retrieve the daily close prices of S&P 500 and VBTLX from 2010 to 2020 from yfinance.
2. Calculate the daily return of each index, drop the first row as it contains `NaN`, and add it to a new column named `strat_return`.
3. Calculate the cumulative return of each security by multiplying the cumulative value of the `strat_return` column.
4. Convert the date-time index of each data frame to date format.
5. Plot the cumulative return of each asset class and label them accordingly.
6. Create a plot displaying cumulative annual returns of the EURJPY to visually compare the performance with the \cf2 S&P 500 and VBTLX.

**Results**

The plots below show the cumulative return of each asset class from 2010 to 2020. We can see that the S&P 500 has performed relatively better than the other 2 asset classes. In contrast, the EURJPY has performed relatively better than the VBTLX. In simple terms, for every one dollar invested in S&P 500 in 2010, the investors could have expected to receive more than three dollars in return which is higher than the return if invested in the other two assets classes.

![This plot shows the cumulative return of the S&P 500 (red line) and VBTLX (blue line) from 2010 to 2020.](https://raw.githubusercontent.com/halamkim/project_01/main/Cumulative%20Return%20of%20SP500%20and%20VBTLX.png)
![This plot shows the cumulative return of the EURJPY from 2010 to 2020.](https://raw.githubusercontent.com/halamkim/project_01/main/Annual%20Return%20of%20EURJPY.png)
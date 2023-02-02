# Portfolio Performance Analysis

## Overview
This project compares the performance of the S&P 500, the VBTLX (Vanguard Bond Index Fund), and the EURJPY currency pair from 2010 to 2020. The data was obtained using the yfinance for the S&P 500 and and the VBTLX and manual upload for the EURJPY currency pair. The cumulative returns were calculated and plotted to visualize the performance over the 10-year period.



## Installations
- pandas
- yfinance
- matplotlib

## Coding Order
1. Import the required packages including pandas, yfinance, and matplotlib.
2. Retrieve the daily close prices of S&P 500 and VBTLX from 2010 to 2020 from yfinance.
3. Calculate the daily return of each index, drop the first row as it contains `NaN`, and add it to a new column named `strat_return`.
4. Calculate the cumulative return of each security by multiplying the cumulative value of the `strat_return` column.
5. Convert the date-time index of each data frame to date format.
6. Plot the cumulative return of each asset class and label them accordingly.
7. Create a plot displaying cumulative annual returns of the EURJPY to visually compare the performance with the S&P 500 and VBTLX.

## Results
The plot shows the cumulative return of each asset class from 2010 to 2020. From the plots, we can see that the S&P 500 has performed relatively better than the other 2 asset classes. In contrast, the EURJPY has performed relatively better than the VBTLX. In simple terms, for every one dollar invested in S&P 500 in 2010, the investors could have expected to receive more than three dollars in return which is higher than the return if invested in the other two assets classes.


## Conclusion
The plot helps to compare the performance of each stock in terms of cumulative return and how they performed over the years.







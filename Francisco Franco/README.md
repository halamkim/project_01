# project_01
# Project for Group 2 (Halam Kim, Francisco Franco Mesa, Mike Blanchette, Soheil Gityforoze)

Begin by importing the libraries
import pandas as pd
from pathlib import Path
%matplotlib inline
import hvplot.pandas

import numpy as np
from sklearn.linear_model import LinearRegression

The following library is a good tool to use when back-testing models but we did not get to the point of splitting data to back test.
from sklearn.model_selection import train_test_split


Start by importing the data and plotting specifically for the AUD/USD currency pair. After having that done, start implementing the steps to apply the linear regression method using AUD/USD data to forecast future closing price of the currency pair:
1. Find the "x" varibale by creating a numpy array of the 'HIGH', 'LOW', 'OPEN', 'CLOSE' from AUD/USD data. The "x" is the previous close (feature) we elected to forecast the target close "y". It will basically be used as previous day data to predict "y".
2. Find the "y" varibale by creating a numpy array for the AUDUSD shifted data (by 1 day). "y" is the actual target (or close - figured out with "x")
3. Fit the linear regression model by using creating a variable called model equal to the linear regression function:
    model = LinearRegression()

    Then calculate optimal values of wieghts for b0 and b1 by fitting the model by running the following code: 
    model.fit(x, y)

    In order for the model to fit you should get tthe following result after runing the previous code:
    LinearRegression()
    
4. Find the R^2 value (coefficient of determination) - Determines variation in y explained by dependance on x in a regression model.
    Larger R^2 determines a better fit which indicates that the model can explain the change in outputs with it's different inputs.
 
    R^2 = 1 indicates the perfect fit

    r_sq = model.score(x, y)
    print(f"coefficient of determination: {r_sq}")

    Finding the intercept b0
    print(f"intercept: {model.intercept_}")

    Finding the slope b1
    print(f"slope: {model.coef_}")
    
5. # Utilizing the linear regression formula 𝑓(𝑥) = 𝑏₀ + 𝑏₁𝑥 to predict values for 𝑓(𝑥). Then print the prediction for y:
    y_pred = model.intercept_ + model.coef_ * x
    print(f"predicted response:\n{y_pred}")
    
6. Plot both original and projected close price graphs for AUD/USD to determine how did the model affect price-action of the currency pair. 

CONCLUSION: Considering the result of the R^2 (0.99) and confirming results after analyzing both plots, the linear regression method shifted by one day (aiming to forecast the next day) is not an effective method to project price-action. This model is over-fitted and basically replicated previous information. Therefore, another method might be required to predict the trend or price-action in certain timeframes for the currency pairs.

Therefore, we will analyze the impact that 10-year bond interest rates for both the USD and EUR have in the Forex market for these currencies. 

We will begin by importing the data for the 10-year bond price of the USD. Then, we will plot the data in a hvplot to dynamically see how the rates have been changing from 2000 to 2018.

Once we have an idea of the overall price-action, we will plot it seperately with each currency pair that contains USD as one of the currencies in each pair (at the end we will plot all currencies with the 10-year bond as well). This will serve to review how did changes in interest rates for the USD affected price-action of the currency pair. Also, we would be considering the following macroeconomic principle:

If interest rate raises, the price of the currency should increase due to supply shortage. When governments increase rates, it means that there would be less circulating supply of that currency pair; therefore, the currency's price should increase if no other variables are considered and demand stays constant. Basically people would start giving money back to the government to capture those higher interest rates, investing in bonds or "high" yielding savings accounts. On the contrary, if a government decides to lower rates, it means there would be more circulating supply of that currency. As a consequence, the price of that currency would go down considering no other variables and a constant demand.

This would let us review if the previously mentioned principle applies and if it does, in which degree for every currency pair. 

After plotting AUD/USD, USD/CAD, USD/CHF, USD/JPY against the 10-year bond rates, we can determine that the principle is visible at certain degree depending on the currency pair you're analyzing and the timeframe in consideration. Specially for the USD/CHF you can see a direct correlation and strong relationship in rates and currency pair prices. As interest rates decrease --> USD/CHF price also decreases.

We will apply the same exercise for the pairs containing the euro (EUR) and compare them with it's respective 10-year bond. Surprisingly, we have a similar result on the EUR/CHF, whose price-action continously decreases as rates decrease.


Finally, we will analyze the EUR/USD wihth both 10-year bonds for the euro and the US Dollar. Now we are considering both currencies rates fluctuation... As a intriguing fator, most of the time that EUR rates are above USD rates, price-action of the pair tends to be bullish, whether as in the opposite rate scenario price-action tends to be bearish (for most of the time). Specially when seeing what happened after 2014, when Euro rates sunk under USD rates (as USD rates increased) and EUR/USD price-action took a overall bearish condition to the downside.

It is important to know that visually we can consider the fact that rates are correlated to currencies price-action but we also need to have in mind that there are many other variables affecting the currency price. Nevertheless, it would be very interesting dialing in a detailed correlation analysis between 10-year bond and currency pairs prices. That would be significantly helpful to forecast price-action once governments decide to increase or decrease interest rates for their national currency. 
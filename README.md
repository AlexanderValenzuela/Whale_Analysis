# Project Title - Algo Investment Trading Platform
This project aims to build a FinTech investment platform that leverages algorithmic trading and offers customers a one-stop investment solution for their retirement portfolios.


## Technologies
**Python Libraries**
```python
from pathlib import Path
import pandas as pd
import numpy as np
%matplotlib inline
```

## Installation Guide
`pip install pandas`


Provide the instructions for installing any project dependencies.


## Usage

I. Importing the Data
>*About the data?*<br>
The CSV file contains net asset values (NAV) of four portfolio funds: [Soros Fund Management LLC](https://en.wikipedia.org/wiki/Soros_Fund_Management), [Paulson & Co Inc](https://en.wikipedia.org/wiki/Paulson_%26_Co.), [Tiger Global Management LLC](https://en.wikipedia.org/wiki/Tiger_Global_Management) and [Berkshire Hathaway Inc](https://en.wikipedia.org/wiki/Berkshire_Hathaway).  Also included is the [S&P 500 index](https://www.spglobal.com/spdji/en/indices/equity/sp-500/#overview), which will serve as the standard for analyzing the four portfolio funds.  

Use the `read_csv` function and the `Path module` to read the whale_navs.csv file into a Pandas DataFrame.<br>
Use the `head` function to examine the first five rows of the DataFrame.<br>
![Screenshot 2023-04-15 at 1 38 07 AM](https://user-images.githubusercontent.com/111409358/232201189-97f7cbab-4491-4cb7-9d9c-76addb62c02f.png)

Use the Pandas `pct_change` and the `dropna` functions to create the daily returns DataFrame.<br>
![Screenshot 2023-04-15 at 2 38 26 AM](https://user-images.githubusercontent.com/111409358/232206080-f51e43cb-3886-4a76-a583-5adf68b78e51.png)


II. Quantitative Analysis

>1. Analyze the Performance<br>
Analyze the data to determine if any of the portfolios outperform the broader stock market, which the S&P 500 represents.

Step 1 - Use the `plot` function to visualize the daily return of the four fund portfolios & the S&P 500.
```python
daily_returns_df.plot(figsize=(15,10),title="Daily Return of the Four Fund Portfolios & the S&P 500")
```
Step 2 - Use the `cumprod` function to calculate the cumulative returns for the four fund portfolios and the S&P 500.  Use the `tail` function to review the last five rows of the cumulative returns DataFrame.
```python
cumulative_returns = (1 + daily_returns_df).cumprod()
cumulative_returns.head()
```
Step 3 - Use the `plot` function to visualize the cumulative return values of the S&P 500 over time.
```python
cumulative_returns.plot(figsize=(20,15), title="Cumulative Returns of the Four Fund Portfolios vs S&P 500")
```

>2. Analyze the Volatility<br>
Analyze the volatility of each of the four fund portfolios and of the S&P 500 Index by using box plots.

Step 1 - Use the `plot` function and the 'kind="box"` parameter to visualize the daily return data for each of the four portfolios and the S&P 500 in a box plot.
```python
daily_returns_df.plot(kind="box",figsize=(20,15), title="Daily Returns of the Four Fund Portfolios vs S&P 500")
```
Step 2 - Create a new DataFrame and then use the `drop` function to drop the S&P 500 column. Use the `plot` function and the `kind="box"` parameter on the new DataFrame to display the daily returns of the four fund portfolios in a box plot.
```python
portfolio_funds_df = daily_returns_df.drop(['S&P 500'], axis=1)
portfolio_funds_df.plot(kind="box",figsize=(20,15), title="Daily Returns of Four Portfolio Portfolios")
```

>3. Analyze the Risk<br>
Analyze the data to determine if any of the portfolios outperform the broader stock market, which the S&P 500 represents.

Step 1 - Use the `std` function to calculate the standard deviation for each of the four portfolios and the S&P 500.  Use the `sort_values` funciton to sort from smallest to largest.
```python
standard_deviation = daily_returns_df.std()
standard_deviation_sorted = standard_deviation.sort_values()
standard_deviation_sorted
```
Step 2 - Calculate the annualized standard deviation for each of the four portfolios and the S&P 500.  Multiply the standard deviation by the square root of the number of trading days, '252'.
```python
annual_standard_deviation = standard_deviation * np.sqrt(252)
annual_standard_deviation_sorted = annual_standard_deviation.sort_values()
annual_standard_deviation_sorted
```
Step 3 - Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of the four fund portfolios and the S&P 500 index.
```python
daily_returns_df.rolling(window=21).std().plot(figsize=(15,10),title="Four Fund Portfoliods vs S&P 500 - 21-Day Rolling Standard Deviation")
```
Step 4 - Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of only the four fund portfolios. 
```python
portfolio_funds_df.rolling(window=21).std().plot(figsize=(15,10), title="Four Fund Portfolios - 21-Day Rolling Standard Deviation")
```

>4. Analyze the Risk-Return Profile<br>
To determine the overall risk of an asset or portfolio, quantitative analysts and investment managers consider not only its risk metrics but also its risk-return profile. After all, if you have two portfolios that each offer a 10% return but one has less risk, you’d probably invest in the smaller-risk portfolio. For this reason, you need to consider the Sharpe ratios for each portfolio.<br>

Step 1 - Use the daily return DataFrame to calculate the annualized average return data for the four fund portfolios and the S&P 500 index.  Use 252 for the number of tradingf days.  Review the annualized average returns, sorted from lowest to highest.
```python
average_annual_return = daily_returns_df.mean() * 252
average_annual_return_sorted = average_annual_return.sort_values()
average_annual_return_sorted
```
Step 2 - Calculate the Sharpe ratios of the four fund portfolios and for the S&P 500.  Divide the annualized average return by the annualized standard deviation for each.  Review the resulting Sharpe ratios, sorted from lowest to highest.
```python
annualized_sharpe_ratios = average_annual_return / annual_standard_deviation
annualized_sharpe_ratios_sorted = annualized_sharpe_ratios.sort_values()
annualized_sharpe_ratios_sorted
```
Step 3 - Visualize the Sharpe ratios for the four funds and for the S&P 500 in a bar chart. 
```python
annualized_sharpe_ratios.plot.bar(figsize=(10,7),title="Four Portfolio Funds vs S&P 500 - Sharpe Ratios")
```

>5. Diversify the Portfolio<br>
Evaluate how the portfolios react relative to the broader market. Based on my analysis so far, I chose two portfolios that I recommend as investment options.













## Contributors
Alexander Valenzuela<br>
[LinkedIn Profile](<https://www.linkedin.com/in/alex-valenzuela-97826842/>)


## License
The Unlicense




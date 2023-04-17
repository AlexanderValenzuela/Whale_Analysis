# Project Title - Algo Investment Trading Platform
This project aims to build a FinTech investment platform that leverages algorithmic trading and offers customers a one-stop investment solution for their retirement portfolios.


## Technologies
**Python Pandas Libraries**
```python
from pathlib import Path
import pandas as pd
import numpy as np
%matplotlib inline
```

## Installation Guide
[Anaconda](https://docs.continuum.io/anaconda/install/)<br>
[Jupyter Labs Docs](https://jupyterlab.readthedocs.io/en/stable/getting_started/starting.html)<br>
`pip install jupyterlab`<br>
[Jupyter Notebook Docs](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html)<br>
`pip install notebook`<br>

## Usage

I. Importing the Data
>*Getting to Know the Data*<br>
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
![Screenshot 2023-04-16 at 7 19 46 PM](https://user-images.githubusercontent.com/111409358/232364555-7c382dc4-594c-4bdd-b984-21a066836903.png)

Step 2 - Use the `cumprod` function to calculate the cumulative returns for the four fund portfolios and the S&P 500.  Use the `tail` function to review the last five rows of the cumulative returns DataFrame.
```python
cumulative_returns = (1 + daily_returns_df).cumprod()
cumulative_returns.head()
```
Step 3 - Use the `plot` function to visualize the cumulative return values of the S&P 500 over time.
```python
cumulative_returns.plot(figsize=(20,15), title="Cumulative Returns of the Four Fund Portfolios vs S&P 500")
```
![Screenshot 2023-04-16 at 7 21 17 PM](https://user-images.githubusercontent.com/111409358/232364724-623874ef-fb82-429f-9b92-bbbcb68121e1.png)

>2. Analyze the Volatility<br>
Analyze the volatility of each of the four fund portfolios and of the S&P 500 Index by using box plots.

Step 1 - Use the `plot` function and the 'kind="box"` parameter to visualize the daily return data for each of the four portfolios and the S&P 500 in a box plot.
```python
daily_returns_df.plot(kind="box",figsize=(20,15), title="Daily Returns of the Four Fund Portfolios vs S&P 500")
```
![Screenshot 2023-04-16 at 7 40 19 PM](https://user-images.githubusercontent.com/111409358/232365052-7ce9a11c-b88c-4781-8a53-0a1ae11256eb.png)

Step 2 - Create a new DataFrame and then use the `drop` function to drop the S&P 500 column. Use the `plot` function and the `kind="box"` parameter on the new DataFrame to display the daily returns of the four fund portfolios in a box plot.
```python
portfolio_funds_df = daily_returns_df.drop(['S&P 500'], axis=1)
portfolio_funds_df.plot(kind="box",figsize=(20,15), title="Daily Returns of Four Portfolio Portfolios")
```
![Screenshot 2023-04-16 at 7 22 32 PM](https://user-images.githubusercontent.com/111409358/232365119-0f7f6df6-718a-4ed5-844e-8b6fc6a21da7.png)

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
![Screenshot 2023-04-16 at 7 24 34 PM](https://user-images.githubusercontent.com/111409358/232364217-c8736cf2-d00a-4070-885e-e6b2e068787c.png)

Step 4 - Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of only the four fund portfolios. 
```python
portfolio_funds_df.rolling(window=21).std().plot(figsize=(15,10), title="Four Fund Portfolios - 21-Day Rolling Standard Deviation")
```
![Screenshot 2023-04-16 at 7 44 07 PM](https://user-images.githubusercontent.com/111409358/232365504-3d6a3d74-11ed-4b85-aa76-2eac10172a8a.png)

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
![Screenshot 2023-04-16 at 7 30 44 PM](https://user-images.githubusercontent.com/111409358/232364054-59b8ba71-63d6-4003-b2dc-81fb1542a50e.png)

>5. Diversify the Portfolio<br>
Evaluate how the portfolios react relative to the broader market. Based on my analysis so far, I chose two portfolios that I recommend as investment options.

Portfolio 1<br>

Step 1: Using the 60-day rolling window, the daily return data, and the S&P 500 returns, calculate the covariance. Review the last five rows of the covariance of the portfolio.
```python
tiger_rolling_60_covariance = daily_returns_df['TIGER GLOBAL MANAGEMENT LLC'].rolling(window=60).cov(daily_returns_df['S&P 500'])
tiger_rolling_60_covariance.tail()
```
Step 2: Calculate the beta of the portfolio. To do that, divide the covariance of the portfolio by the variance of the S&P 500.
```python
tiger_rolling_60_beta = tiger_rolling_60_covariance / sp500_rolling_60_variance
tiger_rolling_60_beta.tail()
```
Step 3: Use the Pandas mean function to calculate the average value of the 60-day rolling beta of the portfolio.
```python
tiger_rolling_60_beta_mean = tiger_rolling_60_beta.mean()
tiger_rolling_60_beta_mean
```
Step 4: Plot the 60-day rolling beta. Be sure to include the title parameter, and adjust the figure size if necessary.
```python
tiger_rolling_60_beta.plot(figsize=(10,5), title="Tiger Management LLC Beta - 60 Day Rolling Beta")
```
![Screenshot 2023-04-16 at 7 46 44 PM](https://user-images.githubusercontent.com/111409358/232365860-aedb069d-7d92-4a1c-a64c-2c9c2aea1755.png)

Portfolio 2<br>
Step 1: Using the 60-day rolling window, the daily return data, and the S&P 500 returns, calculate the covariance. Review the last five rows of the covariance of the portfolio.
```python
berkshire_rolling_60_covariance = daily_returns_df['BERKSHIRE HATHAWAY INC'].rolling(window=60).cov(daily_returns_df['S&P 500'])
berkshire_rolling_60_covariance.tail()
```
Step 2: Calculate the beta of the portfolio. To do that, divide the covariance of the portfolio by the variance of the S&P 500.
```python
berkshire_rolling_60_beta = berkshire_rolling_60_covariance / sp500_rolling_60_variance
berkshire_rolling_60_beta.tail()
```
Step 3: Use the Pandas mean function to calculate the average value of the 60-day rolling beta of the portfolio.
```python
berkshire_rolling_60_beta_mean = berkshire_rolling_60_beta.mean()
berkshire_rolling_60_beta_mean
```
Step 4: Plot the 60-day rolling beta. Be sure to include the title parameter, and adjust the figure size if necessary.
```python
berkshire_rolling_60_beta.plot(figsize=(10,5),title="BERKSHIRE HATHAWAY INC - 60-Day Rolling Beta")
```
![Screenshot 2023-04-16 at 7 47 38 PM](https://user-images.githubusercontent.com/111409358/232365954-560647a3-1cde-4b1b-b4d9-d63c4c882b93.png)


## Contributors
Alexander Valenzuela<br>
[LinkedIn Profile](<https://www.linkedin.com/in/alex-valenzuela-97826842/>)


## License
The Unlicense




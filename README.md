# Project Title - Algo Investment Trading Platform
This project aims to build a FinTech investment platform that leverages algorithmic trading and offers customers a one-stop investment solution for their retirement portfolios.


## Technologies
* Pathlib
* Pandas
* Numpy 
* %matplotlib inline


## Installation Guide

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

>1. Analyze the Performance

* Use the `plot` function to visualize the daily return of the four fund portfolios & the S&P 500:
*  Use the `cumprod` function to calculate the cumulative returns for the four fund portfolios and the S&P 500.  Use the `tail` function to review the last five rows of the cumulative returns DataFrame.
* Use the `plot` function to visualize the cumulative return values of the S&P 500 over time.

>2. Analyze the Volatility

* Use the `plot` function and the 'kind="box"` parameter to visualize the daily return data for each of the four portfolios and the S&P 500 in a box plot.
* Create a new DataFrame and then use the `drop` function to drop the S&P 500 column. Use the `plot` function and the `kind="box"` parameter on the new DataFrame to display the daily returns of the four fund portfolios in a box plot.

>3. Analyze the Risk
* Use the `std` function to calculate the standard deviation for each of the four portfolios and the S&P 500.  Use the `sort_values` funciton to sort from smallest to largest.
* Calculate the annualized standard deviation for each of the four portfolios and the S&P 500.  Multiply the standard deviation by the square root of the number of trading days, '252'.
* Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of the four fund portfolios and the S&P 500 index.
* Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of only the four fund portfolios. 

>4. Analyze the Risk-Return Profile
* Use the daily return DataFrame to calculate the annualized average return data for the four fund portfolios and the S&P 500 index.  Use 252 for the number of tradingf days.  Review the annualized average returns, sorted from lowest to highest.
* Calculate the Sharpe ratios of the four fund portfolios and for the S&P 500.  Divide the annualized average return by the annualized standard deviation for each.  Review the resulting Sharpe ratios, sorted from lowest to highest.
* Visualize the Sharpe ratios for the four funds and for the S&P 500 in a bar chart. 

>4. Diversify the Portfolio













## Contributors
Alexander Valenzuela<br>
[LinkedIn Profile](<https://www.linkedin.com/in/alex-valenzuela-97826842/>)


## License
The Unlicense


A `print` function in Python displays the text or variable passed in the function as output:

```python
text = ‘This is a sentence that you would like to display.’
print(text)
```

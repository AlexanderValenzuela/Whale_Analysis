# Project Title - Algo Investment
This project aims to build a FinTech investment platform that leverages algorithmic trading and offers customers a one-stop investment solution for their retirement portfolios.


## Technologies
* Pathlib
* Pandas
* Numpy 
* %matplotlib inline


## Installation Guide

Provide the instructions for installing any project dependencies.


## Usage

Importing the Data
>*About the data?*<br>
The CSV file contains net asset values (NAV) of four portfolio funds: [Soros Fund Management LLC](https://en.wikipedia.org/wiki/Soros_Fund_Management), [Paulson & Co Inc](https://en.wikipedia.org/wiki/Paulson_%26_Co.), [Tiger Global Management LLC](https://en.wikipedia.org/wiki/Tiger_Global_Management) and [Berkshire Hathaway Inc](https://en.wikipedia.org/wiki/Berkshire_Hathaway).  Also included is the [S&P 500 index](https://www.spglobal.com/spdji/en/indices/equity/sp-500/#overview), which will serve as the standard for analyzing the four portfolio funds.  

Use the `read_csv` function and the `Path module` to read the whale_navs.csv file into a Pandas DataFrame.<br>
Use the `head` function to examine the first five rows of the DataFrame.<br>
![Screenshot 2023-04-15 at 1 38 07 AM](https://user-images.githubusercontent.com/111409358/232201189-97f7cbab-4491-4cb7-9d9c-76addb62c02f.png)

Use the Pandas `pct_change` and the `dropna` functions to create the daily returns DataFrame.<br>
![Screenshot 2023-04-15 at 2 38 26 AM](https://user-images.githubusercontent.com/111409358/232206080-f51e43cb-3886-4a76-a583-5adf68b78e51.png)


Quantitative Analysis







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

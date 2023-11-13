## Project 1: Financial Analysis

### Helpful Links

*Yahoo finance [https://finance.yahoo.com] - provided stock data

*Py Portfolio Opt [https://pyportfolioopt.readthedocs.io/en/latest/] - provides portfolio optimization.

*HV Plot [https://hvplot.holoviz.org] - provides high level plotting.

*Matplotlib[https://matplotlib.org] - provides interactive visualization. 

*Pandas[https://pandas.pydata.org] - provides open source data and allows for data manipulation.

*Numpy[https://numpy.org] - provides scientific computing.

--------

**##QUESTIONS**

<details>
<summary>**What are the stocks that will be analyzed?**/summary>
Create a list of multiple stocks to be analyzed. Make sure to include stocks of all variations to be able to have a wide variety of possible allocations. As follows:

**tickers = ["TSLA", "BIDU", "NVDA", "AAL", "AMD", "WMT", "DIS", "DHR", "PANW","AAPL","MCL.CN","FI"]

</details>
<summary>**What is Yahoo Finance and what was it able to provide?**</summary>
Yahoo Finance is a library that is able to provided current and historical stock data at any given moment. It's a source outlet for those who like to use online tools to receive news, data, and financial reports from the stock market. In this instance we will be able to get each stocks historical and current price along with its adjusted close stock price. 

**stock_data = yf.download(tickers, period="10y")

**prices = pd.DataFrame(stock_data["Adj Close"].dropna(how="all"))


</details>
<summary>**What is your Portfolios Proposal?**</summary>
Our project is to build an optimal portfolio by analyzing historical data from stocks 
and comparing it to SPY(a benchmark portfolio) and an equal weight portfolio.
We will determine which portfolio performs the best by evaluating Returns and Sharpe Ratios and will also examine the ideal portfolio for each asset by minimizing risks and maximizing profits. 

**combined_df = pd.concat([cumulative_profit_ef,cumulative_profit_ew,cumulative_profit_spy], axis='columns', join='inner')
combined_df.columns = ["Optimized", "Equal Weight","SPY"]
combined_df


<details>
<summary>**Modern Portfolio Theory**</summary>
MPT, also known as mean-variance analysis, is a mathematical framework 
for constructing a portfolio of assets to maximize expected returns and minimize risks.

<details>
<summary>**Expected Return**</summary>
The expected return of the portfolio is calculated as a weighted sum of the individual assets
returns. The Portfolio risk depends on the proportion (weights) invested in each stock, their individual risks, and the correlation or covariance. 

**#Used pyportfolioOpt to find our expected returns per stock using Capital Asset Pricing Model.
mu = expected_returns.capm_return(prices)
mu


<details>
<summary>**Covariance**</summary>
Covariance is a measurement of the spread between numbers in a dataset. The higher the variance of an asset 
price, the higher the risk asset bears and a higher return.

**#created a covariance matrix through pyportfolioOpt to compare all stocks to eachother
sample_cov = risk_models.sample_cov(prices, frequency=252)
sample_cov

<details>
<summary>**Capital Asset Pricing Model**(CAPM)</summary>

The capital asset pricing model(CAPM) is a financial model that calculates the expected rate of return for an asset or investment. It establishes a linear relationship between the required return on an investment and risk. It is based on the relationship between an asset's beta, the risk-free rate, and the expected return on the market minus the risk-free rate.

**#Used pyportfolioOpt to find our expected returns per stock using Capital Asset Pricing Model.
mu = expected_returns.capm_return(prices)
mu


<details>
<summary>**Efficient Frontier**</summary>
An Efficient Frontier represents all possible portfolio combinations. It has the maximum return portfolio,
which consist of a single asset with the highest return at the extreme right and the minimum 
variance portfolio on the 
extreme left. The return represents the y-axis, while the level of risk lies on the x-axis.

**#PyportfolioOpt finding weights for our optimized portfolio on the efficient frontier
S = risk_models.CovarianceShrinkage(prices).ledoit_wolf()
ef = EfficientFrontier(mu, S)
weights = ef.max_sharpe() #for maximizing the Sharpe ratio #Optimization
cleaned_weights = ef.clean_weights() #to clean the raw weights


**ef.portfolio_performance(verbose=True);
Expected annual return: 41.1%
Annual volatility: 27.3%
Sharpe Ratio: 1.43


<details>
<summary>**Portfolio Findings**</summary>

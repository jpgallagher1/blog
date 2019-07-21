---
layout:     post
title:      Momentum Trading Strategy
date:       2019-06-19 14:19:56
author:     John Gallagher
summary:    In this post we will build a momentum strategy from scratch and show the diversification benefits. 
categories: Quant Finance
thumbnail:  star
tags:
 - Quant
 - Momentum
 - Trading
 - Finance
 - Strategy
 - Algorithm
 - Algorithmic
 - Risk
 - Diversification
 - Portfolio
---

# A Simple Algorithmic Trading Strategy

Incorporating multiple strategies and factors into your portfolio helps diversify against concentrated risks.  In this post we will build a simple momentum strategy from scratch and show the diversification benefits.  

![Lower Volatility Portfolio Returns](/blog/img/BlendedvsBenchmar_Rolling_Returns.png)

## The Momentum Risk Premium

Within investing, a security's return can be modeled as a function of several different parameters.  For example, using capital asset pricing model: 

$$E[R_i] = R_{free} + \beta_i(R_{market} - R_{free})$$

Where $$E[R_i]$$ is the expected return of asset $$i$$.  The total return is the sum of the risk free rate of return, $$R_{free}$$, and the asset's relationship to the market return, $$\beta_i(E[R_{market}]-R_{free})$$.  One of the major limitations of this model, is the simplicity.  This model ignores many other possible factors that could affect an assets price, for example momentum. 

Momentum is the tendency for assets to continue to perform the way they have.  For example, if a stock has performed well, momentum assumes the stock will continue to perform well.  If a stock ahs performed poorly, momentum similarly assumes the stock will continue to fall in price.  

Although there are many ways to model momentum, we will use a simple trailing 3 month return. $$R_{3m}$$

## The Backtest and Methodology

First we begin by selecting our universe of stocks to pick from. We will use the S&P 500 Financial sector (50 companies) and 5 years of trading days (1260 days).

We calculate the return history, and the trading signal, rolling 3 month return.  After ranking the signals, the signal is lagged by one day to prevent look ahead bias.  Then we long buy the top 18, (strongest signal), and short sell the bottom 18 companies with the weakest signal.  The number long/short is arbitrary but this, along with this signal is one of many parameters that can be optimized.  

After we find the holdings, we then calculate each holding's performance.  This is done by multiplying the holdings and the return matrix.  The holdings are positive if we are long the security and negative if we are short.  The weighting is 1/36th of the portfolio for each security.  This represents half of our portfolio long and half of our portfolio short.  We will be net neutral towards the market.  This is also optional, as you can change each holdings' weight.  It is also possible to go net long or short.  The optimization of holdings, via risk models is another area that can be tweaked.  

## Results

We can see here that the strategy offers diversification benefits.  It performs differently than the financial sector as a whole.  It also performs differently than the S&P 500.  The diversification benefits can be seen when examining the rolling volatility.  Through the different time periods, it is clear that a combination of the strategy and the S&P 500 offers lower volatility, as well as higher risk adjusted performance.  

- IYG, IShares US Financial Services ETF
- SPY, SPDR S&P 500 ETF
- Port, The Momentum strategy by itself
- 50/50, SPY and the momentum strategy blended 50%/50%, rebalanced daily.  

![A Comparison of Historical Performance](/blog/img/Pure_and_Blended_StrategyvsBenchmarks.png)

Below we can see the volatility of the portfolio is significantly reduced.  

![Rolling Volatility Comparison](/blog/img/BlendedvsBenchmark_Rolling_Volatiltiy.png)


Lastly in this table, we find that the portfolio does offer significant risk reduction benefits, reducing the overall volatility of the portfolio by nearly half of the S&P500's annualized volatility over the last 5 years.  13% compared to 7.3%   It is also significantly less than the IShares US Financial Services ETF. 18% compared to 7.3%

|        | SPY  | IYG  |Port  |**50/50**|
| :---:  |:---: |:---: |:---: |  :---:  |
| Return | 9.4% | 9.1% | 4.5% |**6.9%** | 
|  Vol   |13%   |18%   | 8.1% |**7.3%** |
| Sharpe | 0.713| 0.498| 0.559|**0.951**|


The blended strategy spends significantly less time underwater than the S&P 500.  In this chart, we can see how much shallower the draw-downs are.  

Benchmark Drawdown Chart (SPY)

![Benchmark Drawdown](/blog/img/BenchmarkDrawdowns.png)

Blended Portfolio Drawdown Chart

![Blended Portfolio Drawdown Chart](/blog/img/Blended_Drawdowns.png)

You can find the source code on [my github](https://github.com/jpgallagher1/Risk-Premiums)
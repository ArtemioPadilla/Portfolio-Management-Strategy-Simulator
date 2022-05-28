# Portfolio Management Strategy Simulator

Portfolio management strategies can bring with them some heated discussions. Which metric is the most important? What is the best way to optimize a portfolio? How to choose our assets?

This project implements a Portfolio Management Strategy Simulator that tests a variety of different possible management strategies.

The asset selection is based on a ranking function which serves as a metric to evaluate the possible stocks candidates and selects only a subset of them to then optimize the portfolio with the selected stocks.

Smart beta strategies are usually referred to as a mid-term strategy between active investing and passive investing. An active investing strategy requires from the investor an active role in picking the assets to invest, while a passive strategy requires almost no active roll [[1]](https://corporatefinanceinstitute.com/resources/knowledge/trading-investing/smart-beta/).

A smart beta strategy is therefore based on a set of fixed rules that are usually automatically applied to portfolio operations and ensure that the portfolio will follow a predefined behavior based on a range of factors. This is why a smart-beta strategy is also sometimes referred to as a [factor investing](https://www.blackrock.com/us/individual/investment-ideas/what-is-factor-investing).

The factors to be chosen for the rules of the portfolio operation are varied, some are based on technical analysis metrics, such as the [Nifty 200 Momentum 30](https://www.niftyindices.com/indices/equity/strategy-indices/nifty200-momentum-30) which selects a portfolio of assets based on momentum, others smart-beta strategies may take factors such as metrics from fundamental analysis, credit scores, volatility or even sustainability and moral factors into consideration for asset selection [[2]](https://www.blackrock.com/us/individual/investment-ideas/what-is-factor-investing)[[3]](https://www.blackrock.com/us/individual/investment-ideas/sustainable-investing).

With this in mind, this project will implement a Portfolio Management Strategy Simulator that weekly selects and invest all avaliable capital in a subset of selected assets from an bigger universe of candidate assets by ranking the canditate assets with a generic ranking function $f$ defined in this project as:

$$f(\text{stock price history}, t)\rightarrow m$$

Where $t$ the number of trading calendar days into the past to take into account to get the score $m$ for the $\text{stock price history}$ up to the present moment in the simulation.

With this ranking function, one can propose a selection of the top N stocks to where to allocate funds. To know how much of the available capital to allocate to each selected asset one could use the ranking itself but there are already well know optimization techniques for portfolios. In the current implementation of the simulator, the available options are to optimize to get the Maximum Sortino Ratio (MSR) portfolio or the Global Minimum Volatility (GMV) portfolio.

Optimizing for the chosen subset of assets using the ranking function lets the simulator reduce the size of the state space for the possible portfolio capital allocations and therefore require less computational power and will be quicker to process.

Rankings are thoroughly used in society and are a way to reduce the complexity of a system into a simpler metric that can be used to compare elements within the system [[4]](https://www.nature.com/articles/s41467-022-29256-x#:~:text=Rankings%20reduce%20complex%20systems%20to,temporal%20rank%20data%20is%20aggregated.).


Rankings are used everywhere, from fields like sports [(e.g. the NFL's top 100 player rankings)](https://www.nfl.com/network/shows/nfl-top-100) to sociology, where one could measure the influence of people by [ranking them by the number of Instagram followers](https://en.wikipedia.org/wiki/List_of_most-followed_Instagram_accounts) going all the way to money and power, where one can get a list like the [Forbes annual richest list](https://www.forbes.com/billionaires/).

Since many ranks usually are really big or don't have clear bounds (for example the actual complete ranking for the richest persons) in practice many rankings are further simplified to a top-N ranking.

So far the factors implemented to rank the assets are:

- Random Ranking
- Momentum
- Historic VaR 

None-the-less, the simulator is implemented in such a way where other functions can be easily applied in future work.

## Algorithm

The algorithm of the Portfolio Management Strategy Strategy Simulator is the following:
        
    - Define algorithm hyperparameters
        
    - Every chosen weekday (if possible):
        - Get the top N stocks for the day according to rank by criteria and t
        - Optimize portfolio weights according to the chosen technique and window
        - Allocate all available capital (Buy stocks)
        
## Suppositions

- The universe of possible stock candidates is the S&P500 

- All historic prices analyzed are closing prices of the day

- For simplicity, we will not consider transaction fees

- The expected return will be estimated as the annualized return in the window of analysis

- The expected return and variance-covariance matrix are calculated with data from the windows of analysis

- We will assume we can buy hole stocks and fractions of stocks

- We will allocate all available capital each week

- We can't take short positions

- We will trade weekly on the specified weekday by the user. If that day of the week the markets are close the portfolio will hold the previous week's assets until the next tradeable day and resume the algorithm


## Capabilities

The current version of this simulator lets the user specify the following hyperparameters:

- Ranking Function
- $t$ the hyperparameter of the ranking function
- $N$ (for top N selection)
- The optimization technique (MSR, GMV or equally weighted)
- The window of analysis of historic prices to use in the optimization
- The initial capital
- The start date of the simulation
- The end date of the simulation
- The historic risk-free rate
- The weekday to trade
- The minimum weight for allocation
- The maximum weight for allocation


The simulation also lets the user track the allocations and close market days to further study portfolio behavior and increase behavior traceability.


The recorded portfolio behavior is compared to the S&P500 and the risk-free rate.

Implemented in Python

[Download notebook](https://github.com/ArtemioPadilla/Portfolio-Management-Strategy-Simulator/raw/main/PMSS.ipynb)

[View Notebook in HTML](https://artemiopadilla.github.io/Portfolio-Management-Strategy-Simulator/PMSS.html)

[View slideshow](https://artemiopadilla.github.io/Portfolio-Management-Strategy-Simulator/)


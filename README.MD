# TASS - A trading algorithm
## Description
Aims to be a fully self-ruling trading algorithm. It uses the scalping strategy based on different indicators.
## Third Party
The trading API used is [Alpaca](https://github.com/alpacahq/alpaca-trade-api-python). The stocks to trade are retrivied from [Yahoo Finance](https://finance.yahoo.com/).
## TODO
Further documentation will be provided explaining the code and how to use it.

Currently the project is in back testing. After that it will enter a paper trading training phase, and finally will be tested with real money.
## Progression
### Report of 24-05-2020
#### Work done
The implemented indicators are the following: STOCH, MACD, SAR, RSI, VWAP.
All except VWAP are computed with the tA-Lib module.
However, the decision of each indicator is custom made.

The only available strategy for now is scalping.
It as the ability to choose the best indicators regarding a given dataset.
It can also choose the best ratio from a given range, regarding a given dataset.
The ratio determine the percentage of decisions regarding a position that need to be filter or not.
The final decision is based on every decision of each choosen indicators, filtered by the ratio.

There are 2 types of trading : back trading (with existing data) and front trading (paper trading for now).
The front trading uses the front API, and the back trading uses the back API.
The front API is a layer of the main API, which is Alpaca for now. It simply translate the function.
The back API is more complex. It basically divides the dataset in 2 parts.
The first part is a initialization set or a learning set which is used to compute the different parameters specified above.
The second is the training set where the algorithm will run.
#### Current results
The algorithm can run of every stock, up to 10 stocks approximitly (limited by trending stocks retriever).
It seems to bring consistent results with an average profit of 0.83 % running on 9 stocks.
However it is better to run it only on 5 stocks per session, with an average profit of 1.43 %.
Of course, the algorithm looses sometimes when running on only 1 stock.
But this loss is smoothed by the fact that, when running on multiple stocks, it tends to win for than loose.
To have more relevant results, the algorithm will run a month on a paper trading account with a starting balance at 1000 $.
### Report of 05-06-2020
#### Work done
The algorithm is now running 24/7 using paper trading on a cloud server (heroku worker) according to the market hours.
The tA-Lib module as been replaced by finta due to compatibilty issues with the cloud server.
ADX indicator has been added.
Backtrading is now very fast due to multiprocessing pools (parallelize).
The algorithm is now only selecting profitable stocks by testing a bunch of them.
It also select the best mode (trending tickers or most active stocks).
The API layer is now more robust. It can handle api issues by waiting and retrying or aborting without causing the algorithm to crash.
For example it's waiting the order to be cancelled properly before closing the related position.
#### Current results
The algorithm has been running in paper trading from 01-06-2020 to 05-06-2020. The results are over expectations.
We were aiming at a 2.5 % profit and the algorithm showed a 5.647 % profit for the week.
Of course we don't want to be result oriented and we'll see what it does next week.
But this is encouraging.
## Issues
### Residencing
The Alpaca API requires an American passeport or visa in order to trade with real money.
I am a French citizen so this will be a problem.
They may open American stocks trading to other countries but it's not confirmed yet.
It the mean time, I still have time to look for an other API before the algoritm starts trading with real money (if profitable enough).

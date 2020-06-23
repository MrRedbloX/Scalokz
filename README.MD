# Scalokz - A trading algorithm
## Description
Aims to be a fully self-ruling trading algorithm. It uses the scalping strategy based on different indicators.
## Third Party
The trading API used is [Alpaca](https://github.com/alpacahq/alpaca-trade-api-python). The stocks to trade are retrivied from [Wikipedia S&P500](https://en.wikipedia.org/wiki/List_of_S%26P_500_companies) and [Yahoo Finance](https://finance.yahoo.com).
## Join
For more information, you can go to the official [website](https://www.scalokz.com).
## Structure
The app submodule is just the repository for the website.
The main-worker submodule will run the core of the algorithm, making decisions and transactions in real time for every client.
The other workers submodules are here to take some workload that takes time. For example backtrading on hundreds of symbols at the same time to choose only profitable ones.
All of these submodules can communicate with each other via a [MongoDB](https://www.mongodb.com/) database.

# Algorithmic Trading using Technical Analysis

## Summary
This analysis attempts to build a machine learning model to generate buy/sell trading signals of an investible asset based on technical indicators like momentum, volatility, trends, etc.  

A couple of machine learning models are built.  Random Forest, LightLGM, XGBoost to name a few and finally using crowd wisdom VotingClassifer to consolidate all the trading signals.

Each model is trained, cross validated and tuned using historical data before 1 Jan 2020 and then forward tested on unseen data after 1 Jan 2020.  Trading performance is shown at the end of this analysis.

## Trading Instrument
Cryptocurrency BTCUSD is the trading instrument picked for this analysis.

## Data
*To register your own API key to assess the Binance API.*  

1-min OHLC prices to be downloaded using Binance API.  Prices will be resampled at 15-min intervals for model training.

## Machine Learning
### Multiclassification Models
1. Random Forest
2. LightGBM
3. XGBoost
4. Gradient Boosting Trees
5. Voting Classifier

### Features
1. Technical Indicators
2. Candlestick Patterns
3. Historical Return

### Target Label
Next hourly return broken down into 3 buckets:
1. **Red**: Next Hourly Return < -0.015
2. **Yellow**: Next Hourly Return between -0.015 to 0.015
3. **Green**: Next Hourly Return > 0.015

## Trading Strategy
The model predicts with probability where the next hourly return will be one of the 3 possible targets: Green, Yellow and Red.  Under unbiased random sampling, each target should have a probability of 33.33%.  One can consider taking a trade when the model predicts with a probability greater than 33.33%.

Hence,
1. Trade the instrument when the model predicts with probability of at least 45%.  **Green** to go long and **Red** to go short.
2. Hold and close the position after exactly 1 hour.

## Forward Testing
Trading strategy testing on unseen forward data.  Performance of each trade is consolidated and measured against a benchmark which is the performance of the trading instrument over the same period.

## Notebook
https://github.com/edgetrader/algo-trading-ta/blob/master/notebook/algo-trading-ta.ipynb

## Useful Libraries
1. [Binance REST API python implementation](https://pypi.org/project/python-binance/)
2. [Technical Analysis Library in Python](https://pypi.org/project/ta/)
3. [Hurst exponent evaluation and R/S-analysis](https://pypi.org/project/hurst/)

## Reference
1. [How to Use Binance API Key | Full Guide](https://cryptopro.app/help/automatic-import/binance-api-key/)
2. [Technical Analysis Library in Python](https://github.com/bukosabino/ta)
3. [Python wrapper for TA-Lib](https://github.com/mrjbq7/ta-lib)
4. [An unofficial mirror to the old SF repo](https://github.com/TA-Lib)

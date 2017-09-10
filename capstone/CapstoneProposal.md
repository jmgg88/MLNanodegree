# Machine Learning Engineer Nanodegree
## Capstone Proposal
Juan Manuel García
September 6, 2017

## Proposal // Trading expert system

### Domain Background

The stock markets provide a perfect environment for using big data techniques. The number of possibilities are endless, since the amount of data and the possible correlations existing between different market indicators, prices and stock values is enormous. A proper analysis of market data can lead to a better understanding of its behaviour, unvealing unexpected properties, relations between pairs of stocks, or even providing prediction capabilities to some extent. Though a high level of theoretical controversy exists around the idea that markets can be profitably traded (see [2]), many trading systems exist that, when traded consistently, show significant profit (10%-20%). More importantly, these systems are adaptative in the sense that they do not require a healthy global economy (a global rising trend) to make profit, but rather act differently in the different situations so that a benefit is achieved. Consistent and intelligent trading requires facing the markets as a statistical environment in which no certainties exist (like a poker game), trying to maximize the Benefit/Risk ratio that is put at stake in each market operation. 

The process of analyzing the markets and systematically applying a trading system that is able to detect good trading opportunities is tedious to be performed manually and, even when the system rules are clear, it is often hard to automate them since they are based on visual indicators that cannot be easily transformed into a numerical detection algorithm. The aim of this project is to use Deep Learning techniques to obtain a prediction model for stock values based on their historical data. Using this prediction model, an expert system able to automatically signal potential entry opportunities will be built, thus reducing all the manual work to a simple review of the signaled opportunities.


### Problem Statement

Design an intelligent automatic system that alerts the user whenever a profitable trading opportunity appears in any NYSE or NASDAQ traded stock. The time frame to be used for trading is the daily one.

A profitable trading opportunity is defined as follows. Let's assume a prediction for the closing price of the stock exists for each of the next N days. If a position is to be taken today, let there be a systematic rule to compute the stop loss level (protection level beyond which, if the price moves in that direction, the operation is considered failed and the position is closed with control amount of loss). The current situation is considered a profitable trading opportunity if, for any of the next N days the following rules are fulfilled:
+The Benefit/Risk = (predicted price - current price)/(current price - stop loss) ratio is above 2.5
+The price never triggers the stop loss between day 1 and day N (i.e., price > stop loss always)

Thus, the core of the system relies on a tool to predict the future expected closing price of a generic stock value for the following N days (with N in the order of 5 to 10 days). The rule to define the stop loss will be developed as part of the process, but shall be a simple rule based on historical parameters. 


### Datasets and Inputs

A set of 30 stocks will be selected based on the following criteria:
+ Average variation of closing price between one day and the next between 1.5% and 5%: we want to discard values which vary very little, thus presenting no trading opportunity, and very noisy values.
+ Average volume of traded contracts above 500000: we want to trade liquid stocks
+ Price range between 10$ and 150$: these values are better adapted to normal account sizes (in the order of thousand of dollars). 

For each selected stock, the following data is considered relevant to the model:
+Minimum/Maximum/Opening/Closing weekly price of the stock
+Minimum/Maximum/Opening/Closing daily price of the stock
+Volume of the stock
+Force Index of the stock (a derived indicator which is simply computed as [close(n)-close(n-1)]/volume(n). Other indirectly computed indicators could also be added during the implementation process if required. 

In addition, the following data is considered relevant for all the stocks:
+Minimum/Maximum/Opening/Closing weekly SP500 value
+Minimum/Maximum/Opening/Closing daily SP500 value

The time range to be analyzed will cover the span between 01/01/2000 and 31/12/2016. This is important because different market regimes exist during this period, and the resulting model should be able to adapt to these changes. The period from year 2000 to year 2012 (included) will be used as training set, and the period from 2013 to 2016 will be used as testing set. From the set of selected stocks, 20 will be used in the training process as described above. The other 10 will be reserved for extra testing without having shown any part of their history to the system. This is necessary to test the ability of the system to generalize to any provided stock.

The data to be used for the project will be retrieved from Yahoo Finance through a python API (see [3])

### Solution Statement

Since the nature of the market data is sequential, the proposed solution is to model the system using a Recurrent Neural Network, which is intrinsicly adapted to the structure of the problem. The network will be provided with depth since experimental evidence strongly suggests this helps obtaining a better model (see [1]). In addition, the proposed solution will use Long Short-Term Memory cells (LSTMs) since it is expected they will be able to learn better the market behaviours, which are highly influenced by long and short term depdendencies. It is expected that this will also allow the model to better adapt to the different market regimes (trendy or lateral). The architecture and tuning of the network will be iterated as part of the project. The implementation will be performed in python using tensorflow.


### Benchmark Model

The objective of the system is to outperform the market in a real world trading scenario. To measure this, the outcome of the system will be compared against three different benchmark models for different running periods of time (of a year duration):

+ Buy (or sell) and hold for the SP500 
+ Buy (or sell) and hold for the stock at stake
+ Optimal swing trading for the stock at stake

The first two benchmark models simply give an indication about whether the system is any good or not. Performing worse than them simply implies a naive trading strategy is better than our sophisticated system. Performing better indicates simply the opposite, which doesn't say much about the profitability of the model. 

The third benchmark however is an approximation to the "perfect trading strategy", one that would maximize the outcome of the market by taking advantage of all the price swings in both directions. Thus, comparing against this benchmark indicates how close the model is to the maximum possible profitability.

### Evaluation Metrics

The network performance will be evaluated using the normalized sum of the squared errors of the predicted prices compared against the actual prices. This will provide a measure of the quality of the prediction model. 

The full system performance will be evaluated by comparison with all three benchmark models proposed above by comparing the earnings obtained for periods of one year applying each of the strategies (starting with the same initial account size). The benchmark metric will simply be computed as the ratio between the final value of the trading account using the developed model and the final value using the benchmark models. 

### Project Design

The project will be split in the following phases:

#### 1. Data retrieval
- Select a representative set of 30 stocks based on the criteria described above
- Retrieve the historical data of the previous stocks and store in convenient format
- Implement and test a small set of python functions to easily access the input data

#### 2. Data preprocessing
- Compute extra derived indicators required for the model (Force Index, etc)
- Analyze possibilities for data normalization 
- Implement functions for data normalization
- Normalize the data
- Split the dataset into training and testing sets

#### 3. Develop RNN model
- Propose several RNN architectures
- Train all of them and iterate, tuning the model until a good result in terms of price prediction is achieved

#### 4. Develop trading simulation
- Develop trading strategy and implement functions for each criterion
- Encapsulate the RNN model into an expert system that provides trading signals according to the previous trading strategy
- Visualize of the signaled opportunities and iterate until the number and quality of them is optimized
- Create expert systems for the different benchmark models
- Develop functions to backtest a trading system

#### 5. Compute the model benchmark
- Backtest all the systems for different running periods of one year
- Compute the benchmark of the model

#### 6. Conclusions
- Based on the benchmark results, analyze how good and useful the model is
- Propose possible future steps and improvements for the model (e.g., expansion to different time frames)


### References

[1] Goodfellow I., Bengio Y., Courville A. - Deep Learning
[2] Efficient Market Hypothesis - https://en.wikipedia.org/wiki/Efficient-market_hypothesis
[3] Yahoo Finance Python API - https://pypi.python.org/pypi/yahoo-finance


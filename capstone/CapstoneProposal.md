# Machine Learning Engineer Nanodegree
## Capstone Proposal
Juan Manuel García
September 6, 2017

## Proposal 

### Domain Background
_(approx. 1-2 paragraphs)_

The stock markets provide a perfect environment for using big data techniques. The number of possibilities are endless, since the amount of data and the possible correlations existing between different market indicators and stock values is enormous. A proper analysis of market data can lead to a better understanding of its behaviour, unvealing unexpected properties, relations between pairs of stocks, or even providing prediction capabilities to some extent. Though a high level of theoretical controversy exists around the idea that markets can be profitably traded, many trading systems exist that, when traded consistently, show significant profit (10%-20%). More importantly, these systems are adaptative in the sense that they do not require a healthy global economy (a global rising trend) to make profit, but rather act differently in the different situations so that a benefit is achieved. Consistent and intelligent trading requires facing the markets as a statistical environment in which no certainties exist (like a poker game), trying to Benefit/Risk ratio that is put at stake in each market operation. 

The process of analyzing the markets and systematically applying a trading system that is able to detect good trading opportunities is tedious to be performed manually and, even when the system rules are clear, it is often hard to automate them since they are based on visual indicators that cannot be easily transform into a numerical detection algorithm. The aim of this project is to use Deep Learning techniques to obtain a prediction model for stock values based on their historical data. Using this prediction model able to automatically signal potential entry opportunities can be built, thus reducing the manual work to a simple review of the signaled opportunities. 


### Problem Statement
_(approx. 1 paragraph)_

The problem to solve can be stated as follows:

Design an intelligent automatic system that alerts the user whenever a profitable trading opportunity appears in any NYSE or NASDAQ traded stock. The time frame to be looked at depends on the global behaviour of the market (global ascending trend or anything else). The user shall be able to select between these two options depending on his analysis of the global market status. 

A profitable trading opportunity is defined as follows. Let's assume a prediction for the closing price of the stock exists for each of the next N days. If a position is to be taken today, let the rule of parallel colors (To be explained) define the price of the stop loss for that order. The current situation is considered a profitable trading opportunity if, for any of the next N days the following rules are fulfilled:
+The Benefit/Risk ratio is above 2.5
+The price never triggers the stop loss between day 1 and day N

Thus, the core of the system relies on a tool to predict the future expected closing price of a generic stock value for the following N days (with N in the order of a few days). 

The prediction tool will apply Deep Learning, particularly Recurrent Neural Networks (and more precisely LSTMs). The prediction accuracy will be measured by comparing the actual prices of some testing set to the predicted prices (so really in terms of predicted values and not in terms of trading benefits). 


In this section, clearly describe the problem that is to be solved. The problem described should be well defined and should have at least one relevant potential solution. Additionally, describe the problem thoroughly such that it is clear that the problem is quantifiable (the problem can be expressed in mathematical or logical terms) , measurable (the problem can be measured by some metric and clearly observed), and replicable (the problem can be reproduced and occurs more than once).

### Datasets and Inputs
_(approx. 2-3 paragraphs)_

The data to be used for the project will be retrieved from Yahoo Finance through the python API shown in the reference (TBD). The data consists of the following elements:

+Minimum/Maximum/Opening/Closing weekly price of the stock
+Minimum/Maximum/Opening/Closing daily price of the stock
+Minimum/Maximum/Opening/Closing weekly SP500 value
+Minimum/Maximum/Opening/Closing daily SP500 value
+Volume of the stock
+Force Index of the stock and potentially other indirectly computed indicators

The set of stock values will be chosen arbitrarily from the set of stocks traded in NYSE or NASDAQ fulfilling the following conditions:
+Their mean price is above 8$
+Their mean trading volume is above 500000
+JMG to add the other conditions


In this section, the dataset(s) and/or input(s) being considered for the project should be thoroughly described, such as how they relate to the problem and why they should be used. Information such as how the dataset or input is (was) obtained, and the characteristics of the dataset or input, should be included with relevant references and citations as necessary It should be clear how the dataset(s) or input(s) will be used in the project and whether their use is appropriate given the context of the problem.

### Solution Statement
_(approx. 1 paragraph)_

In this section, clearly describe a solution to the problem. The solution should be applicable to the project domain and appropriate for the dataset(s) or input(s) given. Additionally, describe the solution thoroughly such that it is clear that the solution is quantifiable (the solution can be expressed in mathematical or logical terms) , measurable (the solution can be measured by some metric and clearly observed), and replicable (the solution can be reproduced and occurs more than once).

### Benchmark Model
_(approximately 1-2 paragraphs)_

In this section, provide the details for a benchmark model or result that relates to the domain, problem statement, and intended solution. Ideally, the benchmark model or result contextualizes existing methods or known information in the domain and problem given, which could then be objectively compared to the solution. Describe how the benchmark model or result is measurable (can be measured by some metric and clearly observed) with thorough detail.

### Evaluation Metrics
_(approx. 1-2 paragraphs)_

In this section, propose at least one evaluation metric that can be used to quantify the performance of both the benchmark model and the solution model. The evaluation metric(s) you propose should be appropriate given the context of the data, the problem statement, and the intended solution. Describe how the evaluation metric(s) are derived and provide an example of their mathematical representations (if applicable). Complex evaluation metrics should be clearly defined and quantifiable (can be expressed in mathematical or logical terms).

### Project Design
_(approx. 1 page)_

In this final section, summarize a theoretical workflow for approaching a solution given the problem. Provide thorough discussion for what strategies you may consider employing, what analysis of the data might be required before being used, or which algorithms will be considered for your implementation. The workflow and discussion that you provide should align with the qualities of the previous sections. Additionally, you are encouraged to include small visualizations, pseudocode, or diagrams to aid in describing the project design, but it is not required. The discussion should clearly outline your intended workflow of the capstone project.

-----------

**Before submitting your proposal, ask yourself. . .**

- Does the proposal you have written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Solution Statement** and **Project Design**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your proposal?
- Have you properly proofread your proposal to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?

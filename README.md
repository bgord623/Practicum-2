# Practicum 2
Title: **Predicting daily stock market movement with machine learning**

**Table of Contents**
1. Overview
2. Scoring
3. Data
4. Exploratory data analysis and visualization
5. Modeling of investment strategies
6. Evaluation

# Overview
The purpose of this project is to create a daily stock direction prediction tool. I’ll be working with Tesla (TSLA) stock market data but ideally the techniques can be applied broadly. Investment strategies focused on classification, including machine learning algorithms, will make buy (1) and sell (0) predictions of the stock before the trading day begins. Specifically, a buy (1) prediction indicates the sign of the return (i.e., daily percent change) will be positive for the predicted day, while the sell (0) prediction indicates the sign of the return will be negative. The presentation covers the final notebook and detailed notebooks are located in weekly folders.

# Scoring 
Scoring focused on financial performance and accuracy score during the test data timeframe (1/3/23 – 4/19/23).
- Financial performance reflects the difference in percentage points between the TSLA stock performance and strategy performance
- Accuracy score is the number of correct predictions divided by the number of total predictions
# Data
Stock data was obtained with the yfinance library, which utilizes the Yahoo Finance API and Pandas to allow one to easily download stock data to a DataFrame:
![image](https://user-images.githubusercontent.com/102693978/235254630-f0a92858-ccfa-4e68-8e0b-1669e4bf9618.png)
Data downloaded with yfinance contains no missing values but frequently calculations to the data create missing values, such as adding price lags and calculating moving averages. These null values always occur at the head-end and are least important for the purposes of this project, and thus deleted. <br> I wanted to start with simple techniques as well as a simple dataset, so only the closing price (‘Adj Close’) was retained. Feature engineering began with creating a daily ‘return’ (% change) and creating ‘lags’ of those returns in an attempt to create a pattern leading to the sign of the return:
![image](https://user-images.githubusercontent.com/102693978/235254697-662d6330-300b-4ec1-bee2-3b2cf35750be.png)
# Exploratory data analysis and visualization
Various market indicator data was explored including US Treasury data and Financial Industry Regulatory Authority (FINRA) data, but a comparison with TSLA stock did not reveal useful insight. <br> Several market indicators were also explored including volatility, relative strength index, Bollinger bands, moving average convergence divergence (MACD), and candlesticks. While many of those showed promise, the MACD was easiest to understand and incorporate during later stages.
![image](https://user-images.githubusercontent.com/102693978/235254799-83be5621-fbec-44d7-83ea-963824dfd7d4.png)
# Modeling of investment strategies
Investment strategies modeled include:
- Indicator Strategies
  - MACD
  -	Momentum
- Linear Regression (ordinary least squares)
- Logistic Regression (Sklearn)
- Deep Learning (Keras)

After reviewing modeling results, I adjusted the approach to the problem by adding features, adding lags of those features, and choosing a new classification algorithm:
- Features (10 lags each)
  - Rolling volume
  - Rolling daily minimum price
  - Rolling daily maximum price
  - MACD buy/sell signal
- AdaBoost() classification algorithm
# Evaluation
The full results are shown in the table below. As the models increased in complexity (deep learning/revised approach), overfitting was apparent and financial performance on the test data exceeded only the momentum strategy. The revised approach provided the highest accuracy scores and the MACD strategy had the top overall financial performance. 
![image](https://user-images.githubusercontent.com/102693978/235255264-21bdbf69-2e13-4315-9256-a358832f60ab.png)
Regarding deployment, I believe much more analysis & insight is needed before any of these models can be relied upon for consistent positive returns.

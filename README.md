# 📈 Nasdaq-Closing-Price-Prediction-Challenge: An Optiver Case Study

### Abstract 🎯
This project aims to develop a sophisticated model capable of predicting the closing price movements of Nasdaq-listed stocks during the critical final ten minutes of the trading day. By integrating and analyzing data from both the order book and closing auctions, the model leverages insights into nuanced supply and demand dynamics to forecast price movements and identify lucrative trading opportunities. To enhance model performance, Optuna, an open-source optimization library, is utilized for the efficient and automatic tuning of hyperparameters. The predictive performance of the model is measured using the Mean Absolute Error (MAE) between predicted and observed stock closing prices.

### Introduction 🚀
Predicting stock market movements, especially in the volatile closing minutes, is a complex challenge that attracts significant attention from financial analysts and traders. The Nasdaq stock market, characterized by high liquidity and rapid price changes, presents a fertile ground for applying advanced predictive analytics. This project focuses on harnessing detailed order book data and closing auction information to build a model that not only predicts the closing prices but also uncovers potential trading strategies during peak trading times. To optimize the model’s parameters, we employ Optuna, a sophisticated hyperparameter optimization framework. Optuna enhances the model development process through its support for several state-of-the-art algorithms, such as the Tree-structured Parzen Estimator (TPE), Categorical Algorithm for Numerical and Categorical Bayesian Optimization (CMA-ES), and Random Search, which facilitate efficient exploration and optimization of the hyperparameter space.

## Literature Review 📚
- **Order Book Dynamics:** Research in financial markets often highlights the importance of order book data in understanding market microstructure. Studies like "A High-Frequency Trade Model for Financial Regulation" (J. Gatheral, 2010) provide insights into how order flow and depth can influence price movements.
- **Auction Theory and Market Closing Prices:** The work of K. G. Nyborg (2017), "[Auctions for Securities](#)" delves into how auctions contribute to price discovery at market close, relevant for our model’s focus on closing auction data.
- **Predictive Modeling in Finance:** Significant literature, including "Stock Market Forecasting Using Machine Learning Algorithms" (S. Kumar, 2013), discusses various approaches to predictive modeling, from traditional statistical models to more recent machine learning techniques.

## Methodology 🧠
### Data Collection
### Order Book 📖

An order book is a fundamental component in financial markets, representing a real-time, continuously updated record of buy and sell orders for a specific financial instrument. Typically, an order book is maintained by an exchange (such as Nasdaq) and plays a critical role in the price discovery process. Here’s a more detailed breakdown:

#### Structure 🏗️
The order book lists various buy orders (bids) and sell orders (asks) for an asset. Each entry typically includes the price at which a buyer or seller is willing to transact and the quantity of the asset they wish to buy or sell at that price. The order book is organized in a manner where the highest bidding price is matched with the lowest asking price.

#### Types of Orders 📑
- **Limit Orders**: These are orders to buy or sell a stock at a specified price or better. They are placed in the order book until they are filled or canceled.
- **Market Orders**: Orders to buy or sell immediately at the best available current price. They do not enter the order book as they are executed instantly by matching with the best available opposite order.

#### Functions 🔍
- **Price Discovery**: The interaction of buy and sell orders in an order book helps establish the fair market price of a stock.
- **Liquidity**: A dense order book, with lots of buy and sell orders at various prices, generally indicates high liquidity, allowing large volumes of trades to occur with minimal impact on the stock's price.
- **Market Depth**: The order book displays the market depth, which is an indicator of the quantity available for trading closer to the bid and ask prices. A deeper market can handle larger orders without a significant impact on the price.

### Closing Auction 🔔

The closing auction is a mechanism used by stock exchanges to determine the official closing prices of stocks. This process typically occurs at the end of the trading day and is especially significant because many derivatives and index funds use these prices for valuations. Here’s how it works:

#### Process 🔄
1. **Order Collection**: Exchanges begin by collecting orders specifically meant for the auction during a period leading up to the close. These orders might include market-on-close (MOC) or limit-on-close (LOC) orders, which are intended to execute at the closing price.
2. **Price Determination**: The closing price is determined through a process that balances buy and sell orders to maximize the volume of shares that can be executed. The price at which this equilibrium is achieved becomes the official closing price.
3. **Execution**: At the closing price, all orders collected for the closing auction are executed. This often results in a significant volume of trades happening at one price point at the end of the trading session.

#### Importance 🌟
- **Fair and Transparent Pricing**: The closing auction helps mitigate price manipulation and volatility by aggregating trades at a single price point, reflecting a consensus value as determined by the market participants.
- **Benchmarking and Valuation**: Since the closing price is used for the calculation of index values and for performance benchmarking across various funds, its accuracy and stability are crucial.

Both the order book and the closing auction play vital roles in the functioning of modern financial markets, providing the structure and processes needed for orderly trading, price determination, and liquidity management.

### Educational Videos 🎥

For those who wish to deepen their understanding of the topics discussed above, here are some recommended video tutorials that provide clear and detailed explanations:

#### The Order Book 📚
Explore the intricacies of the order book and its role in financial markets through this insightful video:
- [Understanding the Order Book](https://youtu.be/_0KVAfy49h0?si=lj0uAerDv-tsujm1)

#### Market Mechanics and Hedge Funds 📉
Learn how hedge funds exploit market mechanics to their advantage, offering a unique glimpse into professional trading strategies:
- [How Hedge Funds Exploit Market Mechanics](https://youtu.be/LPGQL4MphBo?si=gGhdogcv3Ou6q4Q7)

These resources are excellent for both novices and experienced traders looking to enhance their knowledge of market dynamics and trading mechanisms.

### Data Processing
- **Feature Engineering:** Create features that reflect market sentiment, liquidity, and trading intensity during the last ten minutes of trading.
- **Normalization:** Standardize data to handle outliers and scale differences.

### Model Development
- **Predictive Model:** Utilize machine learning techniques such as Random Forests, Gradient Boosting Machines (GBM), and Neural Networks to predict closing prices.
- **Integration of Data Sources:** Develop a methodology to seamlessly integrate order book and auction data for holistic analysis.

## Evaluation 📏

### Submission Evaluation
Submissions are evaluated on the Mean Absolute Error (MAE) between the predicted return and the observed target. The formula is given by:

MAE = \frac{1}{n} \sum_{i=1}^n |y_i - x_i|

Where:
- `n` is the total number of data points.
- `y_i` is the predicted value for data point `i`.
- `x_i` is the observed value for data point `i`.

### Code Requirements 🛠️

Submissions to this competition must be made through Notebooks.

- **CPU Notebook:** <= 9 hours run-time
- **GPU Notebook:** <= 9 hours run-time
- **Internet access:** disabled

### Citation 📖
Tom Forbes, John Macgillivray, Matteo Pietrobon, Sohier Dane, Maggie Demkin. (2023). [Optiver - Trading at the Close](https://kaggle.com/competitions/optiver-trading-at-the-close).

### Dataset Description 🗃️
This dataset contains historic data for the daily ten-minute closing auction on the NASDAQ stock exchange. Your challenge is to predict the future price movements of stocks relative to the price future price movement of a synthetic index composed of NASDAQ-listed stocks. 

**Files:**
- **[train/test].csv:** The auction data. The test data will be delivered by the API.
  - `stock_id`: A unique identifier for the stock. Not all stock IDs exist in every time bucket.
  - `date_id`: A unique identifier for the date. Date IDs are sequential & consistent across all stocks.
  - `imbalance_size`: The amount unmatched at the current reference price (in USD).
  - `imbalance_buy_sell_flag`: An indicator reflecting the direction of auction imbalance.
    - buy-side imbalance; 1
    - sell-side imbalance; -1
    - no imbalance; 0
  - `reference_price`: The price at which paired shares are maximized, the imbalance is minimized and the distance from the bid-ask midpoint is minimized.
  - `matched_size`: The amount that can be matched at the current reference price (in USD).
  - `far_price`, `near_price`, `[bid/ask]_price`, `[bid/ask]_size`: Various pricing and size indicators.
  - `wap`: The weighted average price in the non-auction book.
  - `seconds_in_bucket`: The number of seconds elapsed since the beginning of the day's closing auction, always starting from 0.
  - `target`: The 60 second future move in the wap of the stock, less the 60 second future move of the synthetic index. Only provided for the train set.

**Additional Files:**
- `sample_submission`: A valid sample submission, delivered by the API.
- `revealed_targets`, `public_timeseries_testing_util.py`, `example_test_files/`, `optiver2023/`: Various utilities and example files to assist with API integration and testing.

For more details and to access the data, visit the [Kaggle competition dataset page](https://www.kaggle.com/competitions/optiver-trading-at-the-close/data). 📈🔍

## Results and Discussion 🔍
The developed model's ability to predict closing prices with a minimized MAE indicates its effectiveness in capturing the essential dynamics of the Nasdaq market. The identification of key features from the order book and auction data that most significantly impact price movements offers insights into the critical factors driving last-minute price changes.

## Conclusion 🎓
The Nasdaq Closing Price Prediction Challenge encapsulates the complexity of financial market predictions while showcasing the potential of advanced analytics in real-time trading environments. The project not only enhances understanding of market dynamics but also opens avenues for developing automated trading strategies that can operate efficiently in the frenetic closing moments of stock trading. The insights gained here extend beyond mere price prediction, suggesting broader applications in market theory and financial regulation.

---

Feel free to reach out at [adityasaxena@g.harvard.edu](mailto:adityasaxena@g.harvard.edu) for more insights or potential collaboration! 🤝 Happy trading and analyzing! 📊🚀

### PS: Helpful Resources
 - https://github.com/hyperopt/hyperopt
 - https://github.com/autonomio/talos
 - https://towardsdatascience.com/a-guide-to-an-efficient-way-to-build-neural-network-architectures-part-i-hyper-parameter-8129009f131b

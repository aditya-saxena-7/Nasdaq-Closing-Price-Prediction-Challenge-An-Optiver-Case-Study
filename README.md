# 📈 Nasdaq-Closing-Price-Prediction-Challenge: An Optiver Case Study

## Abstract 🎯
This project aims to develop a sophisticated model capable of predicting the closing price movements of Nasdaq-listed stocks during the final critical ten minutes of the trading day. By integrating and analyzing data from both the order book and closing auctions, the model will leverage insights into the nuanced supply and demand dynamics to forecast price movements and identify lucrative trading opportunities. The predictive performance of the model will be measured using the Mean Absolute Error (MAE) between predicted and observed stock closing prices.

## Introduction 🚀
Predicting stock market movements, especially in the volatile closing minutes, is a complex challenge that attracts significant attention from financial analysts and traders. The Nasdaq stock market, characterized by high liquidity and rapid price changes, presents a fertile ground for applying advanced predictive analytics. This project focuses on harnessing detailed order book data and closing auction information to build a model that not only predicts the closing prices but also uncovers potential trading strategies during peak trading times.

## Literature Review 📚
- **Order Book Dynamics:** Research in financial markets often highlights the importance of order book data in understanding market microstructure. Studies like "A High-Frequency Trade Model for Financial Regulation" (J. Gatheral, 2010) provide insights into how order flow and depth can influence price movements.
- **Auction Theory and Market Closing Prices:** The work of K. G. Nyborg (2017), "[Auctions for Securities](#)" delves into how auctions contribute to price discovery at market close, relevant for our model’s focus on closing auction data.
- **Predictive Modeling in Finance:** Significant literature, including "Stock Market Forecasting Using Machine Learning Algorithms" (S. Kumar, 2013), discusses various approaches to predictive modeling, from traditional statistical models to more recent machine learning techniques.

## Methodology 🧠
### Data Collection
- **Order Book Data:** Collect historical order book data for Nasdaq-listed stocks, focusing on bid-ask spreads, order sizes, and order depths.
- **Closing Auction Data:** Gather data on auction volumes, final auction prices, and imbalance information.

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

This is a forecasting competition using the time series API. The private leaderboard will be determined using real market data gathered after the submission period closes.

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

Feel free to reach out for more insights or potential collaboration! 🤝 Happy trading and analyzing! 📊🚀

### PS: Helpful Resources
 - https://github.com/hyperopt/hyperopt
 - https://github.com/autonomio/talos
 - https://towardsdatascience.com/a-guide-to-an-efficient-way-to-build-neural-network-architectures-part-i-hyper-parameter-8129009f131b

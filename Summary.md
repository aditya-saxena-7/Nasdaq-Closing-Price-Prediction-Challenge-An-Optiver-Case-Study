## 📈 Nasdaq-Closing-Price-Prediction-Challenge: An Optiver Case Study
---

### 1. Abstract 🎯
---

This project aims to develop a sophisticated model capable of predicting the closing price movements of Nasdaq-listed stocks during the critical final ten minutes of the trading day. 

By integrating and analyzing data from both the order book and closing auctions, the model leverages insights into nuanced supply and demand dynamics to forecast price movements and identify lucrative trading opportunities.

The predictive performance of the model is measured using the Mean Absolute Error (MAE) between predicted and observed stock closing prices.

### 2. Introduction 🚀
---

Predicting stock market movements, especially in the volatile closing minutes, is a complex challenge that attracts significant attention from financial analysts and traders.  

This project focuses on harnessing detailed order book data and closing auction information to build a model that not only predicts the closing prices but also uncovers potential trading strategies during peak trading times. To optimize the model’s parameters, we employ Optuna, a sophisticated hyperparameter optimization framework. 

### 3. Data Collection
---

#### 3.1 Order Book 📖

An order book is a fundamental component in financial markets, representing a real-time, continuously updated record of buy and sell orders for a specific financial instrument. 

Typically, an order book is maintained by an exchange (such as Nasdaq) and plays a critical role in the price discovery process. Here’s a more detailed breakdown:

#### 3.2 Structure 🏗️

The order book lists various buy orders (bids) and sell orders (asks) for an asset. Each entry typically includes the price at which a buyer or seller is willing to transact and the quantity of the asset they wish to buy or sell at that price. 

The order book is organized in a manner where the highest bidding price is matched with the lowest asking price.

#### 3.3 Types of Orders 📑

- **Limit Orders**: These are orders to buy or sell a stock at a specified price or better. They are placed in the order book until they are filled or canceled.
  
- **Market Orders**: Orders to buy or sell immediately at the best available current price. They do not enter the order book as they are executed instantly by matching with the best available opposite order.

#### 3.4 Functions 🔍

- **Price Discovery**: The interaction of buy and sell orders in an order book helps establish the fair market price of a stock.
  
- **Liquidity**: A dense order book, with lots of buy and sell orders at various prices, generally indicates high liquidity, allowing large volumes of trades to occur with minimal impact on the stock's price.
  
- **Market Depth**: The order book displays the market depth, which is an indicator of the quantity available for trading closer to the bid and ask prices. A deeper market can handle larger orders without a significant impact on the price.

#### 3.4 Closing Auction 🔔

The closing auction is a mechanism used by stock exchanges to determine the official closing prices of stocks. This process typically occurs at the end of the trading day and is especially significant because many derivatives and index funds use these prices for valuations. Here’s how it works:

#### 3.6 Process 🔄

1. **Order Collection**: Exchanges begin by collecting orders specifically meant for the auction during a period leading up to the close. These orders might include market-on-close (MOC) or limit-on-close (LOC) orders, which are intended to execute at the closing price.
   
2. **Price Determination**: The closing price is determined through a process that balances buy and sell orders to maximize the volume of shares that can be executed. The price at which this equilibrium is achieved becomes the official closing price.
   
3. **Execution**: At the closing price, all orders collected for the closing auction are executed. This often results in a significant volume of trades happening at one price point at the end of the trading session.

### 4. Dataset Description 🗃️
---

This dataset contains historic data for the daily ten-minute closing auction on the NASDAQ stock exchange.

**stock_id:**
- **Description:** A unique identifier for each stock.
- **Context:** Not every stock appears in every time bucket (a specific, often small, period of time during trading), making this identifier crucial for tracking the performance and data specific to each stock across different periods.
  
**date_id:**
- **Description:** A unique identifier for the date on which the trading data was recorded. These IDs are sequential and consistent across all stocks.
- **Context:** Allows the model to differentiate data across different trading days and to identify trends or patterns over time.

**imbalance_size:**
- **Description:** Represents the volume of shares that remain unmatched at the current reference price, expressed in USD.
- **Context:** A critical measure in understanding supply and demand dynamics at the closing auction, influencing the model's ability to predict price movements based on existing imbalances.

**imbalance_buy_sell_flag:**
- **Description:** A categorical flag indicating the direction of the auction imbalance:
1 for a buy-side imbalance (more demand than supply)
-1 for a sell-side imbalance (more supply than demand)
0 for no imbalance
- **Context:** This indicator helps in predicting whether the price is likely to rise or fall at the close, based on whether there is excess buying pressure or selling pressure.

**matched_size:**
- **Description:** The total amount in USD that can be matched at the current reference price.
- **Context:** Indicates the volume of trades that can be executed without affecting the market price too significantly, crucial for understanding market liquidity.

**far_price, near_price, [bid/ask]_price, [bid/ask]_size:**

- **Description:** These are various price points and quantities in the order book.
  
Far price and near price likely relate to the prices available at further and closer points in the order book.

[bid/ask]_price are the highest buy and lowest sell prices respectively.

[bid/ask]_size are the volumes available at these prices.

- **Context: These metrics provide detailed insights into the order book's depth and the distribution of buy and sell orders around the reference price, informing predictions on price movement pressures.

**wap (Weighted Average Price):**

- **Description:** Calculated over a specific time frame within the non-auction book, it's a price that reflects the average price at which stocks are traded, weighted by volume.
- **Context:** WAP is used to gauge the average trading price over a period, often used in financial models to understand market trends and to normalize the impact of large trades on simple average price calculations.

**target:**

The target variable you're predicting is the difference between the 60-second future movement in a stock's Weighted Average Price (WAP) and the 60-second future movement of a synthetic index.
What Does This Mean?

Weighted Average Price (WAP): This is like an average price at which a stock trades, but it's "weighted" based on the number of shares traded at each price. If more shares are traded at a particular price, that price has more influence on the WAP.

Synthetic Index: Think of this as a benchmark or reference point representing the overall market's movement.

### **Quantitative Example:**

**Step 1: Initial Conditions at 11:59:00 AM**

- **Stock WAP (Weighted Average Price)**: The WAP for a particular stock at 11:59:00 AM is **$100.00**.
- **Synthetic Index**: The WAP for a synthetic index, representing the overall market, at 11:59:00 AM is **$102.00**.

**Step 2: Observations at 12:00:00 PM (60 Seconds Later)**

- **Stock WAP**: At 12:00:00 PM, the WAP for the stock has increased to **$101.50**.
- **Synthetic Index**: At 12:00:00 PM, the WAP for the synthetic index has increased to **$102.30**.

**Step 3: Calculate the Movements**

- **Stock WAP Movement**: 
   - Initial WAP: $100.00
   - Final WAP: $101.50
   - **Movement**: $101.50 - $100.00 = **$1.50**

- **Synthetic Index Movement**:
   - Initial WAP: $102.00
   - Final WAP: $102.30
   - **Movement**: $102.30 - $102.00 = **$0.30**

**Step 4: Calculate the Target Variable**

- **Target Variable**: This is the difference between the stock's movement and the synthetic index's movement.
   - **Target**: $1.50 (Stock Movement) - $0.30 (Index Movement) = **$1.20**

### **Interpretation:**

- **Positive Target ($1.20)**: In this example, the stock's price increased by $1.50 over the 60 seconds, while the market index only increased by $0.30. The target variable of $1.20 indicates that the stock outperformed the market by $1.20 in this short period.

- **Usefulness**: This information tells a trader that, in this specific instance, the stock showed stronger growth than the general market, making it a potentially attractive buy if the trend is expected to continue.

### **Effect of the Target Variable on Model Performance:**

- The model is trained to predict this target variable. If it can accurately forecast whether a stock will outperform or underperform the market in the next 60 seconds, traders can use this information to make quick, informed decisions, such as buying, selling, or holding the stock.
  
- A positive target suggests a potential buying opportunity, while a negative target (had the stock moved less than the index) might indicate a selling opportunity.

This target variable is crucial because it quantifies the stock's performance relative to the market, providing actionable insights for trading decisions.

### 5. Model Development
---

- **Predictive Model:** Utilize machine learning techniques like Random Forests and LightGBM to predict closing prices.
  
- **Integration of Data Sources:** Develop a methodology to seamlessly integrate order book and auction data for holistic analysis.

### 6. Model Initialization
---

lgbm_model = lgbm.LGBMRegressor(objective='mae', n_estimators=500, random_state=1234)

**(Study Math of Random Forest and LightGBM)**

**LGBMRegressor:**

This class implements the LightGBM regressor. A regressor predicts continuous values, which is appropriate for predicting stock prices as continuous numerical data.

#### 6.1 **Parameters:**

- **objective='mae':** Specifies the loss function to be minimized in the learning process. Here, 'mae' stands for Mean Absolute Error, which aligns with the project’s evaluation criteria. 

It measures the average magnitude of errors in a set of predictions, without considering their direction (i.e., whether they are over or underestimates).

- **n_estimators=500:** This defines the number of boosting stages the model has to go through. More trees can lead to a more accurate model but can also cause overfitting if not handled correctly. In this context, 500 trees are chosen to balance between bias and variance.

- **random_state=1234:** This parameter ensures reproducibility of the model’s results by providing a fixed seed for the random number generator, which influences aspects of model training like the selection of features at each split.

#### 6.2 Feature Engineering

Add 3 new features related imbalance_ratio, bid-size and ask-size.

1. **New Feature: imbalance_ratio**

- **Definition:** It is calculated as the division of imbalance_size by matched_size.
  
imbalance_size: This could represent the volume of shares that remain unmatched at the current reference price.

- **matched_size:** This typically indicates the volume of shares that can be matched at the current reference price.

**Significance of the imbalance_ratio Feature**

- **Insight into Market Dynamics:** This ratio provides insight into the relative size of unmatched orders compared to matched orders at the reference price, potentially signaling market pressure (either buying or selling pressure) that isn't fully resolved by current order matches.
  
- **Indicator of Market Sentiment:** A high imbalance_ratio might suggest a strong imbalance in buy or sell orders that could affect the stock price shortly, especially during the closing auction when liquidity and volatility are high.

- **Formula:** Imbalance Ratio = Imbalance Size / Matched Size
- **Imbalance Size:** The total volume of orders that haven't been matched (either buy or sell).
- **Matched Size:** The total volume of orders that have been successfully matched.

Example:
- Imbalance Size: $500,000 (unmatched orders)
- Matched Size: $1,000,000 (matched orders)
- Imbalance Ratio: $500,000 / $1,000,000 = 0.5

**Quantitative Interpretation:**

- **What It Tells Us:** An imbalance ratio of 0.5 indicates that for every dollar's worth of orders that got matched, there’s 50 cents worth of unmatched orders. This suggests a significant supply-demand imbalance, which might lead to price changes as the market tries to match these orders.

- **Impact on Prediction:** A higher imbalance ratio might suggest that the stock price could move sharply soon, as the market attempts to balance the excess demand or supply. If there's a large number of unmatched buy orders, for instance, the stock price may rise as buyers are willing to pay more to get their orders filled.

2. **imbl_size1 (Normalized Difference Between Bid Size and Ask Size)**

- **Definition:** The normalized difference between bid_size and ask_size.
- **Formula:** (df['bid_size'] - df['ask_size']) / (df['bid_size'] + df['ask_size'])
- **Purpose:** Captures the net order flow direction, indicating whether buying or selling pressure is dominant.

**Effect on Accuracy:**

- **Order Flow Direction:** This feature captures the net direction of order flow. A higher value suggests dominant buying pressure, while a lower value indicates selling pressure. This helps the model understand whether the market is more inclined towards buying or selling, which directly impacts price predictions.

- **Enhanced Sensitivity:** By normalizing the difference between bid and ask sizes, the feature accounts for the relative strength of buy and sell orders, improving the model’s sensitivity to subtle shifts in market dynamics.

- **Formula:** Imbl_size1 = (Bid Size - Ask Size) / (Bid Size + Ask Size)
- **Bid Size:** The total volume of buy orders at the current bid price.
- **Ask Size:** The total volume of sell orders at the current ask price.

Example:
- Bid Size: 10,000 shares
- Ask Size: 8,000 shares
- Imbl_size1: (10,000 - 8,000) / (10,000 + 8,000) = 2,000 / 18,000 ≈ 0.11

**Quantitative Interpretation:**

- **What It Tells Us:** An imbl_size1 of 0.11 indicates that there’s slightly more buying interest (bid size) than selling interest (ask size). This suggests that there might be upward pressure on the stock price because more people are looking to buy than sell.

- **Impact on Prediction:** When the bid size is larger than the ask size, the stock price might increase as buyers are more eager to purchase, potentially driving up the price. Conversely, if imbl_size1 were negative, it would suggest more selling pressure, possibly leading to a price drop.

3. **imbl_size2 (Normalized Difference Between Imbalance Size and Matched Size)**

- **Definition:** The normalized difference between imbalance_size and matched_size.
- **Formula:** (df['imbalance_size'] - df['matched_size']) / (df['imbalance_size'] + df['matched_size'])
- **Purpose:** Similar to imbalance_ratio but focuses on the relative difference rather than the ratio, providing another perspective on market liquidity and order imbalance.

**Effect on Accuracy:**

- **Relative Liquidity and Imbalance:** This feature adds another layer of insight by focusing on the difference between unmatched orders (imbalance size) and those that can be matched (matched size). It highlights how much of the order book remains unresolved, which can be crucial in predicting price changes.

- **Complementary Perspective:** While imbalance_ratio gives a ratio-based view, imbl_size2 provides a difference-based perspective, offering a complementary approach to understanding market liquidity and pressure. This dual perspective allows the model to capture a broader range of market conditions, leading to more accurate predictions.

- **Formula: Imbl_size2** = (Imbalance Size - Matched Size) / (Imbalance Size + Matched Size)
- **Imbalance Size:** Volume of unmatched orders.
- **Matched Size:** Volume of matched orders.

Example:
- Imbalance Size: $500,000 (unmatched orders)
- Matched Size: $1,000,000 (matched orders)
- Imbl_size2: ($500,000 - $1,000,000) / ($500,000 + $1,000,000) = -$500,000 / $1,500,000 ≈ -0.33

**Quantitative Interpretation:**

- **What It Tells Us:** An imbl_size2 of -0.33 suggests that the matched orders significantly outweigh the unmatched ones. This might imply that the current market is effectively absorbing the available orders, leading to less price volatility.

- **Impact on Prediction:** A negative imbl_size2 might indicate that the market is relatively stable, with sufficient liquidity to handle current orders without causing large price swings. On the other hand, a positive imbl_size2 would suggest more unmatched orders, indicating potential future price movements due to unresolved supply or demand.

**Summary in Layman's Terms:**

- **Imbalance Ratio:** Think of it like the number of customers waiting in line (unmatched orders) versus the number already served (matched orders). If too many are waiting, the price (ticket) might go up or down to clear the line quickly.

- **Imbl_size1:** This tells you if more people are buying or selling right now. If more are buying, prices might go up; if more are selling, prices might drop.

- **Imbl_size2:** This shows whether the market is calm or under pressure. If the market can handle the current buying and selling (matched orders are higher), prices are stable. If not (unmatched orders are higher), expect price swings.

### 7. Results and Discussion 🔍
---

● Developed a model predicting Nasdaq stock closing prices using order book and auction data, achieving 3.3% Mean Absolute Error.

● Engineered features including imbalance ratios and used Random Forest and LightGBM, improving compute efficiency by 9%

The developed model's ability to predict closing prices with a minimized MAE indicates its effectiveness in capturing the essential dynamics of the Nasdaq market. 

The identification of key features from the order book and auction data that most significantly impact price movements offers insights into the critical factors driving last-minute price changes.

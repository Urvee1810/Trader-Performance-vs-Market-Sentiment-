# Trader-Performance-vs-Market-Sentiment-

#Data Science Intern Assignment - Round 0: Trader Performance vs Market Sentiment

## Objective
This project analyzes how Bitcoin market sentiment (Fear vs. Greed) relates to trader behavior and overall performance on the Hyperliquid platform. The ultimate goal is to uncover actionable behavioral patterns that can inform smarter, automated trading strategies and risk management engines.

---

## Setup & How to Run

### Prerequisites
To run this analysis locally, ensure you have Python installed along with the following libraries:
* `pandas`
* `numpy`
* `matplotlib`
* `seaborn`
* `scikit-learn` (for the bonus K-Means clustering)

### Execution Steps
1. Clone this repository to your local machine.
2. Ensure the two raw data files (`sentiment.csv` and `traders.csv`) are placed in the same directory as the notebook.
3. Open `PrimeTradeAI.ipynb` using Jupyter Notebook, JupyterLab, or Google Colab.
4. Click **"Run All"** to execute the cells sequentially. The code is structured to automatically clean the data, generate the metrics, and output the visualizations inline.

---

## Methodology

1. **Data Cleaning & Alignment:** Loaded the historical transaction logs and daily Bitcoin sentiment scores. Handled timestamp conversions by normalizing Hyperliquid execution times (UTC) to a daily level, allowing for a clean left-join with the sentiment dataset. Dropped trades occurring on days with missing sentiment data to ensure accurate comparisons.
2. **Feature Engineering:** Aggregated raw transaction-level data into daily summaries per account. Created new performance and behavioral metrics, including: Daily PnL, Win Rate, Average Trade Size, Trade Frequency (trades per day), and Long/Short Ratio.
3. **Segmentation:** Grouped traders into distinct categories based on their lifetime behavior across the dataset, specifically analyzing:
    * Frequent vs. Infrequent Traders
    * Consistent Winners (>45% win rate) vs. Inconsistent Traders
    * High Value (Whales) vs. Low Value Traders
4. **Machine Learning (Bonus):** Applied a K-Means clustering algorithm using scaled lifetime metrics to automatically group traders into three distinct behavioral archetypes.

---

## Key Insights

### 1. Performance on Fear vs. Greed Days
* **Fear is Profitable:** Traders perform significantly better during "Fear" market conditions, achieving their highest average win rate (41.5%) and highest average daily PnL ($209,000).
* **Controlled Drawdowns:** Risk is managed better during Fear days. Average losses on red days are relatively contained.
* **Greed Causes Catastrophe:** During "Greed" days, average profits are cut in half. Furthermore, the severity of losing days is massive, with average daily drawdowns exceeding -$327,000. 

### 2. Behavioral Shifts Based on Sentiment
* **Frequency Skyrockets in Fear:** On Fear days, traders execute nearly four times as many trades (4,183 per day) compared to Greed days (1,134 per day), pointing to heavy scalping or active risk management.
* **Blind Buying in Greed:** During "Extreme Greed," the Long/Short ratio explodes, indicating traders heavily bias toward Longs and ignore downside risk. Fear brings balance, dropping the L/S ratio to 0.96 (a nearly equal hedge of buying and selling).

### 3. Trader Segmentation Performance
* **Active Traders Dominate:** "Frequent Traders" perform significantly better than "Infrequent Traders." When the market hits "Extreme Greed," infrequent traders average a net loss, while frequent traders stay profitable.
* **Whale Traps:** "High Value" traders dominate during Fear but actually lose money on average during Extreme Greed, suggesting overconfidence and massive liquidations at market peaks.

---

## Strategy Recommendations

Based on the data-driven insights above, here are two actionable rules of thumb to optimize trading systems:

* **Strategy 1 (Risk Management):** During Extreme Greed days, reduce maximum position sizes for High Value traders to prevent massive liquidations; increase trade frequency alerts only for Infrequent traders to stop them from holding onto losing positions too long.
* **Strategy 2 (Profit Maximization):** During Fear days, increase capital allocation limits for High Value traders to maximize their massive profit edge; enforce a balanced Long/Short ratio requirement for Inconsistent traders to safely capture high volatility profits.

---

## Bonus: Behavioral Archetype Clustering
Using a K-Means clustering algorithm on the scaled lifetime data, three distinct trader archetypes were identified:

1. **The Retail Scalpers (Cluster 0):** Execute massive volumes of trades (>8,000) with the highest win rate (46%), but utilize the smallest average position sizes ($2,800).
2. **The High-Rolling Whales (Cluster 1):** Execute moderate trade volumes but dominate with massive position sizes (averaging >$16,000 per trade) and maintain a solid 35% win rate.
3. **The Casual Amateurs (Cluster 2):** Struggle the most, executing the fewest trades with a highly unprofitable 22% win rate.

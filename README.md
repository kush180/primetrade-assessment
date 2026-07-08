# Primetrade.ai Data Science Assessment: Trader Performance vs. Market Sentiment

**Applicant:** Kushagra Verma  
**Roll Number:** 231020430  

This repository contains the complete execution of the Primetrade.ai Data Science Intern Round-0 assignment. The analysis investigates how market sentiment (Bitcoin Fear/Greed Index) dictates trader behavior and performance on the Hyperliquid platform.

---

## 🛠️ Setup & How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/kush180/primetrade-assessment.git
   cd primetrade-assessment
   ```

2. **Install dependencies:**
   Ensure you have Python 3.8+ installed, then run:
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the Analysis:**
   Open the Jupyter Notebook to view the code, outputs, and interactive visualizations:
   ```bash
   jupyter notebook notebook.ipynb
   ```
   *Note: Ensure the `datasets` folder containing both `historical_data.csv` and `fear_greed_index.csv` remains in the root directory for the notebook to execute properly.*

---

## 📊 Executive Summary & Write-Up

### Methodology
To ensure data integrity and precise timezone alignment, the following processing pipeline was executed:
* **Timezone Synchronization:** The historical dataset's local timestamps (IST) were programmatically converted back to the global UTC standard (subtracting 5h 30m). This ensured accurate merging with the daily-resetting (UTC) Bitcoin Sentiment Index.
* **Feature Engineering:** Daily performance metrics were aggregated per account, including `daily_pnl` (sum of closed PnL), `trade_count`, `win_rate`, `avg_trade_size`, and `long_short_ratio`.
* **Outlier Mitigation:** Due to the heavy-tailed nature of crypto trading volume, **median** values were utilized over standard means for baseline comparisons to accurately reflect typical human behavior.
* **Segmentation Logic:** Accounts were segmented into "Whales" vs. "Retail" based on the global median trade size ($1,947), and into "Consistent" vs. "Inconsistent" based on median win rate (28.57%) and a minimum threshold of 50 trades.

### Key Insights
1. **Extreme Sentiment Drives Reactive Volatility:** Trading activity spikes violently during market distress. Extreme Fear days average 97 trades per day across accounts, indicating traders become highly reactive during panic events.
2. **Whales Capitalize on Market Extremes:** High-volume accounts generate their absolute best relative performance at the poles of market sentiment. Whales posted peak median profitability during Extreme Fear ($1,594) and Extreme Greed ($769), successfully acting as liquidity providers or momentum riders when retail traders panic.
3. **Skill Outpaces Market Conditions:** The "Consistent Winner" segment heavily outperforms inconsistent traders across *all* sentiment conditions, maintaining a 35-40% win rate. The PnL performance gap is widest during extreme market days, proving that structural risk management dictates profitability more than sentiment alone.

### Strategy Recommendations

#### STRATEGY 1: For Whales & High-Volume Traders
* **During Extreme Greed Markets (Index > 75):** Increase position sizes to capitalize on bullish momentum and market optimism. Begin scaling out of winning positions as sentiment approaches peak exhaustion (90+).
* **During Extreme Fear Markets (Index < 20):** Treat this as a prime opportunity for contrarian setups. Deploy capital gradually into oversold assets using strict stop-losses (2-3% below entry) and conservative leverage (max 2-3x) to navigate downside risk.
* **During Regular Fear Markets (Index 20-45):** Reduce position sizes by 40-50% and lower leverage significantly (1-2x max) to prioritize capital preservation.

#### STRATEGY 2: For Retail & Low-Volume Traders
* **During Greed Markets (Index 55-75):** Increase trading frequency with a slight long-bias. This is the optimal trend environment for retail traders to scale in on short-term corrections.
* **During Fear Markets (Index < 45):** Reduce trading frequency significantly, slash position sizes by 50-75%, and avoid taking on leverage entirely. Do not attempt to catch falling knives.
* **During Extreme Fear Markets (Index < 20):** Consider staying heavily in cash or stablecoins. Limit operations to only the highest quality setups with incredibly tight trailing stop-losses (1-2%).
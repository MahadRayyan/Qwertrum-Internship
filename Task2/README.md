# 📊 Super Mart Sales Analysis & AAPL Time Series — Qwertrum Internship Tasks

Two end-to-end data analytics tasks completed during the Qwertrum internship — a Power BI sales dashboard with business intelligence reporting on Super Mart's 3-year sales data, and a professional time series analysis of Apple (AAPL) stock across 1,377 trading days from 2020 to 2025.

---

## ⚡ Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Power BI
- CSV (World Stock Prices Dataset — 310,122 rows, 62 tickers)

---

## 📁 Task 1 — Super Mart Sales Dashboard (Power BI)

### 🚀 Features

- Built an interactive **Power BI dashboard** summarizing Super Mart's sales performance across 2023, 2024, and 2025
- KPI cards tracking **Most Selling Product** (Chair), **Total Revenue** (1.26M), **Total Customers** (1,200), and **Coupons Redeemed** (891)
- **Units Sold by Product** bar chart — ranking Chair, Printer, Laptop, Desk, and Tablet by sales volume
- **Payment Method Breakdown** donut — Online, Cash, Credit Card, Debit Card, and Gift Card distribution
- **Customer Acquisition by Source** donut — Instagram, Email, Google, Facebook, and Referral channel share
- **Revenue by Marketing Channel** stacked bar — comparing revenue contribution per channel broken down by payment method
- **Best Sales Days** bar chart — revenue by day of week, revealing Monday and Tuesday as top performers
- **Yearly Revenue Trend** bar chart — tracking growth from 2023 through 2025
- Year-based **bookmark navigation** (2023 / 2024 / 2025) for dynamic cross-year filtering

### 🧠 Business Questions Answered

**Q1 — Which marketing channel should Super Mart invest in most?**
Instagram leads all channels in both revenue and customer acquisition share, followed closely by Email and Google. Facebook and Referral significantly underperform. Recommendation: prioritize Instagram and Email as primary channels; restructure Facebook and Referral campaigns before further budget allocation.

**Q2 — How has revenue trended over three years?**
Revenue peaked in 2024 and declined in 2025 despite 1.26M in total three-year revenue. The 2025 dip warrants a root cause analysis — reduced marketing spend, increased competition, or shifting customer behavior. The 891 coupons redeemed should be evaluated to determine if discount strategies are retaining customers or only attracting one-time buyers.

**Q3 — Are there structural gaps in weekly sales performance?**
Monday and Tuesday dominate sales, while Saturday and Sunday show the lowest activity. This weekday-heavy pattern aligns with the product mix (office equipment — Chair, Printer, Laptop, Desk, Tablet), suggesting a professional buyer base. Recommendation: design weekend-specific promotions targeting home-use scenarios to activate the dormant weekend segment.

---

## 📁 Task 2 — AAPL Time Series Analysis (Python)

### 🚀 Features

- Loads the **World Stock Prices Dataset** (310,122 rows, 62 tickers) and filters 1,377 Apple (AAPL) trading days from January 2020 to July 2025
- Cleans and normalizes UTC timestamps, removes duplicates, and sets `Date` as the index
- Computes **7-Day and 30-Day Rolling Averages** to separate short-term momentum from long-term trend
- Calculates **daily percentage returns** and **Z-scores** for statistical anomaly detection
- Identifies peak price of **$259.02 (December 26, 2024)** and trough of **$54.85 (March 23, 2020)**
- Detects **25 anomalous trading days** using a |Z-score| > 2.8 threshold, flagging both spikes and drops with their exact percentage moves
- Produces three publication-quality dark-themed plots saved as PNG files:
  - **Plot 1** — Raw time series with annotated peak and trough markers
  - **Plot 2** — 7-Day vs 30-Day rolling averages overlaid on daily close
  - **Plot 3** — Anomaly detection chart with per-event percentage annotations
- Generates a full **insight report** covering trend, seasonality, peak/trough analysis, and anomaly interpretation

### 🧠 Key Findings

- **5-Year Return: 191.5%** — AAPL grew from ~$75 to $259.02 over the analysis window
- **March 2020 anomaly cluster** — 6 extreme events in 4 weeks during the COVID-19 crash, with single-day swings ranging from −12.86% to +11.98%
- **April 2025 tariff shock** — three consecutive drops (−9.25%, −7.29%, −8.47%) followed by a **+15.33% single-day rebound** on April 9 after tariff pause announcements — the largest single-day gain in the dataset
- **Notable mid-period spikes** — +8.90% in November 2022 (CPI inflation fears cooled) and +7.26% in June 2024 (Apple Intelligence AI announcement)
- Every major drawdown across the 5-year window was followed by a stronger recovery, with the 30-day rolling average consistently confirming the long-term bullish trend

### 🛠 Running Task 2

1. Download `World-Stock-Prices-Dataset.csv` from Kaggle and place it in the project directory

2. Install dependencies:

```
pip install pandas numpy matplotlib
```

3. Open the notebook:

```
jupyter notebook Task2_Time_Series_Analysis.ipynb
```

4. Run all cells — three plots are saved automatically as `plot1_raw_timeseries.png`, `plot2_rolling_averages.png`, and `plot3_anomalies.png`

---

## 📊 AAPL Summary Stats

| Metric | Value |
|---|---|
| Dataset rows (all tickers) | 310,122 |
| AAPL trading days analyzed | 1,377 |
| Date range | Jan 2, 2020 — Jul 3, 2025 |
| Trough price | $54.85 (Mar 23, 2020) |
| Peak price | $259.02 (Dec 26, 2024) |
| 5-Year return | 191.5% |
| Anomalies detected (Z > 2.8) | 25 events |


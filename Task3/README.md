# 📢 Marketing Campaign A/B Testing & SQL Order Analysis — Qwertrum Internship Tasks

Two analytics tasks completed during the Qwertrum internship — a full A/B testing analysis comparing Facebook vs AdWords advertising performance across 365 days of campaign data, and a 31-query SQL analysis of an e-commerce orders dataset covering filtering, aggregation, grouping, and KPI reporting.

---

## ⚡ Technologies

- Python
- Pandas
- Matplotlib
- Seaborn
- SciPy (`chi2_contingency`, `stats`)
- Statsmodels (`seasonal_decompose`, `coint`)
- NumPy
- MySQL
- CSV (marketing_campaign.csv — 365 rows, 17 columns)

---

## 📁 Task 3 — A/B Testing: Facebook vs AdWords (Python)

### Business Problem
A marketing agency ran two parallel ad campaigns throughout 2019 — one on Facebook and one on AdWords — and needed to determine which platform delivered better ROI in terms of clicks, conversions, and cost-effectiveness.

### 🚀 Features

- Loads **365 days of campaign data** (2019) with 17 columns covering views, clicks, conversions, cost, CTR, conversion rate, and CPC for both platforms
- Converts `Date` column from object to `datetime64` and generates descriptive statistics across both campaigns
- Plots **distribution histograms with KDE** for clicks and conversions on both platforms — confirming roughly symmetrical distributions with no extreme outliers
- Engineers **conversion category buckets** (< 6, 6–10, 10–15, > 15) for both platforms and compares daily frequency with a **grouped bar chart**
- Visualizes the **clicks vs conversions relationship** via scatter plots for both campaigns and computes correlation coefficients
- Runs a **Chi-Square test** on a 2×2 contingency table (converted vs not converted, Facebook vs AdWords) to statistically validate which platform drives more conversions
- Reports T-statistic and p-value to formally accept or reject the null hypothesis

### 🧠 Key Findings

**Clicks → Conversions Correlation**
- Facebook: correlation = **0.87** — strong positive relationship; more clicks reliably leads to more conversions
- AdWords: correlation = **0.45** — moderate relationship; clicks alone don't explain conversion performance, suggesting other factors at play

**Conversion Category Distribution**
- Facebook dominated the high-conversion days: 189 days in the 10–15 range, 47 days above 15, and only 1 day below 6
- AdWords never exceeded 10 conversions in a single day — 156 days below 6 conversions, 209 days in the 6–10 range

**Hypothesis Test Result**

| | Facebook | AdWords |
|---|---|---|
| Mean daily conversions | **11.74** | 5.98 |
| Chi-Square statistic | **1850.43** | — |
| p-value | **≈ 0.0** | — |
| Decision | **Reject H0** — Facebook significantly outperforms AdWords |

The p-value is essentially zero — far below the 0.05 significance threshold. The null hypothesis (no difference between platforms) is rejected. Facebook advertising generates statistically significantly more conversions than AdWords across the full year of data.

**Recommendation:** Reallocate budget toward Facebook as the primary performance channel. AdWords campaigns should be reviewed for targeting and creative optimization before further investment.

---

## 📁 Task 4 — SQL Order Analysis (MySQL)

### 🚀 Features

A 31-query SQL script covering the full analytical spectrum of an e-commerce `orders` table — from basic filtering to multi-level aggregation and business KPI reporting.

**Filtering & Selection (Q4–Q10)**
- Delivered orders, orders placed in 2024, high-value orders above $2,000
- Laptop orders with `Shipped` status, Credit/Debit Card payments
- Cancelled or Returned orders, date-range filtering for 2023

**Sorting (Q11–Q13)**
- Orders sorted by `TotalPrice` descending, by date (most recent first), and by product name then price

**Aggregation & KPIs (Q14–Q16)**
- Total order count, total revenue (`SUM`), average order value (`AVG`)

**GROUP BY Analysis (Q17–Q24)**
- Orders and revenue by `OrderStatus`, quantity sold per product, average order value by payment method
- Revenue and order count by year, revenue by product, monthly revenue (all years combined)
- Top 5 customers by total spend, cross-tab of payment method × order status

**HAVING Filters (Q27–Q30)**
- Products with total quantity sold above 500, payment methods with average order value above $1,050
- Monthly revenue for 2024 only, cancelled order revenue loss by product

**KPI Summary & Business Questions (Q31–Q34)**
- Overall KPI summary: total orders, total revenue, avg/min/max order value, total items sold
- Most popular product by quantity: **Chair (562 units)**
- Least popular product by quantity: **Phone (411 units)**
- Order status distribution with percentage share per status

### 🛠 Running the SQL Script

1. Import your `orders` table into a MySQL database

2. Open `task3.sql` in MySQL Workbench or any MySQL client

3. Run queries individually or as a full script — each query is independently executable with clear comments (`-- Q4`, `-- Q5`, etc.)

---

## 📁 Repository Structure

```
qwertrum-tasks/
│
├── AB_Testing__Marketing_Campaigns_.ipynb   # A/B testing analysis notebook
├── task3.sql                                # 31 SQL queries on orders dataset
├── marketing_campaign.csv                   # Campaign data (365 rows, 17 columns)
└── README.md
```


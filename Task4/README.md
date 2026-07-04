# 🛒 E-Commerce Business Analytics — Capstone Project (Qwertrum Internship)

A full-stack data analytics capstone project analyzing 10,000 e-commerce orders across 2,000 customers and 1,200 products. The project combines SQL metric extraction, Python statistical hypothesis testing, an interactive Power BI dashboard, and a formal business report — delivering six answered business questions with data-driven recommendations, all presented to stakeholders in a PowerPoint data story.

---

## ⚡ Technologies

- Python (Pandas, SciPy, Matplotlib, NumPy)
- SQL (SQLite)
- Power BI (DAX, bookmarks, slicers, map visual)
- PowerPoint (stakeholder data story)
- CSV (orders, order_items, products, customers)

---

## 📁 Dataset Structure

A relational e-commerce dataset across four linked tables — structured to mirror a real business database rather than a flat file.

| Table | Rows | Description |
|---|---|---|
| `orders` | 10,000 | Order header: date, channel, status |
| `order_items` | ~17,500 | Line items: product, quantity, unit price |
| `products` | 1,200 | Product catalogue with cost and list price |
| `customers` | 2,000 | Customer profile, country, and segment |

Revenue is computed at line-item level as `quantity × unit_price`. Profit subtracts `cost_price` per product. All revenue KPIs are filtered to `status = 'Completed'` orders only.

---

## 🏆 Headline KPIs

| Metric | Value |
|---|---|
| Total Orders | 10,000 |
| Completed Orders | 7,593 (75.9%) |
| Completed Revenue | $6,943,887 |
| Total Profit | $2,627,747 |
| Avg Order Value | $914.51 |
| Overall Profit Margin | ~38% |
| Return Rate | 12.24% |
| Non-Completed Orders | 24.1% of total |

---

## 🚀 Project Components

### 1️⃣ SQL Analysis — `SQL_Queries.sql`

Seven SQL queries written in SQLite answering the headline KPIs and all six business questions through multi-table JOINs, GROUP BY aggregations, subqueries, and window-style calculations.

**Key Metrics Query** — joins `orders`, `order_items`, and `products` to compute total orders, revenue, profit, and average order value in a single pass on completed orders.

**Business Question 1 — Which product categories drive the most revenue and profit?**
Electronics leads at $2.74M revenue (37.7% margin), followed by Home & Kitchen ($1.22M, 39.1%) and Sports & Outdoors ($941K, 37%). Margins are remarkably flat across all categories (37–39%), meaning revenue volume — not pricing efficiency — is the real differentiator.

| Category | Revenue | Profit | Margin % |
|---|---|---|---|
| Electronics | $2,744,135 | $1,033,495 | 37.7% |
| Home & Kitchen | $1,217,013 | $475,524 | 39.1% |
| Sports & Outdoors | $941,778 | $348,480 | 37.0% |
| Toys & Games | $638,428 | $242,660 | 38.0% |
| Clothing | $569,400 | $212,645 | 37.3% |

**Business Question 2 — How does revenue trend month over month?**
Monthly revenue across 2023–2025 is stable and predictable, fluctuating within a consistent band without strong seasonal peaks. Demand is dependable but growth must be actively driven — there is no organic seasonal surge to rely on.

**Business Question 3 — Which sales channel performs best?**
Web leads by volume (3,398 orders, $3.05M), Mobile App is close behind (3,074 orders, $2.85M), and Marketplace is a smaller contributor (1,121 orders, $1.04M). Average order value is nearly identical across all three channels ($898–$929), meaning the difference is purely customer volume — not basket size.

**Business Question 4 — Who are the top 10 customers by lifetime revenue?**
Thomas Rodriguez (UK) leads at $18,556, followed by Michael Wilson (Singapore, $17,977) and David Tanaka (Japan, $15,772). Top customers span six countries, confirming a genuinely global customer base.

**Business Question 5 — How much revenue is tied up in cancellations and returns?**
24.1% of all orders never complete — 1,183 cancelled (11.8%) and 1,224 returned (12.2%) — representing approximately $2.45 million in revenue that did not convert. This is the single largest recoverable opportunity in the dataset.

| Status | Orders | Revenue | % of Orders |
|---|---|---|---|
| Completed | 7,593 | $6,943,887 | 75.9% |
| Returned | 1,224 | $1,344,475 | 12.2% |
| Cancelled | 1,183 | $1,106,811 | 11.8% |

**Business Question 6 — Which customer segment × country combinations are most valuable?**
The Consumer segment dominates in every market. Consumer-USA ($630K), Consumer-Japan ($478K), and Consumer-UK ($450K) are the top three combinations. Corporate-USA ($343K) is the first non-Consumer entry. The business is fundamentally consumer-driven.

---

### 2️⃣ Statistical Analysis — `Statistical_Analysis.ipynb`

A Python hypothesis test to determine whether return rate differences across product categories are statistically significant or just random noise.

**Approach:**
- Merges `order_items`, `orders`, and `products` using Pandas to reconstruct the full transactional view
- Engineers a binary `is_returned` flag per line item
- Builds a contingency table of returned vs not-returned items per category
- Runs a **Chi-Square test of independence** on the 8×2 contingency table

**Results:**

| Category | Returned Items | Return Rate |
|---|---|---|
| Clothing | 365 | **16.9%** |
| Electronics | 331 | **16.0%** |
| Home & Kitchen | 270 | 12.3% |
| Beauty & Health | 220 | 12.0% |
| Sports & Outdoors | 249 | 11.8% |
| Toys & Games | 266 | 10.8% |
| Office Supplies | 197 | 9.8% |
| Books | 247 | **9.2%** |

| Statistic | Value |
|---|---|
| Chi-Square (χ²) | **111.19** |
| Degrees of freedom | 7 |
| p-value | **5.20e-21** |
| Decision | **Reject H₀** — return rates differ significantly by category |

Clothing and Electronics are returned nearly twice as often as Books and Office Supplies. The difference is statistically confirmed (p < 0.001) — it reflects a genuine structural pattern, not random variation. A dual-axis combo chart (returned item count as bars, return rate % as a line overlay) visualizes both dimensions simultaneously.

---

### 3️⃣ Power BI Dashboard — `E-Commerce_Business_Analytics_Dashboard.pbix`

An interactive dark-themed dashboard with slicers for Channel, Segment, and Category allowing dynamic cross-filtering of all visuals.

**Visuals included:**
- KPI cards — Revenue (9.40M), Total Orders (10K), Profit (3.56M), Avg Order Value ($939.52), Return Rate (12.24%)
- **Avg Order Value by Segment** — bar chart showing Corporate ($963), Consumer ($930), Home Office ($929) are near-identical
- **Revenue by Discount** — bar chart showing the 0% discount tier generates $5.9M, confirming discounting is not a primary growth driver
- **Revenue by Category** — treemap with Electronics ($3.92M) dominating the space
- **Profit and Revenue by Year** — dual-line trend showing steady growth from 2023 ($2.5M revenue, $0.96M profit) through 2025 ($3.6M revenue, $1.35M profit)
- **Completed Revenue by Country** — choropleth world map showing geographic spread
- **Customer Type by Count** — donut chart breaking down Frequent, Occasional, One-time, and No-order customers

---

### 4️⃣ Business Report — `E-Commerce_Business_Analytics_Report.pdf`

A 7-page formal analytics report structured for business stakeholders — covering executive summary, methodology, key findings, trends, anomalies, and data-driven recommendations.

**Recommendations:**
1. **Tackle returns at the source** — Clothing and Electronics account for the highest return rates; invest in better sizing guides, fit imagery, and quality control respectively
2. **Protect and grow the core** — Electronics is the revenue engine; with flat margins across all categories, volume growth is the only lever
3. **Convert more orders** — an 11.8% cancellation rate points to friction at checkout, payment, or delivery-expectation stages worth diagnosing
4. **Nurture the Consumer segment** — it dominates in every country; loyalty and retention programs would directly protect the business's primary revenue base

---

### 5️⃣ Data Story — `Capstone_Project_Data_Story.pptx`

A stakeholder-ready PowerPoint presentation translating the full technical analysis into a clear business narrative — covering the problem, methodology, key findings, anomalies, and actionable recommendations for a non-technical management audience.

---

## 🛠 Running the Project

**SQL:**
1. Load `orders.csv`, `order_items.csv`, `products.csv`, and `customers.csv` into a SQLite or MySQL database
2. Run `SQL_Queries.sql` — each section is independently executable with clear business question headers

**Python:**
1. Install dependencies:
```
pip install pandas scipy matplotlib numpy
```
2. Place all four CSV files in the project directory
3. Open and run all cells in `Statistical_Analysis.ipynb`

**Power BI:**
1. Open `E-Commerce_Business_Analytics_Dashboard.pbix` in Power BI Desktop
2. Update data source paths to point to your local CSV files and refresh

---

## 📁 Repository Structure

```
capstone-project/
│
├── SQL_Queries.sql                              # KPI + 6 business question queries
├── Statistical_Analysis.ipynb                  # Chi-Square return rate analysis
├── E-Commerce_Business_Analytics_Dashboard.pbix # Interactive Power BI dashboard
├── E-Commerce_Business_Analytics_Report.pdf    # 7-page formal business report
├── Capstone_Project_Data_Story.pptx            # Stakeholder PowerPoint presentation
├── Statistical_Analysis_Chart.png              # Returns by category combo chart
├── orders.csv                                  # 10,000 order headers
├── order_items.csv                             # ~17,500 line items
├── products.csv                                # 1,200 products with cost prices
├── customers.csv                               # 2,000 customer profiles
└── README.md
```


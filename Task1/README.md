# 🛒 Superstore EDA & Employee Data Cleaning — Qwertrum Internship Tasks

Two end-to-end data analytics tasks completed during the Qwertrum internship — an exploratory data analysis and business insight report on the Sample Superstore dataset (9,994 orders), and a full data cleaning pipeline that transformed a messy 1,020-row employee dataset into a structured, analysis-ready CSV.

---

## ⚡ Technologies

- Python
- Pandas
- Matplotlib
- CSV (Sample Superstore dataset, Messy & Cleaned Employee datasets)

---

## 📁 Task 1 — Superstore Exploratory Data Analysis (Python)

### 🚀 Features

- Loads the **Sample Superstore dataset** (9,994 rows, 21 columns) and inspects data types and descriptive statistics
- Identifies the **Top 5 best-selling products by total revenue** — led by Canon imageCLASS 2200 Advanced Copier ($61,599) followed by Fellowes PB500, Cisco TelePresence, HON Task Chairs, and GBC DocuBind
- Converts `Order Date` from string to datetime and extracts month-level aggregations to compute **monthly revenue trends**
- Produces three clean **Matplotlib visualizations**:
  - **Line chart** — Total revenue by month, revealing a strong Q4 surge and a quiet February/September dip
  - **Bar chart** — Top 5 best-selling products by revenue
  - **Pie chart** — Revenue split by category (Technology, Furniture, Office Supplies)
- Derives **5 key business insights** from the analysis, written in plain language for non-technical stakeholders

### 🧠 Key Business Insights

**Insight 1 — Technology is carrying the whole business**
Technology alone accounts for nearly two-thirds of all revenue. While impressive, the concentration is a risk — a slowdown in tech sales would disproportionately impact the entire business. Furniture and Office Supplies need strategic attention before this dependency becomes a liability.

**Insight 2 — Nobody expected the USB Hub to win**
Among all sub-categories, a simple USB Hub quietly outsold laptops, monitors, and high-end furniture by unit demand. With remote work desk setups still common, bundling it with larger purchases is a low-effort, high-return opportunity.

**Insight 3 — Summer and year-end are where the money is**
Revenue peaks in June and again in October–November, with a noticeable dip in February and September. These quiet months are predictable — meaning targeted promotions and seasonal deals could convert dead periods into consistent revenue.

**Insight 4 — Office Supplies are being left behind**
Contributing just 2.5% of total revenue for a category that fills every desk in every office is a red flag. Whether it's the product mix, pricing, or lack of promotion — this category needs a reset.

**Insight 5 — The profit story is genuinely strong**
The store earns close to $0.30 profit on every dollar of revenue — a margin most retailers would be satisfied with. The one risk is discount depth: some orders are being discounted up to 80%, and over time that quietly erodes margins that are otherwise healthy.

### 📊 Monthly Revenue Highlights

| Month | Revenue |
|---|---|
| November | $352,461 (highest) |
| December | $325,294 |
| September | $307,650 |
| February | $59,751 (lowest) |
| January | $94,925 |

---

## 📁 Task 2 — Employee Dataset Cleaning (Python)

### 🚀 Features

- Loads a **1,020-row messy employee CSV** and diagnoses all data quality issues before touching a single value
- Documents **5 distinct problems** across the raw dataset in a structured audit table
- Imputes **211 missing `Age` values** with the column median — chosen over mean to avoid distortion from outliers
- Imputes **24 missing `Salary` values** with the column median for the same reason
- Confirms zero missing values across all 12 columns after imputation
- Detects and removes duplicate rows (none found — confirmed clean on this front)
- Converts `Join_Date` from `object` (string) to `datetime64` for proper date-based operations
- Fixes **all-negative `Phone` numbers** (e.g. `-1651623197`) by applying `.abs()` — converting them to valid positive integers
- Converts `Age` from `float64` to `int32` after median fill
- Splits the merged `Department_Region` column (e.g. `"DevOps-California"`) into two clean separate columns: `Department` and `Region`
- Drops the original `Department_Region` column after splitting
- Exports the fully cleaned dataset as **`Cleaned_Employee_dataset.csv`**

### 🧠 Problems Found & Fixed

| # | Column | Problem | Fix Applied |
|---|---|---|---|
| 1 | `Age` | 211 missing values (20% of data) | Median imputation |
| 2 | `Salary` | 24 missing values | Median imputation |
| 3 | `Phone` | All values were negative numbers | `.abs()` to convert to positive |
| 4 | `Join_Date` | Stored as string, not datetime | `pd.to_datetime()` conversion |
| 5 | `Department_Region` | Two fields merged in one column | `.str.split('-', expand=True)` |

### 🛠 Running Both Notebooks

1. Place all CSV files (`Sample - Superstore.csv`, `Messy_Employee_dataset.csv`) in the project directory and update the paths in the notebooks' `pd.read_csv()` calls

2. Install dependencies:

```
pip install pandas matplotlib
```

3. Open the notebooks:

```
jupyter notebook Task1.ipynb
jupyter notebook Task2.ipynb
```

4. Run all cells top to bottom — Task 2 auto-exports `Cleaned_Employee_dataset.csv` on completion

---

## 📁 Repository Structure

```
qwertrum-tasks/
│
├── Task1.ipynb                     # Superstore EDA & business insights
├── Task2.ipynb                     # Employee data cleaning pipeline
├── Sample - Superstore.csv         # Raw Superstore dataset (9,994 rows)
├── Messy_Employee_dataset.csv      # Raw messy employee data (1,020 rows)
├── Cleaned_Employee_dataset.csv    # Output — fully cleaned employee data
└── README.md
```


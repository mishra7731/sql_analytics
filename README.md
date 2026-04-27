# sql_analytics
# SQL Analytics Portfolio — NYC Yellow Taxi (January 2024)

A data analytics portfolio built on ~2.9 million real NYC Yellow Taxi trips, 
demonstrating SQL querying, exploratory data analysis, and data visualization 
using Python, DuckDB, and pandas.

---

## Project Overview

This portfolio answers real operational and business questions a transport or 
analytics team might face, using publicly available NYC TLC trip data. All 
analysis is performed using SQL via DuckDB, with visualizations built in 
matplotlib.

**Dataset**: NYC TLC Yellow Taxi Trip Records — January 2024  
**Source**: [NYC Taxi & Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)  
**Size**: ~2.9 million trips, 19 columns  

---

## Key Findings

- **$78.5M total revenue** generated across January 2024, averaging $2.53M per day
- **Credit card payments dominate**: 2.3M card trips vs 422K cash trips — 
  card payments account for ~84% of all revenue
- **58% of card-paying passengers tip above 25%** — far exceeding the assumed 20% norm
- **Peak demand**: Midweek evenings (Tue–Thu, 6–7pm) are consistently the busiest 
  windows — not weekends as many assume
- **Sunday is the slowest day** in both trip volume (~330K) and revenue
- **Demand grew across January**: Daily trips rose from ~75K in week 1 to 95K+ 
  by month end, visible via 7-day rolling average
- **JFK flat-rate effect**: A visible spike at exactly $70 in the fare distribution 
  represents ~100K airport flat-rate trips
- **Top earning trips travel 11x further**: Q1 trips average 9.23 miles vs Q4's 
  0.84 miles — distance is the single biggest driver of total earnings
- **Corrupt timestamp rows** (dated as early as 2002) found in the raw data — 
  filtered using strict date range conditions

---

## Notebooks

| Notebook | Business Questions Answered |
|---|---|
| [01 — Exploration](notebooks/exploration.ipynb) | Dataset structure, data quality, trip volume by hour and day |
| [02 — Revenue Analysis](notebooks/revenue_analysis.ipynb) | Payment types, tip behavior, fare components |
| [03 — Time Patterns](notebooks/time_patterns.ipynb) | Demand heatmap, daily revenue trend, peak vs off-peak |
| [04 — Driver Performance](notebooks/driver_performance.ipynb) | Vendor comparison, revenue per mile, earnings quartiles |
| [05 — Advanced Windows](notebooks/advanced_windows.ipynb) | Rolling averages, LAG/LEAD, percentile distribution |

---

## SQL Techniques Demonstrated

- Aggregations with `GROUP BY`, `HAVING`, `CASE WHEN`
- Common Table Expressions (CTEs)
- Window functions: `SUM() OVER()`, `AVG() OVER()`, `LAG()`, `NTILE()`
- Rolling averages with `ROWS BETWEEN N PRECEDING AND CURRENT ROW`
- Date/time extraction with `EXTRACT()`, `DAYNAME()`, `DATE()`
- Data cleaning with `NULLIF()`, range filters, and null checks
- Percentile ranking using cumulative window sums

---

## Tech Stack

| Tool | Purpose |
|---|---|
| DuckDB | SQL engine — queries run directly on Parquet files |
| Python 3.13 | Scripting and data manipulation |
| pandas | DataFrame handling and `.describe()` stats |
| matplotlib | All charts and visualizations |
| Jupyter / VS Code | Notebook environment |

---

## Project Structure
SQL_Analytics/
├── data/
│   └── yellow_tripdata_2024-01.parquet
├── notebooks/
│   ├── 01_exploration.ipynb
│   ├── 02_revenue_analysis.ipynb
│   ├── 03_time_patterns.ipynb
│   ├── 04_driver_performance.ipynb
│   └── 05_advanced_windows.ipynb
├── charts/
│   ├── trips_by_hour.png
│   ├── trips_by_day.png
│   ├── fare_distribution.png
│   ├── tip_distribution.png
│   ├── demand_heatmap.png
│   ├── revenue_over_time.png
│   ├── rolling_average.png
│   └── fare_percentiles.png
├── .gitignore
└── README.md


## What I Learned

- Real-world datasets always have quality issues — corrupt timestamps, 
  negative fares, and missing values require careful filtering before analysis
- DuckDB is remarkably fast for analytical SQL directly on Parquet files 
  with no database server required
- Window functions are essential for time-series analysis — rolling averages 
  and LAG comparisons reveal patterns invisible in simple aggregations
- Business context matters: the JFK flat-rate spike, the midweek demand peak, 
  and the consistent tip percentages across fare quartiles are all more 
  interesting than raw numbers alone


## How to Run

```bash
# Clone the repo
git clone https://github.com/mishra7731/sql_analytics.git
cd sql_analytics

# Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install duckdb pandas matplotlib notebook

# Download the dataset
# Go to https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
# Download Yellow Taxi January 2024 Parquet file into the data/ folder

# Open notebooks
jupyter notebook
```

---

# Project 04: Cohort Analysis
### Do Customers Stick Around? Retention, Revenue, and the Leaky Bucket Problem

---

## Business Brief

Every business has a leaky bucket problem. You pour customers in at the top and they drip out over time. The question is not whether customers leave. They always do. The question is how fast, and whether newer customers are better or worse at staying than older ones.

This project runs a full cohort analysis on real e-commerce transaction data and answers:

1. What does the customer retention curve look like over 12 months?
2. Are newer acquisition cohorts retaining better than older ones?
3. Which cohorts drive the most long-term revenue?
4. What is the average customer lifetime value by cohort?

---

## Dataset

| Property | Detail |
|----------|--------|
| **Name** | E-Commerce Data |
| **Direct Link** | https://www.kaggle.com/datasets/carrie1/ecommerce-data |
| **Records** | 541,909 transactions, 4,300+ UK customers |
| **Period** | December 2010 to December 2011 |
| **Why** | 13 months of data gives enough time depth to run proper 12-period retention cohorts |

---

## What Makes This Different

- Builds three separate cohort views: retention rate, revenue, and CLV
- Uses SQL to build the cohort aggregation before any pivot operations
- Calculates a cohort quality score ranking acquisition months by long-term retention
- Identifies the critical drop-off window with precision
- Shows that cohort size and cohort quality are not the same thing

---

## Project Structure

```
cohort-analysis/
├── project_04_cohort_analysis.ipynb
└── README.md
```

---

## Kaggle Setup

1. Search **"E-Commerce Data"** by *carrie1* on Kaggle and attach it
2. Upload `project_04_cohort_analysis.ipynb`
3. Run the path finder cell first
4. Update `DATA_PATH` in Cell 3 if needed
5. Run all cells

---

## Notebook Walkthrough

### Section 1: Setup
Libraries, colour system, output directory.

### Section 2: Load and Prepare
Loads the dataset. Same cleaning pipeline as Project 02 (same dataset). Adds InvoiceMonth as a Period column.

### Section 3: Building the Cohort Table
Step-by-step cohort construction:
1. Finds each customer's first purchase month (cohort assignment)
2. Calculates CohortPeriod (months since first purchase) for every transaction
3. Loads into SQLite and queries cohort sizes
4. Builds the retention and revenue matrices with a SQL aggregation query
5. Pivots into heatmap-ready format (rows = cohorts, columns = periods)

### Section 4: Cohort Heatmaps
Two heatmaps using Seaborn:
- Retention rate heatmap (RdYlGn colour scale, 0 to 100%)
- Revenue heatmap (Blues colour scale, values in GBP thousands)

### Section 5: Retention Curves
Two-panel Plotly chart:
- Left: average retention curve across all cohorts with area fill
- Right: individual cohort lines overlaid for comparison

Key stats printed: Month 1 retention rate, Month 3 retention rate, drop from Month 0 to 1.

### Section 6: CLV by Cohort
SQL query calculating total revenue, CLV per customer, total orders, and orders per customer for each cohort. Two-panel chart: CLV bar chart by cohort and CLV vs cohort size scatter.

### Section 7: Critical Drop-off Window
Month-on-month retention drop calculation. Bar chart showing which transition period has the biggest churn. Retention curve with the critical window highlighted in red. Key stat: what percentage of total eventual churn happens within the first 3 months.

### Section 8: Cohort Quality Score
Composite score (average retention rate across all periods) per cohort. Ranked bar chart colour-coded green/amber/red. Top 3 and bottom 3 cohorts printed with CLV and size for context.

### Section 9: Executive Summary Dashboard
Dark-theme KPI cards: Month 1 retention, Month 3 retention, best cohort, highest CLV, weakest cohort, total revenue tracked.

### Section 10: Findings and Recommendations
Five findings with evidence. Four recommendations with specific business actions.

---

## Key Findings

| Finding | Evidence |
|---------|----------|
| Largest retention drop happens Month 0 to Month 1 | Drop-off analysis |
| Retention stabilises significantly after Month 3 | Average retention curve |
| Cohort quality varies independently of cohort size | Quality score vs size scatter |
| Some months produced fewer but more valuable customers | CLV analysis |
| A clear critical intervention window exists in the first 3 months | Cumulative drop calculation |

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Python (Pandas, NumPy) | Data manipulation, cohort period calculation |
| SQLite3 | Cohort size and aggregation queries |
| Seaborn | Annotated heatmaps |
| Plotly | Interactive retention curves and CLV charts |
| Matplotlib | Drop-off bar chart, quality score chart |

---

*Built by Jessica Dan-Odhomo - [LinkedIn](https://www.linkedin.com/in/jessica-dan-odhomo) - [GitHub](https://github.com/Teekaayyy)*

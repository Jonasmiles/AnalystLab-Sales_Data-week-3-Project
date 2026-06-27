# AnalystLab-Sales_Data-week-3-Project
## Sales Data SQL Analysis

SQL-based exploratory and business analysis on a sales transactions dataset (2,823 records, 2003–2005), covering schema design, core/advanced SQL, business problem solving, and query optimization.

## Overview

| Metric | Value |
|---|---|
| Total Records | 2,823 |
| Date Range | 2003 – 2005 |
| Source File | `sales_data_sample.csv` |
| Entities | Customers, Orders, Order Lines, Products |

## Schema

The raw CSV is a single denormalized file combining four logical entities:

```
CUSTOMERS ──< ORDERS ──< ORDER_LINES >── PRODUCTS
```

| Entity | Primary Key | Relationship |
|---|---|---|
| Customers | `CUSTOMERNAME` | 1-to-many → Orders |
| Orders | `ORDERNUMBER` | 1-to-many → Order Lines |
| Order Lines | `ORDERNUMBER` + `ORDERLINENUMBER` | many-to-1 → Products |
| Products | `PRODUCTCODE` | Referenced by Order Lines |

`SALES = QUANTITYORDERED * PRICEEACH`

## What's Covered

- **Core SQL** — `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `HAVING`, aggregate functions (`SUM`, `AVG`, `COUNT`)
- **Advanced SQL** — `INNER`/`LEFT`/`RIGHT JOIN`, subqueries, window functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`, `PARTITION BY`, `LAG`)
- **Business analysis** — top products/customers, revenue trends over time, customer purchasing behavior, segmentation
- **Optimization** — indexing strategy, clean/readable query style

## Key Insights

1. **Revenue is concentrated** — A small set of product lines (Classic Cars, Motorcycles) and top-10 customers drive a disproportionate share of total revenue.
2. **Seasonal revenue pattern** — Sales consistently peak toward Q4 each year.
3. **Strong repeat-customer base** — Most customers place multiple orders rather than purchasing once.
4. **Deal size varies by product line** — Higher-value deals cluster around specific categories.
5. **Order volume is geographically concentrated** — A handful of countries, led by the USA, account for the majority of orders.

## Repo Structure

```
├── scripts/
│   ├── 01_core_queries.sql
│   ├── 02_joins.sql
│   ├── 03_subqueries_window_functions.sql
│   ├── 04_business_questions.sql
│   └── 05_indexing_optimization.sql
├── reports/
│   └── Sales_Data_SQL_Queries_and_Insights.docx
└── README.md
```

## Sample Query

```sql
-- Top 10 customers by total spend, ranked
SELECT
    CUSTOMERNAME,
    SUM(SALES) AS total_spend,
    RANK() OVER (ORDER BY SUM(SALES) DESC) AS customer_rank
FROM sales_data_sample
GROUP BY CUSTOMERNAME
ORDER BY total_spend DESC;
```

Full scripts: [`scripts/`](./scripts) · Full report: [`reports/Sales_Data_SQL_Queries_and_Insights.docx`](./reports/Sales_Data_SQL_Queries_and_Insights.docx)

## Tools Used
SQL Server

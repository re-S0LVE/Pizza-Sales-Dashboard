# Pizza Sales Dashboard

An end-to-end data analytics project built with SQL Server and Power BI, analyzing 48,000+ fictional pizza order records across 2015 to surface revenue trends, product performance, and peak ordering patterns.

---

## Project Overview

This project follows a full analytics workflow, writing and validating SQL queries against a relational database, then building an interactive Power BI dashboard that mirrors those results. SQL output served as an extra validation layer, every KPI and chart value in Power BI was cross-checked against the query results before the dashboard was finalized.

---

## Tools Used

- **SQL Server Management Studio (SSMS)** — data import, querying, aggregation, query showcase
- **Power BI Desktop** — data modeling, DAX measures, Power Query, visualization
- **Power Query (M)** — data cleaning and column transformations

---

## Dataset

- 48,620 rows of pizza sales data (2015)
- Fields: order ID, date, time, pizza name/category/size, quantity, unit price, total price
> **Note:** This dataset is fictional and intended for portfolio and learning purposes only.

---

## SQL — Queries Written

All queries were written from scratch and saved with screenshots for validation.

**KPIs**
- Total Revenue — `SUM(total_price)`
- Average Order Value — `SUM(total_price) / COUNT(DISTINCT order_id)`
- Total Pizzas Sold — `SUM(quantity)`
- Total Orders — `COUNT(DISTINCT order_id)`
- Avg Pizzas per Order — `CAST(SUM(quantity) AS DECIMAL) / COUNT(DISTINCT order_id)`

**Trend Analysis**
- Daily order trend using `DATENAME(DW, order_date)`
- Monthly order trend using `DATENAME(MONTH, order_date)`

**Category Breakdown**
- % of sales by pizza category and size using subquery-based percentage of total
- Applied `WHERE` filters inside subqueries to ensure accurate filtered results

**Best / Worst Sellers**
- Top 5 and bottom 5 pizzas by Revenue, Quantity, and Total Orders using `TOP 5` with `ORDER BY DESC/ASC`

---

## Power BI — Dashboard Pages

### Page 1: Dashboard
- 5 KPI cards (new card visual)
- Daily trend bar chart (sorted by custom `Day Number` column)
- Monthly trend area chart (sorted by `Month Number` column)
- Donut charts: % of sales by category and size
- Funnel chart: total pizzas sold by category
- Slicers: Pizza Category (dropdown), Date Range (between slider)
- Insight text panel: busiest days/times, sales performance by category and size

### Page 2: Best / Worst Sellers
- Top 5 and bottom 5 bar charts for Revenue, Quantity, and Total Orders
- Conditional formatting gradient colors per chart
- Visual-level Top N filters applied directly in Power BI

---

## DAX Measures

```
Total Revenue = SUM(pizza_sales[total_price])
Total Orders = DISTINCTCOUNT(pizza_sales[order_id])
Avg Order Value = [Total Revenue] / [Total Orders]
Total Pizzas Sold = SUM(pizza_sales[quantity])
Avg Pizzas per Order = [Total Pizzas Sold] / [Total Orders]
```

---

## Power Query Transformations

- Replaced abbreviated pizza size codes (S, M, L, XL, XXL) with full labels
- Extracted `Day Name` and `Month Name` from `order_date`
- Created `Day Number` and `Month Number` columns for correct sort ordering
- Added `Order Month` (3-letter uppercase abbreviation) for chart axis labels

---

## Key Findings

- Friday and Saturday are the busiest days for orders
- July and January see the highest monthly order volumes
- Classic category leads all categories in total pizzas sold and orders
- Large size accounts for ~46% of sales by revenue
- Thai Chicken Pizza generates the highest revenue; Brie Carre is the lowest performer across all metrics

---

## Validation

All Power BI KPI values were compared against SQL query output before finalizing the dashboard. Results matched exactly across total revenue, order count, pizza quantity, and category breakdowns.

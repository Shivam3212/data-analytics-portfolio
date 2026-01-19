# Sales Performance Analysis using SQL

## Business Objective
To analyze sales performance using SQL queries that support data-driven business decisions.

## Dataset
Sales transaction data containing order, customer, region, category, sales, and profit information.

## Business Questions
1. What are the total sales and profit?
2. Which regions generate the highest sales?
3. How do sales trend over time?

## SQL Queries

### Total Sales and Profit
```sql
SELECT
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit
FROM sales_data;
```
### Sales By Region
```sql
SELECT
    region,
    SUM(sales) AS total_sales
FROM sales_data
GROUP BY region
ORDER BY total_sales DESC;
```
### Monthly Sale Trends 
```sql
SELECT
    DATE_TRUNC('month', order_date) AS sales_month,
    SUM(sales) AS monthly_sales
FROM sales_data
GROUP BY sales_month
ORDER BY sales_month;
```
## Advanced SQL Analysis

### Top Customers by Sales
```sql
SELECT
    customer_id,
    customer_name,
    SUM(sales) AS total_sales
FROM sales_data
GROUP BY customer_id, customer_name
ORDER BY total_sales DESC
LIMIT 10;
```
### Profitability Classification
```sql
SELECT
    category,
    SUM(profit) AS total_profit,
    CASE
        WHEN SUM(profit) > 0 THEN 'Profitable'
        ELSE 'Loss-Making'
    END AS profit_status
FROM sales_data
GROUP BY category;
```
### Profit Margin by Category
```sql
SELECT
    category,
    SUM(profit) / NULLIF(SUM(sales), 0) AS profit_margin
FROM sales_data
GROUP BY category;
```
### Sales By Customer Segment 
```sql
SELECT
    c.segment,
    SUM(s.sales) AS total_sales
FROM sales_data s
JOIN customers c
    ON s.customer_id = c.customer_id
GROUP BY c.segment;
```
### Ranking of Customers by Sales
```sql
SELECT
    customer_id,
    customer_name,
    SUM(sales) AS total_sales,
    ROW_NUMBER() OVER (ORDER BY SUM(sales) DESC) AS sales_rank
FROM sales_data
GROUP BY customer_id, customer_name;
```
### Sales Accumulate Over Time
```sql
SELECT
    order_date,
    sales,
    SUM(sales) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_sales
FROM sales_data;
```
### Growth over month
```sql
SELECT
    sales_month,
    monthly_sales,
    monthly_sales -
    LAG(monthly_sales) OVER (ORDER BY sales_month) AS mom_growth
FROM (
    SELECT
        DATE_TRUNC('month', order_date) AS sales_month,
        SUM(sales) AS monthly_sales
    FROM sales_data
    GROUP BY sales_month
) t;
```





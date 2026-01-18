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



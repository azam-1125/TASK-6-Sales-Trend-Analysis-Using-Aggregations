# TASK 6: MySQL Time-Series Sales Analysis & KPI Calculation

## 🎯 Objective

The objective of this task was to perform a time-series analysis using SQL to calculate key performance indicators (KPIs) for the online orders data. This involved aggregating data by month and year to determine trends in revenue and order volume.

## 🛠️ Tools and Methodology

* **Primary Tool:** MySQL / SQL
* **Dataset:** `oline_orders.csv`
* **Key SQL Concepts Used:**
    * **Time Series Aggregation:** `EXTRACT(YEAR/MONTH FROM ...)` and `GROUP BY` to segment data chronologically.
    * **Revenue Calculation:** `SUM(unitprice * quantity)`.
    * **Volume Calculation:** `COUNT(DISTINCT order_id)`.
    * **KPI Derivation:** Calculation of **Average Revenue per Order** by dividing total revenue by the unique order count.

## 📁 Key Deliverable: Final SQL Query

The following SQL query addresses all task requirements:
### 1.Revenue by year, month and also Count of orders:

```sql
select extract( year from InvoiceDate) as year,
extract(month from InvoiceDate) as month,
Sum(Quantity*UnitPrice) as revenue,
COUNT(DISTINCT InvoiceNo) AS order_volume
from orders.orders
group by year,month
```
### 2. Revenue per each order:
```sql
select InvoiceNo,
Sum(Quantity*UnitPrice) as revenue
from orders.orders
group by Invoiceno
```
### 3. Total unique orders, Total revenue, and average Revenue per each order:
```sql
select count(distinct InvoiceNo) as unq_orders,
Sum(Quantity*UnitPrice) as revenue,
SUM(unitprice * quantity) / COUNT(DISTINCT InvoiceNo) AS avg_revenue_per_order
from orders.orders
```
### 3. Limit results for specific time periods:
```sql
select * from orders.orders
WHERE
    Invoicedate BETWEEN '2010-12-01 08:26:00' AND '2010-12-31 00:00:00'
order by InvoiceDate asc;
```


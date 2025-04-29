# TASK-6-Sales-Trend-Analysis-Using-Aggregations
Objective: Analyze monthly revenue and order volume. (Using:- MYSQL)

task 6:-
---

## ✅ Step-by-Step

---

### 🔹 **Step 1**
```sql
SELECT * FROM online_sales.orders LIMIT 10;
```
🟢 **What it does:**  
This shows the first 10 rows in the table. It helps you look at the data — like the date of the order, how much money was made, and what product was sold.


---

### 🔹 **Step 2**
```sql
SELECT
    order_date,
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month
FROM online_sales.orders
LIMIT 10;
```
🟢 **What it does:**  
Takes the full date (like 2023-03-10) and breaks it into:
- Year (2023)
- Month (3 for March)


---

### 🔹 **Step 3**
```sql
SELECT
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_id) AS total_order_volume
FROM online_sales.orders;
```
🟢 **What it does:**  
- Adds up all the money from orders (`SUM`)
- Counts how many different orders were made


---

### 🔹 **Step 4**
```sql
SELECT
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month
FROM online_sales.orders
GROUP BY
    YEAR(order_date), MONTH(order_date);
```
🟢 **What it does:**  
Groups your data so that all orders from the **same month** and **same year** are put together.


---

### 🔹 **Step 5**
```sql
SELECT
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month,
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_id) AS order_volume
FROM online_sales.orders
GROUP BY YEAR(order_date), MONTH(order_date);
```
🟢 **What it does:**  
Shows how much money you made and how many orders were placed in each month.


---

### 🔹 **Step 6**
```sql
ORDER BY order_year, order_month;
```
🟢 **What it does:**  
Puts the results in order — like January, February, March, etc.


---

### 🔹 **Step 7**
```sql
WHERE order_date BETWEEN '2023-01-01' AND '2024-12-31'
```
🟢 **What it does:**  
Only shows data from 2023 and 2024 — ignores older or future orders.


---

## ✅ Final Simple Query (All Steps Together)

```sql
SELECT
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month,
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_id) AS order_volume
FROM online_sales.orders
WHERE order_date BETWEEN '2023-01-01' AND '2024-12-31'
GROUP BY YEAR(order_date), MONTH(order_date)
ORDER BY order_year, order_month;
```

This shows:
- Total money made each month
- Number of orders each month
- For just 2023 and 2024
- In date order

---

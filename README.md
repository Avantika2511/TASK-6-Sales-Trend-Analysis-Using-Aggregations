# TASK-6-Sales-Trend-Analysis-Using-Aggregations
Objective: Analyze monthly revenue and order volume. (Using:- MYSQL)

task 6:-
---

## ✅ Easy Explanation: Step-by-Step

---

### 🔹 **Step 1: See What’s in the Table**
```sql
SELECT * FROM online_sales.orders LIMIT 10;
```
🟢 **What it does:**  
This shows the first 10 rows in the table. It helps you look at the data — like the date of the order, how much money was made, and what product was sold.

🟢 **Why it matters:**  
It helps you understand what kind of data you're working with before writing complex queries.

---

### 🔹 **Step 2: Get the Year and Month from the Order Date**
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

🟢 **Why it matters:**  
You want to know **how sales change month by month**, so you need to break the date into parts.

---

### 🔹 **Step 3: Total Money and Number of Orders (Overall)**
```sql
SELECT
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_id) AS total_order_volume
FROM online_sales.orders;
```
🟢 **What it does:**  
- Adds up all the money from orders (`SUM`)
- Counts how many different orders were made

🟢 **Why it matters:**  
This gives you the **big picture**: total money and total orders.

---

### 🔹 **Step 4: Group Orders by Year and Month**
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

🟢 **Why it matters:**  
It lets you look at each month as its own group — so you can compare January vs. February, etc.

---

### 🔹 **Step 5: Get Monthly Totals**
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

🟢 **Why it matters:**  
Now you can **see trends** — for example, sales going up in December or dropping in June.

---

### 🔹 **Step 6: Sort by Date**
```sql
ORDER BY order_year, order_month;
```
🟢 **What it does:**  
Puts the results in order — like January, February, March, etc.

🟢 **Why it matters:**  
It makes the report easy to read, like a calendar.

---

### 🔹 **Step 7: Look at a Specific Time Range (Optional)**
```sql
WHERE order_date BETWEEN '2023-01-01' AND '2024-12-31'
```
🟢 **What it does:**  
Only shows data from 2023 and 2024 — ignores older or future orders.

🟢 **Why it matters:**  
You may only want to see **recent data** — not everything in the database.

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

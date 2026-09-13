# Mobile Sales Performance & Time-Intelligence Dashboard

A Power BI analytics project designed to track sales revenue, transaction volume, customer ratings, and historical performance across mobile brands and regional retail markets.

---

## 📌 Project Overview

This dashboard provides business visibility into retail mobile sales performance. It helps analyze which brands generate the highest revenue, how customers choose to pay, and how sales trend over time compared to historical baselines.

---

## 🎯 Key Performance Indicators (KPIs)

The dashboard tracks four primary business metrics at the top of every page[cite: 1]:

| KPI | Value | Description |
| :--- | :--- | :--- |
| **Total Sales** | **769M** | Total gross revenue generated across all transactions[cite: 1]. |
| **Total Quantity** | **19K** | Total number of mobile phone units sold[cite: 1]. |
| **Transactions** | **4K (3,835)** | Total number of completed sales orders[cite: 1]. |
| **Average Price** | **40.11K** | Average selling price per unit sold[cite: 1]. |

---

## 📊 Key Insights from the Data

* **Brand Performance:** Apple generated the highest revenue at **161.6M** (783 transactions), followed by Samsung at **160.0M** (775 transactions) and OnePlus at **153.7M** (768 transactions).
* **Top Selling Models:** The highest revenue-generating phones were the **iPhone SE** (60M), **OnePlus Nord** (58M), and **Galaxy Note 20** (56M).
* **Payment Methods:** Transactions are evenly distributed across all payment channels—UPI (**26.36%**), Debit Card (**24.72%**), Credit Card (**24.69%**), and Cash (**24.22%**).
* **Top Cities by Volume:** Leading cities by units sold include **Ludhiana** (1,696), **Delhi** (1,672), **Jodhpur** (1,625), and **Lucknow** (1,609).
* **Seasonality:** Quarterly sales peaked in **Q1 (196M)** and **Q4 (193M)**.

---

## 🖥️ Dashboard Views

### 1. Executive Dashboard
* Overview of brand sales, model rankings, payment channel distribution, city-wise sales volume, and customer ratings[cite: 1].
* Includes interactive slicers for Mobile Model, Brand, and Payment Method.


### 2. Month-to-Date (MTD) Report
* Tracks daily cumulative revenue throughout the selected month to monitor target pacing[cite: 1].
* Displays day-by-day sales progression alongside current month KPIs.



### 3. Same Period Last Year (SPLY) Analysis
* Compares current period revenue against prior-year benchmarks across years (2021–2024), quarters, and months[cite: 1].
* Identifies Year-over-Year (YoY) growth trends and performance gaps.



---

## ⚙️ Data Model & DAX Formulas

The project connects a sales transaction table (`sales_data`) to a dedicated calendar dimension (`Custom_calender`).

### Core DAX Measures Used:

```dax
// 1. Total Units Sold
Total_Quantity = SUM(sales_data[Units Sold])

// 2. Total Gross Sales
Total_Sales = 
SUMX(
    sales_data,
    sales_data[Units Sold] * sales_data[Price Per Unit]
)

// 3. Total Transaction Count
Transactions = COUNTROWS(sales_data)

// 4. Weighted Average Selling Price
Average_price = DIVIDE([Total_Sales], [Total_Quantity], 0)

// 5. Month-to-Date Cumulative Sales
MTD = 
TOTALMTD(
    [Total_Sales],
    Custom_calender[Date]
)

// 6. Prior Year Sales (Same Period Last Year)
Same Period Last Year = 
CALCULATE(
    [Total_Sales],
    SAMEPERIODLASTYEAR(Custom_calender[Date])
)

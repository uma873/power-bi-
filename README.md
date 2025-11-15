
# Pizza-Sales-Analysis
 The Pizza Sales Analysis Dashboard utilizes MySQL workbench
 and Tableau for comprehensive data analysis,To analyze pizza sales revenue, identify trends, and provide insights to improve
sales.
Steps to Follow:

# Project : Pizza Sales Analysis
## Table of Contents
-	[Problem Statement](#problem-statement)
-	[Data Analysis using MySQL](#data-analysis-using-mysql)
-	[Data Cleaning ](#data-cleaning)
-	[Build Dashboard or a Report using Tableau](#build-dashboard-or-a-report-using-tableau)
-	[Tools, Software and Libraries](#tools-software-and-libraries)
-	[References](#references)
## Problem Statement
### KPI’s REQUIREMENT
We need to analyze key indicators for our pizza sales data to gain insights into our business performance. Specifically, we want to calculate the following metrics:
1.	Total Revenue: The sum of the total price of all pizza orders.
2.	Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
3.	Total Pizzas Sold: The sum of the quantities of all pizzas sold.
4.	Total Orders: The total number of orders placed.
5.	Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.
### CHARTS REQUIREMENT
We would like to visualize various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:
1. Hourly Trend for line chart  chart that displays the hourly trend of total revenue  over a specific time period. This chart will help us identify any patterns or volumes on a hourly basis.
2. Weekly Trend for total revenue: Create a line chart that illustrates the weekly trend of total orders throughout the year. This chart will allow us to identify peak weeks or periods of high order activity.
Total Revenue  over the years (time ) Total revenue over the years shows how the business is growing or declining with time. Any upward trend indicates improved sales performance, while dips highlight periods needing investigation. This helps identify successful years, seasonal patterns, and long-term business health.
4. Percentage of Sales by Pizza Size: Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.
5. Revenue by Piza name in bar chart .The bar chart shows which pizza items generate the highest revenue, helping identify the most profitable products. Top-selling pizzas should be prioritized for promotions and inventory, while low-revenue items may need pricing, marketing, or menu improvement.
6.Filtering by pizza category shows which categories (Classic, Veggie, Supreme, etc.) contribute most to overall sales and revenue. It helps compare customer preferences across categories and identify top-performing or underperforming segments. This allows better menu planning, marketing focus, and inventory control.
7. Using the month filter helps identify seasonal trends in sales throughout the year. It highlights peak months with higher revenue and low-performing months that may need promotions. This supports better forecasting, staffing, and inventory planning.

## Data Analysis using MySQL
Utilized MySQL for data extraction and calculation of key metrics such as Total Revenue, Average Order Value, Total Pizzas Sold, Total Orders, and Average Pizzas Per Order.
### DATA IMPORT https://drive.google.com/open?id=1NlNRLROjMW8vKFZ-YFMq31QJjEMutk6J&usp=drive_fs


##### 
### ANALYSIS OF DIFFERENT SQL STATEMENT ON DATA BASE
#### A.	KPI’s
1.	Total Revenue:
```sql
SELECT SUM(total_price) AS total_revenue FROM pizza_sales;
```
2. Average Order Value:
```sql
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS avg_order_value FROM pizza_sales;
```
3.	Total Pizza Sold:
```sql
SELECT SUM(quantity) AS total_pizza_sold FROM pizza_sales;
```
4.	Total Orders:
```sql
SELECT COUNT(DISTINCT order_id) AS total_order FROM pizza_sales;
```
5.	Average Pizzas Per Order:
```sql
SELECT ROUND(SUM(quantity) / COUNT(DISTINCT order_id), 2) AS avg_pizza_per_order FROM pizza_sales;
```
#### B. Hourly Trend for Total Pizzas Sold
```sql
SELECT HOUR(order_time) AS order_hours, SUM(quantity) AS total_pizzas_sold
FROM pizza_sales
GROUP BY HOUR(order_time)
ORDER BY HOUR(order_time);
```
#### C.	Weekly Trend for Orders
```sql
SELECT WEEK(order_date, 3) AS WeekNumber, YEAR(order_date) AS Year,
      COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales
GROUP BY WEEK(order_date, 3), YEAR(order_date)
ORDER BY Year, WeekNumber;
```
#### D.	% of Sales by Pizza Category
```sql
SELECT pizza_category,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales 
GROUP BY pizza_category;
```
OR
```sql
SELECT pizza_category,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales
     WHERE MONTH(order_date) = 1), 2) AS PCT
 FROM pizza_sales
 WHERE MONTH(order_date) = 1
GROUP BY pizza_category;
```

#### E.	% of Sales by Pizza Size
```sql
SELECT pizza_size,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```
#### F.	Total Pizzas Sold by Pizza Category
```sql
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
-- WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```




## Data Cleaning 
Pizza size category we have in our database is abbreviated and for dashboard we need it in full expanded form. For eg. L= large, M= medium etc, so we will create an alias to temporary change its name in required format.
##### 
## Build Dashboard or a Report using Tableau
Created a comprehensive dashboard in Tableau featuring key metrics and charts, including Hourly Trend, Weekly Trend, Sales by Category, Sales by Size, Total Pizzas Sold by Category, Top 5 Best Sellers, and Bottom 5 Worst Sellers.
### KPI’S
-	Total Revenue SUM([order id])
-	Total Orders COUNTD([order id])
-	Average Order Value [total revenue] / [total orders]
-	Total Pizzas Sold SUM([quantity])
-	Average Pizzas Per Order [total pizzas sold] / [total orders]
##### Dashbaord
<img width="958" height="536" alt="PIZAA SALES" src="https://github.com/user-attachments/assets/9836768e-447b-49ff-9018-d9e83e693e1e" />
####Video Dashboard https://drive.google.com/file/d/1Z80QFOn59O02shD-3nB1kUD9f7DB9wMy/view?usp=drive_link




## Tools, Software, and Libraries
##### -	MySQL Workbench 8.0. 
##### -	Tableau 2025.1.0 
##### -	Excel version 2021
## References



# Pizza-Sales-Analysis
 The Pizza Sales Analysis Dashboard utilizes MySQL and Tableau for comprehensive data analysis, aiding businesses in optimizing sales strategies and enhancing customer satisfaction
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
1. Hourly Trend for Total Pizzas Sold: Create a stacked bar chart that displays the hourly trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a hourly basis.
2. Weekly Trend for Total Orders: Create a line chart that illustrates the weekly trend of total orders throughout the year. This chart will allow us to identify peak weeks or periods of high order activity.
3. Percentage of Sales by Pizza Category: Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.
4. Percentage of Sales by Pizza Size: Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.
5. Total Pizzas Sold by Pizza Category: Create a funnel chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.
6. Top 5 Best Sellers by Revenue, Total Quantity and Total Orders: Create a bar chart highlighting the top 5 best-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will help us identify the most popular pizza options.
7. Bottom 5 Best Sellers by Revenue, Total Quantity and Total Orders: Create a bar chart showcasing the bottom 5 worst-selling pizzas based on the Revenue, Total Quantity, Total Orders. This chart will enable us to identify underperforming or less popular pizza options.
## Data Analysis using MySQL
Utilized MySQL for data extraction and calculation of key metrics such as Total Revenue, Average Order Value, Total Pizzas Sold, Total Orders, and Average Pizzas Per Order.
### DATA IMPORT
<img width="958" height="536" alt="PIZAA SALES" src="https://github.com/user-attachments/assets/e6a472fd-45db-4edc-99bd-8c2eb6f64333" />

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
#### G.	Top 5 Pizzas by Revenue
```sql
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM  pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC LIMIT 5;
```
#### H. Bottom 5 Pizzas by Revenue
```sql
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC LIMIT 5;
```
#### I. Top 5 Pizzas by Quantity
```sql
SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
 LIMIT 5;
```
#### J. Top 5 Pizzas by Total Orders
```sql
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
```
#### K. Borrom 5 Pizzas by Total Orders
```sql
SELECT 
    pizza_name, 
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
LIMIT 5;
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



## Tools, Software, and Libraries
##### -	MySQL Workbench 8.0. 
##### -	Tableau 2025.1.0 
##### -	Excel version 2021
## References


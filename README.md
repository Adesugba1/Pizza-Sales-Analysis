# Pizza-Sales-Analysis
---
## Table of Contents
- [Project Overview](#project-overview)
- [Data](#data)
- [Tools Used](#tools-used)
- [Calculated Metrics](#calculated-metrics)
- [Charts Requirement](#charts-requirement)
- [Data Analysis](#data-analysis)
- [Dashboard](#dashboard)
- [Insights](#insights)
  
## Project Overview
This Pizza Sales Analysis was carried to identify the key indicators for the pizza sales data to gain insights into the business performance.

## Data
The Pizza Sales Data contains 48,621 row and 12 columns.

## Tools Used
-	Microsoft Excel (Data Cleaning)
-	SQL (Data Exploration)
-	PowerBI (Data Visualization)
  
## Calculated Metrics
-	Total Revenue
-	Average Order Value
-	Total Pizza Sold
-	Total Orders
-	Average Pizza per Order
  
## Charts Requirement
Visualization was carried out on various aspect of the pizza sales data to gain insight and understand key trend.  The following requirements were identified for creating charts.
-	Daily trend for total order
-	Monthly trend for total order
-	Percentage of Sales by Pizza category
-	Percentage of Sales by Pizza size
-	Total pizza sold by pizza category
-	Top 5 Customers by Revenue, Total Quantity and Total Orders
-	Bottom 5 Customers by Revenue, Total Quantity and Total Order
-	
## Data Analysis 
### Total Revenue:
```sql
SELECT SUM (total_price) AS Total_Revenue
FROM pizza_sales;
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/c4a3df97-97bc-47de-a5fe-251dc067c6f7)

### Total Pizzas Sold
```sql
SELECT SUM (quantity )AS Total_pizza_sold
FROM pizza_sales
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/2b250fef-31d1-43ab-a481-0419430c4c17)

### Total Orders
```sql
SELECT COUNT (DISTINCTorder_id)AS Total_Orders
FROM pizza_sales
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/98df707b-cd4b-4358-a611-2c64ae32d8ef)

### Average Pizzas Per Order
```sql
SELECT CAST(CAST(SUM(quantity)ASDECIMAL(10,2))/
CAST(COUNT(DISTINCTorder_id)ASDECIMAL(10,2))ASDECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/02286f1a-021e-438c-8347-601a1034d5f2)

### Daily Trend for Total Orders
```sql 
SELECT DATENAME(DW,order_date) AS order_day,
COUNT(DISTINCTorder_id) AS total_orders
FROM pizza_sales
GROUPBY DATENAME(DW,order_date)
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/62da061f-baf6-4dd6-a93f-6c9760f081bd)

### Monthly Trend for Orders
```sql
SELECT DATENAME(MONTH,order_date) AS Month_Name,
COUNT(DISTINCTorder_id) AS Total_Orders
FROM pizza_sales
GROUPBY DATENAME(MONTH,order_date)
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/5dcbea50-ba7a-40b2-a6f2-af2ddf65fbd6)

### % of Sales by Pizza Category
```sql 
SELECTpizza_category, 
CAST(SUM(total_price)ASDECIMAL(10,2))astotal_revenue,
CAST(SUM(total_price)* 100 /(SELECTSUM(total_price)
FROM pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUPBY pizza_category
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/fa8ec087-d84d-4697-bc60-cb25b9d4c1ff)

### % of Sales by Pizza Size
```sql 
SELECT pizza_size,
CAST(SUM(total_price)ASDECIMAL(10,2)) AS total_revenue,
CAST(SUM(total_price)* 100 /(SELECTSUM(total_price)
FROM pizza_sales) AS DECIMAL(10,2))AS PCT
FROM pizza_sales
GROUPBY pizza_size
ORDERBY pizza_size
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/87ca23a3-5f38-443f-99c5-7738f6c82d4a)

### Total Pizzas Sold by Pizza Category
```sql 
SELECTpizza_category,
SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date)= 2
GROUPBY pizza_category
ORDERBY Total_Quantity_Sold DESC
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/5d526175-eb8d-4e68-9c36-95c8d483a5f9)

### Top 5 Customers by Revenue
```sql 
SELECT Top 5 pizza_name,
SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUPBY pizza_name
ORDERBY Total_Revenue DESC
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/e40eba64-4912-4410-a0b9-28d94fc45060)

### Bottom 5 Customers by Revenue
```sql 
SELECT Top 5 pizza_name,
SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUPBY pizza_name
ORDERBY Total_Revenue ASC
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/3a217cdb-3a6f-439e-9aa1-07b0a4f4bd0b)

### Top 5 Customers by Quantity
```sql 
SELECT Top 5 pizza_name,
SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/0750147c-d18f-4c00-851d-6596a123ba98)

### Bottom 5 Customers by Quantity
```sql
SELECT TOP 5 pizza_name,
SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/304c1af6-b851-47c8-89c4-a29afdd21b14)

### Top 5 Customers Pizzas by Total Orders
```sql 
SELECT Top 5 pizza_name,
COUNT(DISTINCTorder_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/607b02c1-e6d6-4bad-a4df-bbdb25a066cc)

### Bottom 5 Customers by Total Orders
```sql 
SELECT Top 5 pizza_name,
COUNT(DISTINCTorder_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_OrdersASC
```
![image](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/5831d799-be17-46d5-a3c9-5bb116d09df5)

## Dashboard
Clink the [Link](https://app.powerbi.com/view?r=eyJrIjoiMTllZTU2MDAtODYxNC00YWQxLWI0MDEtODA5NTBlMjkwODg3IiwidCI6ImRmODY3OWNkLWE4MGUtNDVkOC05OWFjLWM4M2VkN2ZmOTVhMCJ9) for Interactive Dashboard
![Screenshot_20240119-203155_1](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/d0955569-450b-41d2-9fc0-9eecf7652dc0)
![Screenshot_20240305-130747](https://github.com/Adesugba1/Pizza-Sales-Analysis/assets/143879001/47d8b8c9-52e1-4b38-832d-599487b5a5b9)

## Insights
### Busiest Day, Time and Month
-	The highest orders were place on weekends in the evenings with Friday having 3,500 orders and Saturday having 3,200 orders.
-	The maximum orders were seen to be in the months of July (1,935 orders) and January (1,845 orders).
### Sales Performance by Category and Size
-	Classic category contributed to maximum sales & total order with a total of 14,888 making up 26.91% of total sales.
-	Large size pizza category contributed to maximum sales making an average of 45.89% of total sales.
### Best Customers by Revenue, Quantity and Total Order
-	The Thai Chicken pizza contributed to maximum sales with a total revenue.
-	The Classic Deluxe Pizza contributes to maximum total quantities sold and order.
### Worse Customers by Revenue, Quantity and Total Order
-	The Brie Carre Pizza has the lowest revenue, total quantity sold and orders.

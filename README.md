# Sales_Data_Analysis_PowerBI
Server: DESKTOP-Q0EFUBK

### KPI’s requirement

1. Total Revenue: Sum of total price of all pizza orders
    
    <aside>
    💡
    
    select SUM(total_price) as Total_revenue from pizza_sales;
    
    </aside>
    

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/6c68bb4c-8bff-40d7-aa02-6e56b5e78124/image.png)

1. Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.

<aside>
💡

select sum(total_price)/ count(distinct order_id) as Average_Order_Value from pizza_sales;

</aside>

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/827da682-c6fc-4049-8580-fac92fe4fd2b/image.png)

1. **Total Pizzas Sold:** The sum of the quantities of all pizzas sold

<aside>
💡

 select sum(quantity) as Total_pizza_sold from pizza_sales

</aside>

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/8b923b7f-79c7-4428-a89c-acbbb29b730e/image.png)

1. **Total Orders:** The total number of orders placed.

<aside>
💡

 select count(distinct order_id) as Total_Ordersfrom pizza_sales

</aside>

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/bc468380-c7e1-4adf-a820-7197f3eea890/image.png)

1. **Average Pizzas Per Order:** The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders. 

<aside>
💡

select CAST(CAST(sum(quantity) as DECIMAL(10,2)) / CAST(count(distinct order_id) as DECIMAL(10,2)) as DECIMAL(10,2)) as Average_pizza_sold_per_id from pizza_sales

</aside>

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/b19faabd-1324-4c3f-99f5-6add1e244204/image.png)

### **Chart Requirement**

1. **Daily Trend for Total Orders:**

Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.

<aside>
💡

select DATENAME(DW, order_date) as order_day, count(distinct order_id) as Total_Orders from pizza_sales GROUP BY DATENAME(DW, order_date)

</aside>

*DW date of week 'retrieve date week'*

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/47355838-b19d-4d6c-bfaa-2d83bc156740/image.png)

1. **Monthly Trend for Total Orders:**

Create a line chart that illustrates the monthly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.

<aside>
💡

SELECT DATENAME(MONTH, order_date) AS Order_Month,
COUNT(distinct order_id) as Total_Orders from pizza_sales GROUP BY DATENAME(MONTH, order_date) ORDER BY Total_Orders DESC;

</aside>

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/16e3162c-9264-488d-b3e9-819703c6da59/image.png)

1. Percentage of Sales by Pizza Category:

Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

<aside>
💡

SELECT pizza_category, SUM(total_price) as Total_Sales, SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales where MONTH(order_date) = 1) as Perc from pizza_sales
where MONTH(order_date) = 1
GROUP BY pizza_category

</aside>

*This is for January ‘It’s filtered using MONTH = 1’*

*If wanna do for ‘Quarter’ then, we use **DATEPART(QUARTER, order_date) = 1***

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/7e9f31a6-0810-4d13-b97e-ea044a677d00/image.png)

1. **Percentage of Sales by Pizza Size:**

Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.

<aside>
💡

SELECT pizza_size, SUM(total_price) as Total_Sales, CAST(SUM(total_price) * 100 / (SELECT SUM(total_price)
from pizza_sales ) AS DECIMAL(10,2)) as Perc from pizza_sales
GROUP BY pizza_size
ORDER BY Perc DESC

</aside>

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/285c3b67-e862-49ac-9048-bf1018ebb9b9/image.png)

1. **Top 5 Best Sellers by Total Pizzas Sold:**

Create a bar chart highlighting the top 5 best-selling pizzas based on the total number of pizzas sold. This chart will help us identify the most popular pizza options.

<aside>
💡

SELECT TOP 5 pizza_name, sum(total_price) AS Total_Rev from pizza_sales
GROUP BY pizza_name
ORDER BY Total_Rev DESC

</aside>

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/30e3bf08-ab27-41a6-a5e1-2c74cccd881f/image.png)

1. **Bottom 5 Worst Sellers by Total Pizzas Sold:**

Create a bar chart showcasing the bottom 5 worst-selling pizzas based on the total number of pizzas sold. This chart will enable us to identify underperforming or less popular pizza options.

<aside>
💡

SELECT TOP 5 pizza_name, sum(total_price) AS Total_Rev from pizza_sales
GROUP BY pizza_name
ORDER BY Total_Rev ASC

</aside>

![My Image](\Users\HP\OneDrive\Pictures\Screenshots\Screenshot 2025-01-22 192354.png)

1. Top Quantity Pizza

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/2d96f009-abcb-48bb-a0b4-398616cbf5f2/image.png)

### Dashboard in PowerBI

Using this data, I created PowerBI dashboards that visualize the busiest days and months along with sales performance. The dashboards also show which pizzas had the highest and lowest demand.

This is how my dashboard looks like:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/0f8b2041-d123-400a-97bc-c74f1f6dea70/image.png)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ac6299d3-d945-4187-bab5-09cb0952ed52/a5dbac14-a266-44ab-a568-67b69608dda6/image.png)

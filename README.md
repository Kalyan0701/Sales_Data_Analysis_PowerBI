## Pizza Data (SQL & PowerBI)

### KPI Requirements
Total Revenue:
The total revenue is the sum of the total price of all pizza orders.
Query:
sql
```
SELECT SUM(total_price) AS Total_revenue FROM pizza_sales;
```
Average Order Value:
The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
Query:
sql
```
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS Average_Order_Value FROM pizza_sales;
```

Total Pizzas Sold:
The sum of the quantities of all pizzas sold.
Query:
sql
```
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
```
Total Orders:
The total number of orders placed.
Query:
sql
```
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
```

Average Pizzas Per Order:
The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.
Query:
sql
```
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Average_pizza_sold_per_id FROM pizza_sales;
```
### Chart Requirements
Daily Trend for Total Orders:
Create a bar chart displaying the daily trend of total orders over a specific time period.
Query:
sql
```
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales GROUP BY DATENAME(DW, order_date);
```
Monthly Trend for Total Orders:
Create a line chart that illustrates the monthly trend of total orders.
Query:
sql
```
SELECT DATENAME(MONTH, order_date) AS Order_Month, COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales GROUP BY DATENAME(MONTH, order_date) ORDER BY Total_Orders DESC;
```
Percentage of Sales by Pizza Category:
Create a pie chart that shows the distribution of sales across different pizza categories for a specific month (e.g., January).
Query:
sql
```
SELECT pizza_category, SUM(total_price) AS Total_Sales, 
       SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales WHERE MONTH(order_date) = 1) AS Perc 
FROM pizza_sales WHERE MONTH(order_date) = 1
GROUP BY pizza_category;
```

Percentage of Sales by Pizza Size:
Generate a pie chart that represents the percentage of sales attributed to different pizza sizes.
Query:
sql
```
SELECT pizza_size, SUM(total_price) AS Total_Sales, 
       CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS Perc 
FROM pizza_sales
GROUP BY pizza_size
ORDER BY Perc DESC;
```
Top 5 Best Sellers by Total Pizzas Sold:
Create a bar chart highlighting the top 5 best-selling pizzas based on the total number of pizzas sold.
Query:
sql
```
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Rev FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Rev DESC;
```

Bottom 5 Worst Sellers by Total Pizzas Sold:
Create a bar chart showcasing the bottom 5 worst-selling pizzas based on the total number of pizzas sold.
Query:
sql
```
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Rev FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Rev ASC;
```

Top Quantity Pizza:
A chart showcasing the pizza with the highest quantity sold.
Query:
sql
```
SELECT pizza_name, SUM(quantity) AS Total_Quantity FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity DESC;
```

## Dashboard in PowerBI
Using the data from the queries above, I created PowerBI dashboards to visualize key insights:

Busiest Days and Months: Identifying high-demand days and months.
Sales Performance: Visualizing total revenue, average order value, and more.
Best and Worst-Selling Pizzas: Showing top-performing and underperforming pizza options.
This dashboard will help track performance metrics and make informed decisions about sales strategies.

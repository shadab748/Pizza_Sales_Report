# Pizza_Sales_Report
The reports contain how pizza sales changes with respected to pizza category offerings and which time frame the restaurant gets more order

PIZZA SALES SQL QUERIES:
A.KPI’s:

1. Total Revenue:
select sum(total_price) as Total_Revenue from pizza_sales


2. Avg. Order Value:
select sum(total_price)/count(distinct order_id) as Avg_Order_Value from pizza_sales


3. Total Pizza Sold:
select sum(quantity) as Total_Pizza_Sold from pizza_sales


4.Total Order Places:
select count(distinct order_id) as Total_Orders from pizza_sales

 
5. Avg, Pizza Per Order:
select cast(cast (sum(quantity) as decimal(10,2))/cast(count(distinct order_id) as decimal(10,2)) as decimal(10,2)) as Avg_Pizza_Per_Order from pizza_sales

B. Chart Requirement.
1. Daily trends for total orders:
select DATENAME(DW,order_date) as Order_day, count(distinct order_id) as total_orders from pizza_sales
group by DATENAME(DW,order_date)

 
2.Monthly Trends for total orders.
select DATENAME(month,order_date) as Month_name, count(distinct order_id) as total_orders from pizza_sales
group by DATENAME(month,order_date) order by total_orders desc



3. Percentage of Sales by Pizza Category:
select pizza_category, sum(total_price) as Total_price ,sum(total_price) *100/(select sum(total_price) from pizza_sales where month(order_date)=1) as  '%_of Sales' from pizza_sales 
group by pizza_category


4. Percentage of Sales by Pizza Size:
select pizza_size, cast(sum(total_price)  as decimal(10,2)) as Total_sale ,cast(sum(total_price) *100/(select sum(total_price) from pizza_sales where DATEPART(quarter, order_date) =1) as decimal(10,2))as  '%_of Sales' from pizza_sales 
where DATEPART(quarter, order_date) =1
group by pizza_size order by '%_of Sales' desc

5. Top 5 Best Seller by revenue, total qty, and total orders:
5.1 Top 5 best seller by revenue:
select top(5) pizza_name, sum(total_price) as total_revenue from pizza_sales
group by pizza_name
order by total_revenue desc


5.2 Top 5 best seller by qty:
select top(5) pizza_name, sum(quantity) as total_qty from pizza_sales
group by pizza_name
order by total_qty desc


5.3 Top 5 best seller by total orders:
select top(5) pizza_name, sum(distinct order_id) as total_orders from pizza_sales
group by pizza_name
order by total_orders desc




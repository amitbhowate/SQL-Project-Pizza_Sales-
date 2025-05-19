# SQL-Project-Pizza_Sales-
After creating the Dashboard in power bi then the testing process start check the value are correct or not by writing some sql query

 Objective : Testing the value in Dashboard are correct or not

Performing some sql query :
KPI (Key Performance Indicator)
 
TOTAL Revenue

select  
	  cast(sum(total_price) as numeric(10,2)) as Total_Revenue 
	  from pizza_table



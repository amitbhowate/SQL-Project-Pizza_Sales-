# SQL-Project-Pizza_Sales-
After creating the Dashboard in power bi then the testing process start check the value are correct or not by writing some sql query

# Objective : Testing the value in Dashboard are correct or not

# Performing some sql query :
--(Total_Revenue)--
 
select  
	  cast(sum(total_price) as numeric(10,2)) as Total_Revenue 
	  from pizza_table

--or--	  
select 
      sum(total_price)::numeric(10,2) as Total_Revenue from 
      pizza_table

--(Total_order)--

Select 
      count(order_id) as Total_order
	  from pizza_table

--(Avg_order_value)--


select 
        sum(total_price)/count(distinct(order_id))as avg_order_value
		from pizza_table

--(Total_pizza_sold)

Select 
      sum(quantity) as Total_pizza_sold 
	  from pizza_table

--(Avg_pizza_per_order)	

select 
       round(sum(quantity)/count(distinct(order_id))::numeric,2)  as Avg_pizza_per_order
	   from pizza_table


--(Daily Trends for Total_order)--

Select 

      to_char(order_date,'Day') as weekday,
	  count(distinct(order_id)) as Total_order
	  from pizza_table
	  group by 1
	  order by 2 asc

	   
--(Monthly Trends for Total_order)--

"""Alter table pizza_table
alter column order_date type timestamp"""

Select 
      to_char(order_date,'month')  as month_Trends,
	  count(distinct(order_id)) as Total_order
	  from pizza_table
	  group by 1
	  order by 2 desc,1 asc


--(Percantage of sale by pizza_category)--

select 
      pizza_category,
	  round(sum(total_price)::numeric,2) as Total_sale,
	  sum(Total_price)/(select sum(Total_price)from pizza_table)*100  as Pizza_sale
      from pizza_table
      group by 1
	  order by 2 asc
	  
---(Percentage  of sale by pizza_size)---- 
 select 
      pizza_size,
	  round(sum(total_price)::numeric,2) as Total_sale,
	  round((sum(Total_price)*100/(select sum(Total_price)from pizza_table))::numeric,2) as Pizza_sale
      from pizza_table
      group by 1
	  order by 2 asc




----Filter month wise----
select 
      pizza_category,
	  round(sum(total_price)::numeric,2) as Total_sale,
	  round(sum(Total_price)*100/(select sum(Total_price) from pizza_table))::numeric,2  as Percentage_Pizza_sale
      from pizza_table
      where extract(month from order_date) =1
      group by pizza_category




---(Top 5 by Revenue,Total_order,Total_qty)---

Select 
        Pizza_name,
        Round(sum(total_price)::numeric,2) as Top_5Total_Revenue
		from pizza_table
		group by 1
		order by 2 desc
		limit 5
		
Select 
        Pizza_name,
        Round(count(order_id)::numeric,2) as Top_5_Total_order
		from pizza_table
		group by 1
		order by 2 desc
		limit 5

Select 
        Pizza_name,
        Round(count(quantity)::numeric,2) as Top_5_Total_quantity
		from pizza_table
		group by 1
		order by 2 desc
		limit 5

---(bottom 5 by Revenue,Total_order,Total_qty)---

Select 
        Pizza_name,
        Round(sum(total_price)::numeric,2) as Top_5Total_Revenue
		from pizza_table
		group by 1
		order by 2 asc
		limit 5
		
Select 
        Pizza_name,
        Round(count(order_id)::numeric,2) as Top_5_Total_order
		from pizza_table
		group by 1
		order by 2 asc
		limit 5

Select 
        Pizza_name,
        Round(count(quantity)::numeric,2) as Top_5_Total_quantity
		from pizza_table
		group by 1
		order by 2 asc
		limit 5



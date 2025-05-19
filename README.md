# SQL-Project-Pizza_Sales-
After creating the Dashboard in power bi then the testing process start check the value are correct or not by writing some sql query

 Objective : Testing the value in Dashboard are correct or not

Performing some sql query :
KPI (Key Performance Indicator)
 
--(Total_Revenue)--
 
```
select  
cast(sum(total_price) as numeric(10,2)) as Total_Revenue 
from pizza_table

817860.05
````

--(Total_order)--

```
Select 
count(order_id) as Total_order
from pizza_table

48620
```

--(Avg_order_value)--

```
select 
sum(total_price)/count(distinct(order_id))as avg_order_value
from pizza_table

38.30
```

--(Total_pizza_sold)

```
Select   
sum(quantity) as Total_pizza_sold 
from pizza_table

49574
```

--(Avg_pizza_per_order)	
```
select 
round(sum(quantity)/count(distinct(order_id))::numeric,2)  as Avg_pizza_per_order
from pizza_table

2.32
```


--(Daily Trends for Total_order)--
```
Select 
 to_char(order_date,'Day') as weekday,
 count(distinct(order_id)) as Total_order
 from pizza_table
 group by 1
 order by 2 asc

"Sunday   "	2624
"Monday   "	2794
"Tuesday  "	2973
"Wednesday"	3024
"Saturday "	3158
"Thursday "	3239
"Friday   "	3538
```
	   
--(Monthly Trends for Total_order)--

```
Alter table pizza_table
alter column order_date type timestamp

'''Select 
      to_char(order_date,'month')  as month_Trends,
	  count(distinct(order_id)) as Total_order
	  from pizza_table
	  group by 1
	  order by 2 desc,1 asc


"july     "	1935
"may      "	1853
"january  "	1845
"august   "	1841
"march    "	1840
"april    "	1799
"november "	1792
"june     "	1773
"february "	1685
"december "	1680
"september"	1661
"october  "	1646
```

--(Percantage of sale by pizza_category)--

```
select 
pizza_category,
round(sum(total_price)::numeric,2) as Total_sale,
sum(Total_price)/(select sum(Total_price)from pizza_table)*100  as Pizza_sale
from pizza_table
group by 1
order by 2 asc

"Veggie"	193690.45	23.682590927384787
"Chicken"	195919.50	23.955137556847497
"Supreme"	208197.00	25.456311260098847
"Classic"	220053.10	26.905960255669907
	  
```

---(Percentage  of sale by pizza_size)---- 
```
 select 
 pizza_size,
 round(sum(total_price)::numeric,2) as Total_sale,
 round((sum(Total_price)*100/(select sum(Total_price)from pizza_table))::numeric,2) as Pizza_sale
 from pizza_table
 group by 1
 order by 2 asc

"XXL"	1006.60	0.12
"XL"	14076.00	1.72
"S"	178076.50	21.77
"M"	249382.25	30.49
"L"	375318.70	45.89
```
----Filter month wise----
```
select 
pizza_category,
round(sum(total_price)::numeric,2) as Total_sale,
round(sum(Total_price)*100/(select sum(Total_price) from pizza_table))::numeric,2  as Percentage_Pizza_sale
from pizza_table
where extract(month from order_date) =1
group by pizza_category

"Chicken"	16188.75	2	2
"Classic"	18619.40	2	2
"Supreme"	17929.75	2	2
"Veggie"	17055.40	2	2
```



---(Top 5 by Revenue,Total_order,Total_qty)---
```
Select 
Pizza_name,
Round(sum(total_price)::numeric,2) as Top_5Total_Revenue
from pizza_table
group by 1
order by 2 desc
limit 5
"The Thai Chicken Pizza"	43434.25
"The Barbecue Chicken Pizza"	42768.00
"The California Chicken Pizza"	41409.50
"The Classic Deluxe Pizza"	38180.50
"The Spicy Italian Pizza"	34831.25
```
```	
Select 
 Pizza_name,
 Round(count(order_id)::numeric,2) as Top_5_Total_order
 from pizza_table
 group by 1 
 order by 2 desc
 limit 5

 "The Classic Deluxe Pizza"	2416.00
"The Barbecue Chicken Pizza"	2372.00
"The Hawaiian Pizza"	2370.00
"The Pepperoni Pizza"	2369.00
"The Thai Chicken Pizza"	2315.00
```
```
Select 
Pizza_name,
Round(count(quantity)::numeric,2) as Top_5_Total_quantity
from pizza_table
group by 1
order by 2 desc
limit 5

"The Classic Deluxe Pizza"	2416.00
"The Barbecue Chicken Pizza"	2372.00
"The Hawaiian Pizza"	2370.00
"The Pepperoni Pizza"	2369.00
"The Thai Chicken Pizza"	2315.00
```

---(bottom 5 by Revenue,Total_order,Total_qty)---

 ```
Select      
Pizza_name,
Round(sum(total_price)::numeric,2) as bottom_5Total_Revenue
from pizza_table
group by 1
order by 2 asc
limit 5

"The Brie Carre Pizza"	11588.50
"The Green Garden Pizza"	13955.75
"The Spinach Supreme Pizza"	15277.75
"The Mediterranean Pizza"	15360.50
"The Spinach Pesto Pizza"	15596.00
```

```  
Select 
Pizza_name,
Round(count(order_id)::numeric,2) as bottom_5_Total_order
from pizza_table
group by 1
order by 2 asc
limit 5

"The Brie Carre Pizza"	480.00
"The Mediterranean Pizza"	923.00
"The Calabrese Pizza"	927.00
"The Spinach Supreme Pizza"	940.00
"The Spinach Pesto Pizza"	957.00
```
```
Select 
Pizza_name,
Round(count(quantity)::numeric,2) as bottom_5_Total_quantity
from pizza_table
group by 1
order by 2 asc
limit 5

"The Brie Carre Pizza"	480.00
"The Mediterranean Pizza"	923.00
"The Calabrese Pizza"	927.00
"The Spinach Supreme Pizza"	940.00
"The Spinach Pesto Pizza"	957.00
```





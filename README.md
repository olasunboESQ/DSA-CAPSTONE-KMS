# DSA-CAPSTONE-KULTRA MEGA STORES INVENTORY ANALYSIS

### This is an analysis for a a Store's Inventory from the year 2009-2012 using Structured Query Language (SQL)

As Business Intelligent Analyst employeed to suport the Abuja branch of the Store, the first step i took after being handed the 
Excel Dataset containing the order data from the year 2009-2012 was to critically clean my data using Microsoft Excel.

- [Project Overiew](#project-overview)

- [Analysis Tools](#analysis-tools)

- [OUTCOME OF ORDER_DATA USING Structured Query Language (SQL)](#outcome-of-order-data-using-structured-query-language-sql)

- [FINDINGS AND RECOMMENDATIONS](#findings-and-recommendations)


## Project Overiew

This is an Order Data from year 2009-2012, I am tasked with analyzing the Order Inventory of the store for 4 years.
I will use Structured Query Language to explore this Order Data in order to solve two (2) case scenarios.
The first critical step is to create a database unto which i imported the Order data of the store. 


 ## Analysis Tools

📁 - Structured Query Language. I am using this in the SQL Server Management [Download Here](https://www.microsoft.com)

## Outcome Of Order Data Using Structured Query Language

  👋 - Case Scenario One

I created a database called DSA_Project and i imported the excel order data into it as a table

 #### 1. Which product category had the highest sales?

 ```sql
SELECT TOP 1 PRODUCT_CATEGORY, 
SUM (SALES) AS TOTAL_SALES
FROM [dbo].[KMS Sql Case Study]
GROUP BY PRODUCT_CATEGORY
ORDER BY TOTAL_SALES ASC

```

- [Office Supplies,3752740
Q1.csv…]()

         
#### 2. What are the Top 3 and Bottom 3 regions in terms of sales?

```sql
SELECT TOP 3
REGION, SUM (SALES) AS
TOTAL_SALES FROM [dbo].[KMS Sql Case Study]
GROUP BY REGION 
ORDER BY TOTAL_SALES ASC

```

- [West,3597550
Ontario,3063221
Prarie,2837301
g Q2a.csv…]()

```sql
SELECT TOP 3
REGION, SUM (SALES) AS
TOTAL_SALES FROM [dbo].[KMS Sql Case Study]
GROUP BY REGION 
ORDER BY TOTAL_SALES DESC

```

- [Nunavut,116374
Northwest Territories,800850
Yukon,975865
g Q2.csv…]()

   
#### 3. What were the total sales of appliances in Ontario?

 ```sql
SELECT SUM (SALES) AS TOTAL_APPLIANCE_SALES
FROM[dbo].[KMS Sql Case Study]
WHERE Product_SUB_Category = 'APPLIANCES'
AND Region = 'ONTARIO'

```

- [202350
g Q3.csv…]()


- Total Sales of Appliances in Ontario is 202,350


#### 4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers

 ```sql
bottom 10 customers
select top 10 customer_name,
sum (sales)as total_sales
from[dbo].[KMS Sql Case Study]
group by Customer_Name 
order by total_sales asc

```

- [Jeremy Farry,2,86
Natalie DeCherney,1,126
Nicole Fjeld,2,153
Katrina Edelman,2,181
Dorothy Dickinson,1,198
Christine Kargatis,2,293
Eric Murdock,4,344
Chris McAfee,2,351
Rick Huthwaite,2,415
Mark Hamilton,1,451
4.csv…]()

- The management can introduce new offers or improve existing ones, they can also up-sell and cross-sell by encouraging the bottom 10 customers to purchase more products and get complementary items.


#### 5. KMS incurred the most shipping cost using which shipping method?

```sql
select top 1
Ship_Mode,
sum (shipping_cost) as total_shipping_cost
from[dbo].[KMS Sql Case Study]
group by Ship_Mode 
order by total_shipping_cost desc

```

- [Delivery Truck,51971.9397373199 Q5.csv…]()

- KMS incurred the most using Delivery Truck with shipping cost totalling 51971.940


### Case Scenario TWO

        6. Who are the most valuable customers, and what products or services do they typically purchase?

```sql
select customer_name, product_name, Order_Quantity,
sales
from[dbo].[KMS Sql Case Study]
where customer_name ='emily phan'
select top 1
customer_name, 
sum (sales) as total_spent 
from[dbo].[KMS Sql Case Study]
group by Customer_Name 
order by total_spent desc

```
- [Emily Phan,"O'Sullivan Elevations Bookcase, Cherry Finish",30,4012
Emily Phan,Bell Sonecor JB700 Caller ID,27,193
Emily Phan,Harmony HEPA Quiet Air Purifiers,33,362
Emily Phan,Fellowes Bankers Box™ Stor/Drawer® Steel Plus™,16,488
Emily Phan,Polycom ViewStation™ ISDN Videoconferencing Unit,13,89061
Emily Phan,TimeportP7382,40,6637
Emily Phan,Boston 1730 StandUp Electric Pencil Sharpener,16,336
Emily Phan,Heavy-Duty E-Z-D® Binders,11,127
Emily Phan,Hewlett-Packard Deskjet 1220Cse Color Inkjet Printer,39,14591
Emily Phan,Surelock™ Post Binders,44,1317
ng Q6.csv…]()


- [Emily Phan,117124 ng Q6B.csv…]()


 #### 7. Which small business customer had the highest sales?

```sql
select top 1
customer_name,
sum (sales) as highest_sales
from[dbo].[KMS Sql Case Study]
where Customer_Segment = 'small business'
group by Customer_Name 
order by highest_sales desc

```
- [Dennis Kane,75966 ng 7.csv…]()


  #### 8. Which Corporate Customer placed the most number of orders in 2009 – 2012?

```sql
select top 1
customer_name,
count(order_id) as total_orders
from[dbo].[KMS Sql Case Study]
where Customer_Segment ='corporate' and 
Order_Date between '2009-01-01' and '2012-12-31'
group by Customer_Name 
order by total_orders desc

```
- [Adam Hart,18 7.csv…]()

#### 9. Which consumer customer was the most profitable one?
```sql
select top 1
customer_name,
sum (profit)as total_profit
from[dbo].[KMS Sql Case Study]
where Customer_Segment = 'consumer'
group by Customer_Name 
order by total_profit  desc

```

- [Emily Phan,34005.4392166138 Q9.csv…]()


#### 10. Which customer returned items, and what segment do they belong to?
```sql
select distinct customer_name,
customer_segment
from[dbo].[KMS Sql Case Study] 
where status = 'returned'
select top 10 *
from[dbo].[KMS Sql Case Study] 
where status is not null

```
  - [Muhammed MacIntyre,Small Business,3,"Eldon Base for stackable storage shelf, platinum"
Claudia Miner,Small Business,933,"Wilson Jones 1"" Hanging DublLock® Ring Binders"
Allen Rosenblatt,Small Business,998,"#10-4 1/8"" x 9 1/2"" Premium Diagonal Seam Envelopes"
Grant Carroll,Small Business,2275,Col-Erase® Pencils with Erasers
Brad Eason,Small Business,3232,XtraLife® ClearVue™ Slant-D® Ring Binders by Cardinal
Nicole Hansen,Small Business,3524,Computer Printout Paper with Letter-Trim Perforations
Nicole Hansen,Small Business,8419,Xerox 1936
Nicole Hansen,Small Business,8419,Xerox 214
Nicole Hansen,Small Business,8833,Carina Double Wide Media Storage Towers in Natural & Black
Delfina Latchford,Small Business,15108,Xerox 1893
ng q10.csv…]()

- Over 500 customers returned items


#### 11. If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one,do you think
####     the company appropriately spent shipping costs based on the Order Priority? Explain your answer.

```sql
select ship_mode,
 order_priority, 
 count (*) as order_count,
 ROUND(avg(shipping_cost),2) as avgshipcost
 from[dbo].[KMS Sql Case Study]
 group by ship_mode, Order_Priority
 order by Order_Priority,avgshipcost asc

```
- [q11.csv](https://github.com/user-attachments/files/21033786/q11.csv)


- There is a significant inconstitencies in the alignment between priority order and shipping mode. The company did not appropriately spend shipping costs based on the order priority as some shippingmodes do not match urgency for some critical orders.


## FINDINGS AND RECOMMENDATIONS.

- Generally speaking the Kultra Mega Stores order data for 2009-2012 showed that some customers ordered more overtime while some did not.

- Also some customer Segment thrived more than orders based on the product/services purchased and profit made.

- The company can do more in the area of advertisment, complementary gifts or raffle draw promos to boost their sales overtime.

- There is also need to align shipping mode with the order priority to improve the profit base margin. This will aslo curb unnecessary cost inflation of shipping cost.

- Strategic improvement in shipping decision can result in cost saving and improved service reliability.



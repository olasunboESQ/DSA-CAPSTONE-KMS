# DSA-CAPSTONE-KULTRA MEGA STORES INVENTORY ANALYSIS

### This is an analysis for a a Store's Inventory from the year 2009-2012 using Structyred Query Language (SQL)

As Business Intelligent Analyst employeed to suport the Abuja branch of the Store, the first step i took after being handed the 
Excel Dataset containing the order data from the year 2009-2012 was to critically clean my data using Microsoft Excel.

- [Project Overiew](#project-overview)

- [Analysis Tools](#analysis-tools)

- [OUTCOME OF Order Data USING MICROSOFT EXCEL](#outcome-of-order-data-using-microsoft-excel)

- [OUTCOME OF ORDER_DATA USING Structured Query Language (SQL)](#outcome-of-order-data-using-structured-query-language-sql)

- [FINDINGS AND RECOMMENDATIONS](#findings-and-recommendations)


## Project Overiew

This is an Order Data from year 2009-2012, I am tasked with analyzing the Order Inventory of the store for 4 years.
I will use Structured Query Language to explore this Order Data in order to solve two (2) case scenarios.
The first critical step is to create a database unto which i imported the Order data of the store. 


## Analysis Tools

- Microsoft Excel [Download Here](https://www.microsoft.com)
- Structured Query Language

### Case Scenario One

I created a database called DSA_Project and i imported the excel order data into it as a table

    1. Which product category had the highest sales?

 ```sql
SELECT TOP 1 PRODUCT_CATEGORY, 
SUM (SALES) AS TOTAL_SALES
FROM [dbo].[KMS Sql Case Study]
GROUP BY PRODUCT_CATEGORY
ORDER BY TOTAL_SALES ASC

```
       
    2. What are the Top 3 and Bottom 3 regions in terms of sales?

```sql
SELECT TOP 3
REGION, SUM (SALES) AS
TOTAL_SALES FROM [dbo].[KMS Sql Case Study]
GROUP BY REGION 
ORDER BY TOTAL_SALES ASC

SELECT TOP 3
REGION, SUM (SALES) AS
TOTAL_SALES FROM [dbo].[KMS Sql Case Study]
GROUP BY REGION 
ORDER BY TOTAL_SALES DESC

```

    3. What were the total sales of appliances in Ontario?

 ```sql
SELECT SUM (SALES) AS TOTAL_APPLIANCE_SALES
FROM[dbo].[KMS Sql Case Study]
WHERE Product_SUB_Category = 'APPLIANCES'
AND Region = 'ONTARIO'

```

    4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers

 ```sql
bottom 10 customers
select top 10 customer_name,
sum (sales)as total_sales
from[dbo].[KMS Sql Case Study]
group by Customer_Name 
order by total_sales asc

```

    5. KMS incurred the most shipping cost using which shipping method?

```sql
select top 1
Ship_Mode,
shipping_cost
from[dbo].[KMS Sql Case Study]
order by Shipping_Cost

```

### Case Scenario TWO

        6. Who are the most valuable customers, and what products or services do they typically purchase?

```sql

select top 1
customer_name, 
sum (sales) as total_spent 
from[dbo].[KMS Sql Case Study]
group by Customer_Name 
order by total_spent desc

```
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
- The most valuable customer is EMILY PHAN as she spent a total of 117,124 and the item
she purchased most is "O'Sullivan Elevations Bookcase, Cherry Finish" with a total order of Thirty (30)

   7. Which small business customer had the highest sales?

```sql
select top 1
customer_name,
sum (sales) as highest_sales
from[dbo].[KMS Sql Case Study]
where Customer_Segment = 'small business'
group by Customer_Name 
order by highest_sales desc

```
- DENNIS KANE is the small business customer with the highest sales with 75,966.
  
      8. Which Corporate Customer placed the most number of orders in 2009 – 2012?

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
- ADAM HART is the corporate customer who placed 27 orders in 2009-2012

       9. Which consumer customer was the most profitable one?
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
- EMILY PHAN was the most profitable consumer customer with 3,401

       10. Which customer returned items, and what segment do they belong to?
```sql
select distinct customer_name,
customer_segment, order_id
from[dbo].[KMS Sql Case Study]
where status ='returned'
order by Customer_Segment desc

```
  - One Hundred and Eight (108) customers from Small Business returned items
  - Ninety-Four (94) customers from Home Office returned items
  - Two Hundred and Seventy-Eight (278) from corporate returned items
  - SixtyTwo (62) customers from Consumer Segment returned Items
Totalling 542 customers that returned items.


        11. If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one,
            do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer.

```sql
select ship_mode,
 order_priority, 
 count (*) as order_count,
 ROUND(avg(shipping_cost),2) as avgshipcost
 from[dbo].[KMS Sql Case Study]
 group by ship_mode, Order_Priority
 order by Order_Priority,avgshipcost asc

```
-  From the response from the queryabove, the company has a serious cost efficeincy issue as the delivery Truck which is the slowest and should be the most economical is extremely expensive with aveage cost of 44-47. 
-  This result shows that Regular Air is the most cost effective while Express Air is still resonable. The Delivery Truck which should be the cheapest is now extremely expensive and its usage for Critical Order is counterintuitive. Also a significant number of Low priority orders used Express Air inflating the costs unnecessarily, while Critical orders used Delivery Truck, risking customer's dissatifaction.     



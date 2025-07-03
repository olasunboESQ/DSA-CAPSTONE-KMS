[q10.csv](https://github.com/user-attachments/files/21032756/q10.csv)[Q9.csv](https://github.com/user-attachments/files/21032633/Q9.csv)[Q6B.csv](https://github.com/user-attachments/files/21032570/Q6B.csv)[Q6.csv](https://github.com/user-attachments/files/21032534/Q6.csv)[Q6.csv](https://github.com/user-attachments/files/21032418/Q6.csv)[Q5.csv](https://github.com/user-attachments/files/21032334/Q5.csv)[Q3.csv](https://github.com/user-attachments/files/21032276/Q3.csv)[Q3.csv](https://github.com/user-attachments/files/21032153/Q3.csv)[Q4.csv](https://github.com/user-attachments/files/21032149/Q4.csv)# DSA-CAPSTONE-KULTRA MEGA STORES INVENTORY ANALYSIS

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

- Structured Query Language. I am using this in the SQL Server Management [Download Here](https://www.microsoft.com)

## Outcome Of Order Data Using SQL

- Case Scenario One

I created a database called DSA_Project and i imported the excel order data into it as a table

    1. Which product category had the highest sales?

 ```sql
SELECT TOP 1 PRODUCT_CATEGORY, 
SUM (SALES) AS TOTAL_SALES
FROM [dbo].[KMS Sql Case Study]
GROUP BY PRODUCT_CATEGORY
ORDER BY TOTAL_SALES ASC

```

- [Office Supplies,3752740
Q1.csv…]()

         
    2. What are the Top 3 and Bottom 3 regions in terms of sales?

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

   
    3. What were the total sales of appliances in Ontario?

 ```sql
SELECT SUM (SALES) AS TOTAL_APPLIANCE_SALES
FROM[dbo].[KMS Sql Case Study]
WHERE Product_SUB_Category = 'APPLIANCES'
AND Region = 'ONTARIO'

```

- [202350
g Q3.csv…]()

- Total Sales of Appliances in Ontario is 202,350


    4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers

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


    5. KMS incurred the most shipping cost using which shipping method?

```sql
select top 1
Ship_Mode,
sum (shipping_cost) as total_shipping_cost
from[dbo].[KMS Sql Case Study]
group by Ship_Mode 
order by total_shipping_cost desc

```

- [Delivery Truck,51971.9397373199
 Q5.csv…]()

- KMS incurred the most using Delivery Truck with shipping cost totalling 51971.940


### Case Scenario TWO

        6. Who are the most valuable customers, and what products or services do they typically purcha

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
sum (profit)as total_profit
from[dbo].[KMS Sql Case Study]
where Customer_Segment = 'consumer'
group by Customer_Name 
order by total_profit  desc

```

- [UploadingEmily Phan,34005.4392166138 Q9.csv…]()


       10. Which customer returned items, and what segment do they belong to?
```sql
select distinct customer_name,
customer_segment
from[dbo].[KMS Sql Case Study] 
where status = 'returned'
select top 10 *
from[dbo].[KMS Sql Case Study] 
where status is not null

```
  - [q10.csv](https://github.com/user-attachments/files/21032831/q10.csv)
over 500 customers returned items


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
-  [q11.csv](https://github.com/user-attachments/files/21033043/q11.csv)
Critical,Delivery Truck,228,47.2974559131422,1218332.07,1
Critical,Express Air,200,8.71049994021654,197990.83,1
Critical,Regular Air,1180,7.27691522180024,1118846.23,1
High,Delivery Truck,248,45.1890320047255,1338510.57,1
High,Regular Air,1308,7.64909018334628,1306961.6,1
High,Express Air,212,6.85627354287876,201587.18,1
Low,Delivery Truck,250,44.5264397354126,1313679.83,3
Low,Express Air,190,8.16647367257821,190534.53,4
Low,Regular Air,1280,8.01845309105702,1360362.74,4
Medium,Delivery Truck,205,46.154243780927,969386.41,1
Medium,Express Air,201,8.12731339712048,244812.12,1
Medium,Regular Air,1225,7.68875099240517,1260243.74,1
Not Specified,Delivery Truck,215,43.6651625256206,1080840.25,1
Not Specified,Express Air,180,8.16699995663431,194372.03,1
Not Specified,Regular Air,1277,7.62261547660492,1257786.89,1




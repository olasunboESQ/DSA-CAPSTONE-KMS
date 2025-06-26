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


## Analysis Tools

- Microsoft Excel [Download Here](https://www.microsoft.com)
- Structured Query Language

- Case Scenario One

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

    5. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers

    6. KMS incurred the most shipping cost using which shipping method?

  


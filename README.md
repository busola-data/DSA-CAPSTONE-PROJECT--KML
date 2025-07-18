# DSA-CAPSTONE-PROJECT--KMS
## Company Overview 

Kultra Mega Stores (KMS), headquartered in Lagos, specialises in office supplies and 
furniture. Its customer base includes individual consumers, small businesses (retail), and 
large corporate clients (wholesale) across Lagos, Nigeria.

### PROJECT OVERVIEW
This documentation contains various structured query languages detailing;
-  The sales activities for the period analyzed
-  Show-casing the consumer behaviour of the various customer of the company
-  And the various transport system deployed by the company.

  ### DATA COLLECTED
The data set includes the following key columns;
- Order ID: This is a unique number that is assigned to differentiate products being ordered for
- Order Date: This shows the date order is placed 
- Order Quantity: This shows the number of products ordered
- Sales: This is price multiply by quantity 
- Ship Mode: This shows the various transportation means deployed by KMS Company to deliver products as requested by customers 

### TOOLS USED
- Microsoft Excel-csv
- SQL


### DATA ANALYZED
The following syntax query language is used to answer the underlined questions:
```` SQL
CREATE DATABASE KMS_db

Which product category had the highest sales?

select product_category,
sum(sales) AS total_sales
from [dbo].[KMS Sql Case Study]
GROUP BY 
product_category
ORDER BY 
total_sales desc;

What are the Top 3 and Bottom 3 regions in terms of sales?

SELECT TOP 3 REGION,
SUM(SALES) AS TOTAL_SALES
FROM [dbo].[KMS Sql Case Study]
GROUP BY REGION
ORDER BY
TOTAL_SALES desc;

Bottom 3 regions in terms of sales?
SELECT top 3 REGION,
SUM(SALES) AS TOTAL_SALES
FROM [dbo].[KMS Sql Case Study]
GROUP BY REGION
ORDER BY
TOTAL_SALES asc;


What were the total sales of appliances in Ontario?

SELECT REGION,
SUM(SALES) AS TOTAL_APPL_ONTARIO
FROM [dbo].[KMS Sql Case Study]
WHERE PRODUCT_SUB_CATEGORY ='Appliances'
AND PROVINCE ='ONTARIO'
GROUP BY REGION;


Advise the management of KMS on what to do to increase the revenue from the bottom
10 customers

SELECT TOP 10 
CUSTOMER_NAME,product_category,
SUM(sales) AS TOTAL_SALES
FROM [dbo].[KMS Sql Case Study]
GROUP BY CUSTOMER_NAME,product_category
ORDER BY TOTAL_SALES ASC;


 KMS incurred the most shipping cost using which shipping method?

 SELECT TOP 1 SHIP_MODE,
 SUM(SHIPPING_COST) AS TOTAL_SHIPPING_COST
 FROM [dbo].[KMS Sql Case Study]
 GROUP BY SHIP_MODE
 ORDER BY TOTAL_SHIPPING_COST DESC;


 Who are the most valuable customers, and what products or services do they typically
purchase?

SELECT CUSTOMER_NAME,PRODUCT_NAME,PRODUCT_CATEGORY,
SUM(SALES) AS TOTAL_PURCHASE
FROM [dbo].[KMS Sql Case Study]
GROUP BY CUSTOMER_NAME,PRODUCT_NAME,PRODUCT_CATEGORY
ORDER BY TOTAL_PURCHASE DESC;


Which small business customer had the highest sales?

SELECT TOP 1 CUSTOMER_NAME,CUSTOMER_SEGMENT,
SUM ([SALES]) AS [TOTAL SALES]
FROM [dbo].[KMS Sql Case Study]
WHERE CUSTOMER_SEGMENT='SMALL BUSINESS'
GROUP BY CUSTOMER_NAME,CUSTOMER_SEGMENT
ORDER BY [TOTAL SALES] DESC;


 Which Corporate Customer placed the most number of orders in 2009 – 2012?

 SELECT TOP 1 CUSTOMER_NAME,CUSTOMER_SEGMENT,
 COUNT(ORDER_ID) AS TOTAL_ORDERS
FROM [dbo].[KMS Sql Case Study]
WHERE CUSTOMER_SEGMENT='CORPORATE'
AND ORDER_DATE BETWEEN'2009'AND '2012'
GROUP BY CUSTOMER_NAME,CUSTOMER_SEGMENT
ORDER BY TOTAL_ORDERS DESC;


Which consumer customer was the most profitable one? 

SELECT TOP 1 CUSTOMER_NAME,CUSTOMER_SEGMENT,
SUM(PROFIT) AS TOTAL_PROFIT 
FROM [dbo].[KMS Sql Case Study]
WHERE CUSTOMER_SEGMENT='CONSUMER'
GROUP BY CUSTOMER_NAME,CUSTOMER_SEGMENT
ORDER BY TOTAL_PROFIT DESC;

Which customer returned items, and what segment do they belong to? 


SELECT CUSTOMER_NAME,CUSTOMER_SEGMENT,
[STATUS] 
FROM [dbo].[KMS Sql Case Study]
JOIN [dbo].[Order_Status]
ON [dbo].[KMS Sql Case Study].ORDER_ID=
[dbo].[Order_Status].[ORDER_ID]

If the delivery truck is the most economical but the slowest shipping method and 
Express Air is the fastest but the most expensive one, do you think the company 
appropriately spent shipping costs based on the Order Priority? Explain your answer

SELECT ORDER_PRIORITY,SHIP_MODE,
COUNT(ORDER_ID) AS ODER_COUNT,
SUM(SALES-PROFIT) AS ESTIMATED_SHIPPING_COST,
AVG(DATEDIFF(DAY,[ORDER_DATE],
[SHIP_DATE])) AS AVG_SHIP_DATE
FROM [dbo].[KMS Sql Case Study]
GROUP BY ORDER_PRIORITY,SHIP_MODE
ORDER BY ORDER_PRIORITY,SHIP_MODE DESC;


  

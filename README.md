# Incubator Hub Data Capstone-Project II
This is am Inventory Analysis of Kultra Mega Store (KMS), based on available data from 2009 - 2012

## Project Topic: Kultra Mega Stores Inventory Analysis

### Project Overview

Kultra Mega Stores (KMS), headquartered in Lagos, specializes in office supplies and furnitures. Its customer base includes individual customers, small businesses (retail), and large corporate clients (wholesale), across Lagos, Nigeria

The Abuja division is needing some business intelligence support in other to scale up in its operation. 

Therefore, a business data of its operation between 2009 and 2012 has just been shared to provide key insights and findings that can enhance the business operation

### My Data sources

The primary data sources are the “**KMS Case Study**” and “**Order Status**”, both _**CSV files**_

### Tool Used

-	Microsoft SQL Server for Data collection
-	Microsoft SQL Server for
  
    o	Data Loading
 	
 	  o	Data Formatting

    o	Data Querying

    o	Data Analysis

### Data Cleaning /Preparation

At the initial stage, we performed the following

-	Data inspection and formatting
-	Removal of “Null” value rows
-	Data loading

### Exploratory Data Analysis

The data was explored to get answers to some questions like:

#### Scenario I

1.	Which product category had the highest sales?
2.	What are the Top 3 and Bottom 3 regions in terms of sales?
3.	What were the total sales of appliances in Ontario
4.	Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
5.	KMS incurred the most shipping cost using what method?

#### Scenario II

6.	Who are the most valuable customers and what products or services do they typically purchase?
7.	What small business customers had the highest sales?
8.	Which Corporate Customer placed the greatest number of orders from 2009 – 2012?
9.	Which Consumer Customer was the most profitable?
10.	Which Customers returned items, and what segment do they belong to?
11.	If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer

### Data Analysis/Insights

~~~ SQL
Select * from [KMS Sales Table]
~~~

<img width="580" alt="image" src="https://github.com/user-attachments/assets/83561c40-8e2e-4e24-a8f1-52b3243fb14d" />

_**Question 1**_

~~~ SQL

----Product Category with Highest Sales------

Select Product_Category, sum (Sales) as [Highest Sales]
from [KMS Sales Table] 
group by Product_Category
Order by [Highest Sales] desc
~~~

<img width="268" alt="image" src="https://github.com/user-attachments/assets/6795cbdb-70a2-4f97-aea4-95b330e881ba" />

_**Question 2a**_

~~~ SQL
----Top 3 Region in terms of Sales----

Select top 3 Region, sum (Sales) as [Top 3 Region in Sales]
from [KMS Sales Table]
group by Region
Order by [Top 3 Region in Sales] desc
~~~

<img width="215" alt="image" src="https://github.com/user-attachments/assets/08482d36-7ce7-43fd-a727-935bd4a4c2fe" />

_**Question 2b**_

~~~ SQL
-----Bottom 3 Region in terms of Sales-----

Select top 3 Region, sum (Sales) as [Bottom 3 Region in Sales]
from [KMS Sales Table]
group by Region
Order by [Bottom 3 Region in Sales] asc
~~~

<img width="243" alt="image" src="https://github.com/user-attachments/assets/0edfe1d5-adbd-42ba-8c2c-e20e99647908" />

_**Question 3**_

~~~ SQL
----Total Sales of Appliances in Ontario-------

Select Region, Product_Sub_Category, sum (Sales) as [Total Sales]
from [KMS Sales Table]
where Region = 'Ontario' and Product_Sub_Category = 'Appliances'
group by Region, Product_Sub_Category
~~~

<img width="247" alt="image" src="https://github.com/user-attachments/assets/e41a9943-74e5-4fc3-9b56-6b8a111096b9" />

_**Further Analysis**_

~~~ SQL
----Total Number of Customers-----They are 795 Altogether---

Select count (distinct Customer_Name) as [Total Customer base]
from [KMS Sales Table]

----Analysing Total Number of Product-----They are 1263

Select count (distinct Product_Name) as [Total Number of Product]
from [KMS Sales Table]

----Analysing Total Number of Product Sub Category-----They are 17

Select count (distinct Product_Sub_Category) as [Total Product Sub Category]
from [KMS Sales Table]
~~~

~~~ SQL
----Analysing Top 5 Selling Product Sub Category-----

Select top 5 Product_Sub_Category, sum (Sales) as [Total Sales]
from [KMS Sales Table]
group by Product_Sub_Category
Order by [Total Sales] desc
~~~

<img width="293" alt="image" src="https://github.com/user-attachments/assets/e92729d8-ec3e-4f84-8ee4-a097813d1124" />

~~~ SQL
----Bottom 10 Customers Sales Value-----

Select top 10 Customer_Name, sum (Sales) as [Total Sales]
from [KMS Sales Table]
group by Customer_Name
Order by [Total Sales] asc
~~~

<img width="257" alt="image" src="https://github.com/user-attachments/assets/e392a55c-a443-43c4-be84-32433f83df07" />

_**Question 4**_

KMS have a total Customer base of **795**. It has **1263** different product lines in **17 Sub-Categories**, out of which **5 Sub-Categories** are identified to record highest Sales. 

Therefore, the bottom 10 Customers should be developed to focus their sales more on these 5 sub-categories

_**Question 5**_

~~~ SQL
----Analysing the various Shipping Mode and their Cost---

Select Ship_Mode, sum (Shipping_Cost) as [Total Shipping Cost]
from [KMS Sales Table]
Group by Ship_Mode
Order by [Total Shipping Cost] desc
~~~

<img width="264" alt="image" src="https://github.com/user-attachments/assets/775c0989-c373-4074-96bc-685d0cd76fe3" />

KMS incurred the most cost from **Delivery Truck**

#### Scenario II

_**Question 6**_

~~~ SQL
---Top 10 Customers and their Product Sub-Category----

Select top 10 Customer_Name, Product_Category, Product_Sub_Category, sum(Sales) as [Total Sales]
from [KMS Sales Table]
group by [Product_Category], [Product_Sub_Category], Customer_Name
Order by [Total Sales] desc
~~~

<img width="391" alt="image" src="https://github.com/user-attachments/assets/7663c200-43eb-4e7a-a20a-5bbd81c8f507" />

_**Question 7**_

~~~ SQL
---Analysis of the Small business Customer with the Highest Sales---

Select top 1 Customer_Name, Customer_Segment, sum (Sales) as [Total Sales]
from [KMS Sales Table]
where Customer_Segment = 'Small Business'
group by Customer_Name, Customer_Segment
Order by [Total Sales] desc
~~~

<img width="272" alt="image" src="https://github.com/user-attachments/assets/60743f79-4503-4f46-867f-4cdca5362b2d" />

The Small Business with the highest Sales is **Dennis Kane**

_**Question 8**_

~~~ SQL
---Analysis of Corporate Customer with the most order from 2009 - 2012---

Select top 1 Customer_Name, Customer_Segment, sum (Order_Quantity) as [Total Order]
from [KMS Sales Table]
where Customer_Segment = 'Corporate'
group by Customer_Name, Customer_Segment
Order by [Total Order] desc
~~~

<img width="270" alt="image" src="https://github.com/user-attachments/assets/aef17e55-2090-46c4-aa1a-fad6ddba17f0" />

The Corporate Customer with the most order is **Roy Skaria** with **773** orders

_**Question 9**_

~~~ SQL
---Analysis of the most profitable Consumer----

Select top 1 Customer_Name, Customer_Segment, sum (Profit) as [Total Profit]
from [KMS Sales Table]
where Customer_Segment = 'Consumer'
group by Customer_Name, Customer_Segment
Order by [Total Profit] desc
~~~

<img width="299" alt="image" src="https://github.com/user-attachments/assets/af152fc2-4e2f-4e65-a91c-d48295de0f33" />

The most profitable Consumer customer is **Emily Phan**

_**Question 10**_

To determine customer that returned product, we need to **join** KMS Sales table and the KMS Return table using the **primary key Order ID**

~~~ SQL
Create view vw_SalesOrder_tbl
as
Select [KMS Sales Table].Customer_Name,
	   [KMS Sales Table].Order_ID,
	   [KMS Sales Table].Order_Quantity,
	   [KMS Sales Table].Customer_Segment,
	   [KMS Return Table].[Status]
from [KMS Sales Table]
join [KMS Return Table]
on [KMS Return Table].Order_ID = [KMS Sales Table].Order_ID

select * from vw_SalesOrder_tbl

~~~

<img width="356" alt="image" src="https://github.com/user-attachments/assets/6b3065ca-b445-449b-b849-91b21698fda9" />

These are the Customers that returned items and their Customer Segment

~~~ SQL
Select Customer_Name, Customer_Segment, [Status]
from vw_SalesOrder_tbl
~~~

<img width="269" alt="image" src="https://github.com/user-attachments/assets/09700077-d582-45fe-afdf-c7fe3b0f7626" />

_**Question 11**_

Based on the Total Shipping Cost in Case Study 1, It is obvious that KMS spent the highest on "**Delivery Truck**" shipping most, which is considered the cheapest while they spent least on "**Express Air**" which the most expensive of the three, so I believe the company was able to appropriately manage their shipping based on the order priority

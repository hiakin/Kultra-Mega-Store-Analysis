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
----Total Number of Customers-----They 795 Altogether---

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




# DSA-KMS-Project

This is one of the final project for the DSA program that I have been on for the past 3 months ago before now. I'm excited to have started this baby steps journey with DSA.

## Project Topic: Kultra Mega Stores Inventory

### Project Overview

For this data analysis project, the primary objective aims at the supporting strategic and operational decision-making for the Abuja division of KMS by analyzing historical order data dated from 2009 to 2012. This analysis will uncover key business insights that can drive growth, improve operational efficiency, and enhance customer service.

### Data Source

The primary source of the data used in the project is from DSA LMS platform on canvas.

### Tool used 

- SQL Server (For querying and analysis) [Download here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)

### Analysis

#### Case Scenario I

  - To get product category with the highest sales
    
  ``` SQL
    SELECT 
    Product_category, 
    SUM(Sales) AS Total_Sales
    FROM 
    [dbo].[KMS Sql Case Study]
    GROUP BY 
    Product_category
    ORDER BY 
    Total_Sales DESC
  ```

  - To get top 3 regions and buttom 3 region in terms of sales

    ``` SQL
      SELECT TOP 3
    	Region, sum(Sales) as total_sales
      FROM [dbo].[KMS Sql Case Study]
      GROUP BY Region
      order by total_sales desc;
      
      
      SELECT TOP 3
      	Region, sum(Sales) as total_sales
      FROM [dbo].[KMS Sql Case Study]
      GROUP BY Region
      order by total_sales ASC
    ```
    
  - To get the total sales of appliances in Ontario

    ```SQL
      SELECT 
    	Region, sum(Sales)as total_sales , Product_Sub_Category
      FROM [dbo].[KMS Sql Case Study]
      WHERE REGION = 'ONTARIO'and Product_Sub_Category='Appliances'
      GROUP BY Region,Product_Sub_Category
      order by total_sales
    ```

  - Advise on what KMS management can do to increase the revenue from the bottom 10 customers

    ```SQL
     select top 10
    Customer_Name,product_Name,product_category ,Order_Priority,Ship_Mode,Shipping_Cost,
    sum(Profit) as total_profit
    from [dbo].[KMS Sql Case Study]
    group by Customer_Name,product_Name,product_category, Order_Priority,Ship_Mode,Shipping_Cost
    order by total_profit asc
    Answer:The company needs to quickly reassess its pricing, shipping, and customer strategy. The current losses from low-priority customers using expensive shipping options show operational inefficiencies. To improve performance, management should align shipping methods with order priority, evaluate product profit margins, and revise any customer deals that lead to losses.
    ```

  - To get most shipping cost method
    
    ```SQL
      select* from[dbo].[KMS Sql Case Study] 

      select 
      ship_mode,sum (shipping_cost)as total_cost
      from [dbo].[KMS Sql Case Study]
      group by ship_mode
      order by total_cost desc
    ```

#### Case Scenario II

  - The most valuable customers, and products or services they typically purchase

    ``` SQL
    select top 10
    Customer_Name,product_Name,sum(Profit) as total_profit
    from [dbo].[KMS Sql Case Study]
    group by Customer_Name, product_Name
    order by total_profit desc
    ```

  - Small business customer with the highest sales
    
    ``` SQL
    select top 1
    customer_name, customer_segment, sum(sales) as highest_sales
    from[dbo].[KMS Sql Case Study]
    where customer_segment='Small business'
    group by customer_name,customer_segment
    order by highest_sales desc
    ```

  - Corporate Customer with the most number of orders placed in 2009 – 2012

    ``` SQL
    select top 1
    Customer_Name,Customer_Segment,count (distinct Order_year)as sumed_year,
    sum(Order_Quantity)as most_Orders
    from [dbo].[KMS Sql Case Study]
    where Customer_Segment='Corporate' 
    group by Customer_Name,Customer_Segment
    order by most_Orders desc
    ```

  - The most profitable consumer customer

    ``` SQL
    select top 1
    customer_name, customer_segment, sum (profit) as most_profitable
    from[dbo].[KMS Sql Case Study]
    where customer_segment= 'Consumer'
    group by customer_name, customer_segment
    order by most_profitable desc
    ```

  - Customer who returned items, and the segment they belong to

    ``` SQL
    select distinct
    [dbo].[KMS Sql Case Study].Order_ID,
    [dbo].[KMS Sql Case Study].Customer_Name,
    [dbo].[KMS Sql Case Study].Customer_Segment,
    [dbo].[Order_Status].Status
    from[dbo].[KMS Sql Case Study]
    inner join [dbo].[Order_Status]
    on [dbo].[Order_Status].Order_ID=[dbo].[KMS Sql Case Study].Order_ID
    ```

  - If the delivery truck is the most economical but the slowest shipping method and
Express Air is the fastest but the most expensive one, do you think the company
appropriately spent shipping costs based on the Order Priority? Explain your answer

    ``` SQL
    select
    Order_Priority,Order_Quantity,sales,Discount,Ship_Mode,Profit,
    Unit_Price, Shipping_Cost
    from[dbo].[KMS Sql Case Study]
    answer:From the analysis, it’s clear the company is not spending wisely on shipping. High expenses on low-priority orders and low costs on urgent ones show that the shipping strategy is poorly aligned with order importance. Additionally, the negative profits on some orders indicate the need for a thorough review of cost-effectiveness and pricing decisions.
    ```

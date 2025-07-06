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

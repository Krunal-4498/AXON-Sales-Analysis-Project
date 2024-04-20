# Axon Retail Sales Analysis Project

## Overview

This project aims to address the sales data management and analysis issues faced by Axon, a retailer specializing in classic cars. Currently, the company lacks a centralized system to manage and analyze sales data, resulting in challenges for the sales team in making informed decisions and hindering management's ability to access accurate and up-to-date sales reports.

To overcome these challenges, the company has decided to implement a Business Intelligence (BI) tool. After evaluating various options, Microsoft PowerBI and SQL have been shortlisted as potential BI tools for this project.

### Executive Dashboard
![Capstone Project_page-0001](https://github.com/Krunal-4498/AXON_A_Classic_Car_Retailer_Sales_Dashboard/assets/134350505/0d934d96-a6f4-4f74-91b9-f0cae34f41d7)
### Orders Analysis
![Capstone Project_page-0002](https://github.com/Krunal-4498/AXON_A_Classic_Car_Retailer_Sales_Dashboard/assets/134350505/7fa56c1c-57c1-4a86-a162-f395eec482e8)
### Geographical Analysis
![Capture](https://github.com/Krunal-4498/AXON_A_Classic_Car_Retailer_Sales_Dashboard/assets/134350505/dfd3b315-0022-479a-b4e4-4dc05e304fcf)



## Objectives

- 📊 Implement a centralized system for managing and analyzing sales data.
- 🚀 Provide the sales team with the tools necessary to make informed decisions.
- 📈 Enable management to access accurate and up-to-date sales reports.
- 💡 Improve the decision-making process within the company.

## Data Source 
Sales Data : The primary dataset used for analysis is "AXON_sales.sql" containing the details about each sales made by the company.

## Tools
1. MySQL- Data Cleaning and Updating, Exploratory Data Analysis (EDA).
2. Power BI- Creating Reports and Dashboards.

## Data Cleaning/Preparation
1. Checking Dulicate records.
2. Changing Column Datatypes.
3. Giving appropriate Column Names.
4. Removing leading and trailing spaces from column values.

## Exploratory Data Analysis.
1. What is the Total Revenue (In Millions)?
2. How many orders we recived in total?
3. What is the revenue trend?
4. To how many total customer we served?
5. Top revenue generating customer, product, country?

## Data Analysis

1. Count of Orders by Lead Time
```sql
with orders_lead_time as (
    select orderNumber, abs(datediff(orderDate, shippedDate)) as Lead_time_Days
    from Orders
)
select Lead_time_Days, count(*) as Orders_count
from orders_lead_time
group by Lead_time_Days;
```

2. Revenue Year-to-Date (YTD)
```sql 
select sum(quantityOrdered * priceEach)
from orderdetails od
join orders o on od.orderNumber = o.orderNumber
where o.status = 'Shipped'
and date_format(o.orderDate, '%Y') = (
    select date_format(max(orderDate), '%Y')
    from orders
    where status = 'Shipped'
);
```

3. Revenue Month-to-Date (MTD)
```sql
select sum(quantityOrdered * priceEach)
from orderdetails od
join orders o on od.orderNumber = o.orderNumber
where o.status = 'Shipped'
and date_format(o.orderDate, '%Y-%m') = (
    select date_format(max(orderDate), '%Y-%m')
    from orders
    where status = 'Shipped'
);
```




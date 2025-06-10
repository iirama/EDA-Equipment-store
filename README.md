# Equipment Store - Exploratory Data Analysis (EDA)

![EDA Banner](https://via.placeholder.com/800x200?text=Equipment+Store+Data+Analysis) <!-- Consider adding a relevant banner image -->

## 📌 Project Overview
This repository contains a comprehensive Exploratory Data Analysis (EDA) of an equipment store's database. The analysis focuses on uncovering insights from customer data, product information, and sales transactions to drive data-informed business decisions.

## 🗃️ Database Schema
my analysis is based on a SQL database with the following key tables:

### Primary Tables
| Table Name | Description | Key Columns |
|------------|-------------|-------------|
| `gold.dim_customers` | Customer demographic data | `customer_key`, `customer_id`, `first_name`, `last_name`, `country` , `marital_status` , `gender`, `birthdate`, `create_date`|
| `gold.dim_products` | Product inventory information |`product_key`, `product_id`, `product_number`, `product_name`, `category_id` , `category` , `subcategory`, `maintenance`, `cost`  , `product_line` , `start_date` |
| `gold.fact_sales` | Sales transaction records | `order_number`, `product_key`, `customer_key`, `order_date`, `shipping_date` , `due_date` , `sales_amount`, `quantity`, `price` |

## 🎯 Analysis Objectives
1. **Customer Analysis**:
   - Geographic distribution
   - Demographic patterns
   - Purchase behavior

2. **Product Analysis**:
   - Category performance
   - Inventory trends
   - Pricing strategies

3. **Sales Analysis**:
   - Revenue trends
   - Seasonal patterns
   - Customer lifetime value

## 🔍 EDA Process
Our exploratory process includes:

```sql
--1-- Database Exploration
-- 1. explore all object in database 
SELECT * FROM INFORMATION_SCHEMA.TABLES;

-- 2. Explore culomns in database
Select * from NFORMATION_SCHEMA.COLUMNS;
Select * from NFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'dim_customers';
Select * from NFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'dim_products';
Select * from NFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = 'fact_sales';

--2--Dimensions Explooration
-- 1. Explore all countries our customre come from
select DISTINCT country from [gold.dim_customers]

-- 2. explore all categories 'the major Divisions'
select DISTINCT category   from [gold.dim_products]
select DISTINCT category   , subcategory  from [gold.dim_products]
select DISTINCT category   , subcategory , product_name from [gold.dim_products];

--3--Date Exploration
--1. The date of the first and last order and month , years of sales are available
select min(order_date) as first_order_date , max(order_date)as last_order_date  ,
DATEDIFF(year , min(order_date) , max(order_date)) as order_range_years,
DATEDIFF(month , min(order_date) , max(order_date)) as order_range_month
from [gold.fact_sales]
--2. youngest and oldest customres
select min(birthdate) as oldest_birthdate,
datediff(year , min(birthdate) , getdate()) as oldest_age, 
max(birthdate) as youngest_birthdate,
datediff(year , max(birthdate) , getdate()) as youngest_age
from [gold.dim_customers]

--4--Measures Exploration
--1. total sales
select sum(sales_amount) as total_sales from [gold.fact_sales]
--2. items are sold
select sum(quantity) as total_quantity from [gold.fact_sales] 
--3. average selling price
select avg(price) as average_price from [gold.fact_sales] 
--4. total number of order
select count(DISTINCT order_number) as total_number from [gold.fact_sales] 
--5. total number of product
select count (product_key)as total_product from [gold.dim_products]
--6. total number of customer
select count(customer_key)as total_customer from [gold.dim_customers]
--7. total number of customer that has place an order
select count(DISTINCT customer_key)as total_customer from [gold.fact_sales]

--8 Generate report show all key mertics of business

select 'Total Sales' as measure_name , sum(sales_amount) as measure_value from [gold.fact_sales]
union all 
select'Total Quantity' as measure_name, sum(quantity) as measure_value from [gold.fact_sales] 
union all 
select 'Average Price'  as measure_name , avg(price) as measure_value from [gold.fact_sales] 
union all 
select'Total Nr. orders', count(DISTINCT order_number) as measure_value from [gold.fact_sales] 
union all 
select 'Total Nr. Product ' ,count (product_key)as measure_value from [gold.dim_products]
union all
select 'Total Nr. Customers' , count(DISTINCT customer_key)as measure_value from [gold.fact_sales]


--5-- Magnitude Analysis
--1. total customer by countries
select country, count(customer_key) as total_customer from [gold.dim_customers]
group by country
order by total_customer DESC
--2. total customer by gender
select gender, count(customer_key) as total_customer from [gold.dim_customers]
group by gender
order by total_customer DESC
--3. total product by category
select category  , count(product_key) as total_product 
from [gold.dim_products]
group by category
order by total_product DESC
--4. average costs in each category
select category  ,avg(cost) as avg_cost 
from [gold.dim_products]
group by category
order by avg_cost DESC
--5. total revenue generated for eacg category 
select  p.category  , sum(f.sales_amount ) as total_revenue
from [gold.fact_sales] f 
left join [gold.dim_products] p
on p.product_key = f.product_key
group by p.category
order by total_revenue DESC
--6. total revneu is generated by each customer
select c.customer_key , c.first_name , c.last_name , sum (f.sales_amount) as total_revenue
from [gold.fact_sales] f
left join [gold.dim_customers] c
on f.customer_key = c.customer_key
group by c.customer_key , c.first_name , c.last_name
order by total_revenue DESC
--7. distribution of sold item across countries
select c.country , sum (f.quantity) as total_sold_item
from [gold.fact_sales] f
left join [gold.dim_customers] c
on f.customer_key = c.customer_key
group by c.country
order by total_sold_item DESC


--6-- Ranking analysis
--1. 5 product generate the highest revenue
select top 5 p.product_name , sum(f.sales_amount)total_revenue
from [gold.fact_sales] f 
left join [gold.dim_products] p
on p.product_key = f.product_key
group by p.product_name
order by total_revenue DESC

--2. 5 product generate the highest revenue subcategory 
select top 5 p.subcategory , sum(f.sales_amount)total_revenue
from [gold.fact_sales] f 
left join [gold.dim_products] p
on p.product_key = f.product_key
group by p.subcategory
order by total_revenue DESC
--3. the 5 worst-perforaming product on terms of sales
select top 5 p.product_name , sum(f.sales_amount)total_revenue
from [gold.fact_sales] f 
left join [gold.dim_products] p
on p.product_key = f.product_key
group by p.product_name
order by total_revenue 
--4. the 5 worst-perforaming product on terms of sales subcategory
select top 5 p.subcategory , sum(f.sales_amount)total_revenue
from [gold.fact_sales] f 
left join [gold.dim_products] p
on p.product_key = f.product_key
group by p.subcategory
order by total_revenue 

--5 . top 10 customer who have generated the highest revune
select TOP 10 c.customer_key , c.first_name , c.last_name , sum (f.sales_amount) as total_revenue
from [gold.fact_sales] f
left join [gold.dim_customers]c
on f.customer_key = c.customer_key
group by  c.customer_key , c.first_name , c.last_name
order by total_revenue DESC

--6 the 3 customers with the fewest orders placed
select TOP 3 c.customer_key , c.first_name , c.last_name , count(DISTINCT order_number) as total_order
from [gold.fact_sales] f
left join [gold.dim_customers]c
on f.customer_key = c.customer_key
group by  c.customer_key , c.first_name , c.last_name
order by total_order 


# 🏗️ Equipment Store - SQL EDA Project

![SQL](https://img.shields.io/badge/SQL-Exploratory%20Data%20Analysis-blue)
![Database](https://img.shields.io/badge/Database-SQL%20Server-red)
![License](https://img.shields.io/badge/License-MIT-green)

## 📌 Project Overview
This repository documents a complete SQL-based exploratory analysis of an equipment store's database, covering customer demographics, product catalog, and sales transactions from 2010-2014.

## 🔍 EDA Approach
1. **Database Exploration**
2. **Dimension Exploration**
3. **Date Exploration**
4. **Measure Exploration**
5. **Magnitude Exploration**
6. **Ranking Exploration**

## 🗃️ Database Structure
### Core Tables
| Table Name | Description | Key Columns |
|------------|-------------|-------------|
| `gold.dim_customers` | Customer demographic data | `customer_key`, `customer_id`, , `customer number`, `first_name`, `last_name`, `country` , `marital_status` , `gender`, `birthdate`, `create_date`|
| `gold.dim_products` | Product inventory information |`product_key`, `product_id`, `product_number`, `product_name`, `category_id` , `category` , `subcategory`, `maintenance`, `cost`  , `product_line` , `start_date` |
| `gold.fact_sales` | Sales transaction records | `order_number`, `product_key`, `customer_key`, `order_date`, `shipping_date` , `due_date` , `sales_amount`, `quantity`, `price` 

## 📊 Key Findings

### 1. Business Metrics
|Metric|	Value	Business |Interpretation|
|------|----------------|--------------|
|Total Sales	|$29,356,250	|Gross revenue over analysis period|
|Total Quantity	|60,423 units	|Total products sold|
|Average Price|	$486	||Mean transaction value|
|Total Orders|	27,659	|Unique transactions processed|
|Total Products|	295	|SKUs in inventory|
|Active Customers|	18,484|	Unique purchasing customers|

### 2. Customer Insights
#### Geographic Distribution:
|Country | Customers|
|--------|----------|
|United States |	7482|
|Australia|3591|
|United Kingdom|	1913|
|France  |1810 |
|Germany |1780 |
|Canada  |1571 |
|n/a	   |337  |

#### Age Distribution:
|oldest birthdate|oldest age|youngest birthdate|youngest age|
|----------------|----------|------------------|------------|
|1916-02-10 |	109	| 1986-06-25 |	39|

### 3. Product Analysis
#### Category Performance:

|Category|Revenue|
|--------|-------|
|Bikes	|$28,316,272|
|Accessories|	$700,262|
|Clothing	|$339,716|

## Top Performers
###  🏆 Top 5 Products
   1- Mountain-200 Silver - $1,393,994

   2- Mountain-200 Black - $1,373,454

   3- Road-350-W Yellow - $1,361,128

### 🏅 Top 3 Customers
   1- Kaitlyn Henderson - $13,294

   2- Nichole Nara - $13,294

   3- Margaret He - $13,268

## ⚠️ Data Quality Issues
   1- NULL Values: 7 products missing category data

   2- Incomplete Records: 337 customers with 'n/a' country

   3- Age Outliers: Customers >100 years old

 ## 📝 Summary of Insight
   1-  Bikes drive 96.5% of revenue, with consistent 15% YoY growth

   2- Q2 is peak sales season (ideal for promotions)

   3- Top 10 customers generate 12% of total revenue

## **Conclusion**  
- 🚴 **Opportunity**: Bike sales yield 96.5% revenue; optimize inventory.  
- 🎯 **Priority**: Target US males aged 40–60 (highest spenders).  
- 🧹 **Critical**: Clean 337 incomplete customer records. 

## 🔗 LINKES 
### [Full EDA PDF Report](https://github.com/iirama/EDA-Equipment-store/blob/main/Equipment%20Store%20-%20SQL%20EDA%20Report.pdf)
### Advanced Anlysis
   


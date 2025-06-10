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




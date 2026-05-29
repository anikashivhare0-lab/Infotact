# Infotact
-- SELECT * FROM infotact_solutions.data_cleaning;

#use database 
use infotact_solutions;
#table create
CREATE DATABASE sales_project;
USE sales_project;
CREATE TABLE sales_data (
    order_id VARCHAR(50),
    order_date DATETIME,
    year INT,
    quarter VARCHAR(10),
    month INT,
    month_name VARCHAR(20),
    region VARCHAR(50),
    country VARCHAR(50),
    city VARCHAR(50),
    sales_person VARCHAR(100),
    customer_type VARCHAR(50),
    sales_channel VARCHAR(50),
    promotion_type VARCHAR(50),
    product_category VARCHAR(100),
    brand VARCHAR(100),
    product_name VARCHAR(100),
    sku VARCHAR(50),
    units_sold INT,
    unit_price_usd DECIMAL(10,2),
    discount_pct DECIMAL(5,2),
    gross_sales_usd DECIMAL(10,2),
    marketing_spend_usd DECIMAL(10,2),
    cogs_usd DECIMAL(10,2),
    logistics_cost_usd DECIMAL(10,2),
    net_revenue_usd DECIMAL(10,2),
    profit_usd DECIMAL(10,2),
    profit_margin_pct DECIMAL(5,2)
);
#show table 
SELECT * FROM infotact_solutions.data_cleaning;

#Business Question 1
#What is the total revenue
SELECT 
    SUM(net_revenue_usd) AS total_revenue
FROM infotact_solutions.data_cleaning;

#Business Question 2 
#Monthly Sales Trend
SELECT 
    month_name,
    SUM(net_revenue_usd) AS revenue
FROM infotact_solutions.data_cleaning
GROUP BY month_name
ORDER BY MIN(month);

#Business Question 3
#Product Revenue Contribution

SELECT 
    product_category,
    SUM(net_revenue_usd) AS revenue
FROM infotact_solutions.data_cleaning
GROUP BY product_category
ORDER BY revenue DESC;


#Business Question 4
# Order Volume Per City
SELECT 
    city,
    COUNT(order_id) AS total_orders
FROM infotact_solutions.data_cleaning
GROUP BY city
ORDER BY total_orders DESC;

#Peak Operational Hours
#Business Question 5
#What are the peak order hours?
SELECT 
    HOUR(order_date) AS peak_hour,
    COUNT(order_id) AS total_orders
FROM infotact_solutions.data_cleaning
GROUP BY peak_hour
ORDER BY total_orders DESC;

#Quarterly Revenue Analysis
SELECT 
    quarter,
    SUM(net_revenue_usd) AS revenue
FROM  infotact_solutions.data_cleaning
GROUP BY quarter
ORDER BY quarter;

#Top 5 Cities by Revenue
SELECT 
    city,
    SUM(net_revenue_usd) AS revenue
FROM infotact_solutions.data_cleaning
GROUP BY city
ORDER BY revenue DESC
LIMIT 5;

#Best Selling Products
SELECT 
    product_name,
    SUM(units_sold) AS total_units
FROM  infotact_solutions.data_cleaning
GROUP BY product_name
ORDER BY total_units DESC;

#Save All Queries


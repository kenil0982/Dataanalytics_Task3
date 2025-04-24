# Dataanalytics_Task3
Sales and Products Analytics
This project provides an SQL-based analysis of sales data, including product details, sales trends, revenue calculations, and product category performance. The database consists of two key tables: sales and products. This project uses SQL queries for data analysis and insights.

📊 Project Overview
This repository contains SQL scripts that demonstrate various analytics operations such as:

Querying product sales summary

Aggregating revenue and quantities sold

Creating views for easy access to analytics

Optimizing queries with indexes for better performance

🛠 Database Structure
Tables
products
Contains details about products including the name, category, and price.


Column Name	Data Type	Description
product_name	VARCHAR(255)	Name of the product
product_category	VARCHAR(100)	Category of the product
price	DECIMAL(10, 2)	Price of the product
sales
Contains records of each sale, including product name, quantity sold, and sale date.


Column Name	Data Type	Description
sale_id	INT	Unique identifier for each sale
product_name	VARCHAR(255)	Name of the product sold
quantity	INT	Number of items sold
price	DECIMAL(10, 2)	Sale price per item
sale_date	DATE	Date of the sale
🔍 Key Queries and Views
Product Sales Summary View
This view aggregates the total quantity sold and total revenue per product.

sql
Copy
Edit
CREATE VIEW product_sales_summary AS
SELECT 
    p.product_name,
    p.product_category,
    COUNT(s.sale_id) AS total_sales,
    SUM(s.quantity) AS total_quantity_sold,
    SUM(s.quantity * s.price) AS total_revenue
FROM products p
LEFT JOIN sales s ON p.product_name = s.product_name
GROUP BY p.product_name, p.product_category;
Total Revenue by Product Category
Summarizes the revenue by each product category.

sql
Copy
Edit
SELECT 
    p.product_category,
    SUM(s.quantity * s.price) AS category_revenue
FROM sales s
LEFT JOIN products p ON s.product_name = p.product_name
GROUP BY p.product_category
ORDER BY category_revenue DESC;
Top-Selling Products by Quantity
Displays the top-selling products based on the quantity sold.

sql
Copy
Edit
SELECT 
    p.product_name,
    SUM(s.quantity) AS total_quantity_sold
FROM sales s
LEFT JOIN products p ON s.product_name = p.product_name
GROUP BY p.product_name
ORDER BY total_quantity_sold DESC
LIMIT 10;
Sales Trend Over Time (By Date)
Tracks sales performance by date.

sql
Copy
Edit
SELECT 
    DATE(s.sale_date) AS sale_date,
    SUM(s.quantity * s.price) AS total_revenue
FROM sales s
GROUP BY sale_date
ORDER BY sale_date;
Products with No Sales
Identifies products that have not been sold.

sql
Copy
Edit
SELECT 
    p.product_name
FROM products p
LEFT JOIN sales s ON p.product_name = s.product_name
WHERE s.sale_id IS NULL;
⚡ Optimization
Indexes
To improve the performance of queries, especially those with joins, the following indexes can be created:

sql
Copy
Edit
CREATE INDEX idx_product_name ON sales (product_name);
CREATE INDEX idx_sale_date ON sales (sale_date);
📝 Setup Instructions
1. Clone the Repository
bash
Copy
Edit
git clone https://github.com/yourusername/sales-product-analytics.git
2. Set Up the Database
Install MySQL (or your preferred SQL database).

Create a new database and execute the schema creation scripts provided in the schema.sql file.

3. Load Data
Insert sample data into the sales and products tables using the provided data_insert.sql script.

4. Run Queries
You can execute the queries provided in the queries.sql file to generate reports, analyze data, and optimize performance.

🔧 Technologies Used
MySQL: For data storage and querying.

SQL: For writing queries and creating views.

GitHub: For version control and collaboration.


# Commerce-Intelligence-with-SQL-Northwind-Dataset
# 📊 Commerce Intelligence with SQL – Northwind Dataset

## Overview

This project demonstrates how SQL can be used to uncover valuable business insights from the classic **Northwind** database, which simulates a trading company managing customers, products, suppliers, orders, employees, and shipping logistics.

Using well-structured queries and reporting techniques, this project showcases real-world **commerce intelligence** use cases  from tracking sales performance and customer behavior to analyzing employee efficiency and inventory status.





## 🔍 Features

 📈 **Customer & Sales Analysis**: Identify top-performing clients, customer segments, and order value.
 
 🏪 **Inventory & Supply Chain Monitoring**: Spot stock shortages, discontinued items, and reorder trends.
 
 👨‍💼 **Employee Performance & Hierarchy**: Track employee sales activity and map management structure.
 
 🚚 **Shipping & Order Fulfillment Reports**: Analyze delivery channels, order frequency, and lead times.
 
 🧠 **Advanced SQL Use Cases**: Includes joins, subqueries, aggregations, CASE logic, date functions, and more.

 



## 🧱 Database Schema

### Key Tables:

| Table                  | Description |
|------------------------|-------------|
| `customers`            | Information about business clients |
| `orders`               | Order headers linked to customers and employees |
| `order_details`        | Line items (products per order) with pricing and quantity |
| `products`             | Product catalog with category and supplier info |
| `suppliers`            | Vendors supplying the products |
| `categories`           | Product classification |
| `employees`            | Sales staff with a self-referencing hierarchy |
| `shippers`             | Delivery companies used in order fulfillment |
| `territories`, `region`| Sales zones assigned to employees |
| `customer_demographics`| Segmentation data for customers |





## 🔗 Entity Relationship Overview



[customers]──<orders>──<order_details>──┐
│ │ │
│ └──[products]──┬──┘
│ │
└─<customer_customer_demo> │
│ │
[customer_demographics] [suppliers]
[categories]

[orders]──[employees] [shippers]
│ │ (via ShipVia)
└> [employee_territories] ── [territories] ── [region]





## 🧪 Sample SQL Queries


### 🔹 1. Top 5 Customers by Revenue
```sql

SELECT c.CompanyName,
       ROUND(SUM(od.UnitPrice * od.Quantity * (1 - od.Discount)), 2) AS TotalSales
FROM customers c
JOIN orders o ON c.CustomerID = o.CustomerID
JOIN order_details od ON o.OrderID = od.OrderID
GROUP BY c.CompanyName
ORDER BY TotalSales DESC
LIMIT 5;

2. Monthly Sales Trend

SELECT DATE_TRUNC('month', o.OrderDate) AS SalesMonth,
       SUM(od.UnitPrice * od.Quantity * (1 - od.Discount)) AS MonthlySales
FROM orders o
JOIN order_details od ON o.OrderID = od.OrderID
GROUP BY SalesMonth
ORDER BY SalesMonth;


3. Inventory Reorder Alert

SELECT ProductName, UnitsInStock, UnitsOnOrder, ReorderLevel,
       CASE
           WHEN UnitsInStock + UnitsOnOrder <= ReorderLevel THEN 'REORDER NEEDED'
           ELSE 'Stock Sufficient'
       END AS InventoryStatus
FROM products
ORDER BY InventoryStatus DESC;


 4. Employee Supervisor Structure

SELECT e.EmployeeID, e.FirstName || ' ' || e.LastName AS Employee,
       m.FirstName || ' ' || m.LastName AS Manager
FROM employees e
LEFT JOIN employees m ON e.ReportsTo = m.EmployeeID;




🛠️ Tools Used
PostgreSQL / MySQL (Northwind-compatible schema)

SQL (Standard ANSI)

GitHub (for hosting and documentation)




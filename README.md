# 📚 Northwind DB Analysis using MySQL Workbench

This workbook covers fundamental database concepts and practical SQL querying, targeting a Junior Data Analyst role at organizations like **Northwind Traders** and an **international research organization**.

## 3.1. Day 1: Key Database Concepts

### Database Keys and Relationships

| Concept | Explanation | Real-World Example |
| :--- | :--- | :--- |
| **Primary Key** | A field that **uniquely identifies a record** in a table. | A (monogamous) married couple (1:1 relationship example). |
| **Secondary Key** | May not be unique but **helps to retrieve records** from columns and provides additional access. | Recipes and ingredients (M:M relationship example). |
| **Foreign Key** | A **primary key from another table** used to provide a linked relationship between the data. | A doctor and their patient list (1:M relationship example). |

### Relational vs. Non-Relational Databases

| Database Type | Description | Best Fit Data Type & Why |
| :--- | :--- | :--- |
| **Relational** | Consists of **organized data in tables** based on datapoints that relate to each other. | Structured data for efficient management and retrieval. |
| **Non-Relational** | Allows for **diverse unstructured data** to be stored (e.g., key-value, documents, graphs). | **Images and videos** because they are not able to be put in structured format (columns and rows), benefiting from scalability and flexibility. |

## 3.2. Day 2: Basic SQL Queries (Northwind Database)

| Task | Objective | SQL Query |
| :--- | :--- | :--- |
| 1. Full Customer Data | Retrieve all columns from the `Customers` table. | `select * from customers;` |
| 2. Customer Names and Cities | Retrieve only `CustomerName` and `City` from the `Customers` table. | `select CustomerName, City from customers;` |
| 3. Unique Cities | Retrieve distinct city values from the `City` column. | `select distinct City,from customers;` |
| 4. High-Value Products | Retrieve all columns from `Products` where `Price` is greater than 50. | `SELECT * FROM products,WHERE price >50;` |
| 5. International Customers | Retrieve all columns from `Customers` where `Country` is 'USA' or 'UK'. | `Select * From Customers Where country = "usa" or country ="UK";` |
| 6. Recent Orders Report | Retrieve all columns from `Orders`, sorted by `OrderDate` in descending order. | `SELECT * From orders order by OrderDate desc;` |
| 7. Mid-Range Products | Retrieve all columns from `Products` where `Price` is between 20 and 50, ordered by descending `Price`. | `select * from products where price between '20' And '50' order by price Desc;` |
| 8. Local Marketing (USA) | Retrieve all columns from `Customers` where `Country` is 'USA' AND City is 'Portland' OR 'Kirkland'. | `select * from customers where country = "USA" AND city = 'Portland' OR city='Kirkland' order by CustomerName ASC;` |
| 9. UK or London Customers | Retrieve all columns from `Customers` where `Country` is 'UK' OR City is 'London'. | `Select * from customers where country = 'UK' OR city= 'London' order by CustomerName Desc;` |
| 10. Product Inventory | Retrieve all columns from `Products` where `CategoryID` is 1 or 2. | `select * from products where categoryID= '1' OR categoryid= '2' order by ProductName ASC;` |


## 3.3. Day 3: Joins and Multi-Table Queries (Northwind)

### JOIN Type Research

| JOIN Type | Description | Example Use Case |
| :--- | :--- | :--- |
| **Self-join** | A table is **joined to itself**, used for comparisons or hierarchical data. | Retrieve both employees and their managers in one table. |
| **Right join** | Returns **all rows from the right table** and matching rows from the left. | Listing every order made even if they don't have a matching customer. |
| **Full join** | Returns **all rows when there's a match in either table**. | Combining customers and orders even if there's no match in one table. |
| **Inner join** | Combines **matching rows** from two or more tables based on a related column. | Finding customers who have placed orders. |
| **Cross join** | Finds **every possible combination** by pairing every row in the first table with every row in the second. | Finding every possible size, color, and fit combination for every item in a clothing store. |
| **Left join** | Returns **all rows from the left table** and matching rows from the right. | Finding all customers, even if they haven't placed an order. |

### Practical JOIN Queries

| Task | Objective | SQL Query |
| :--- | :--- | :--- |
| 1. Products to Suppliers | Find the supplier name for each product. | `select ProductName, SupplierName From products join suppliers on products.SupplierID = Suppliers.SupplierID;` |
| 2. Classifying Products | Find the category name for each product. | `Select ProductName, CategoryName From Products Join Categories on products.CategoryID = Categories.CategoryID;` |
| 3. Meat/Poultry Report | Retrieve all products belonging to the 'Meat/Poultry' category. | `Select ProductName, CategoryName From Products Join Categories on products.CategoryID = Categories.CategoryID where CategoryName = "Meat/Poultry";` |
| 4. Complete Order Overview | Retrieve `OrderID`, `OrderDate`, `CustomerName`, and `EmployeeName` for all orders. | `select OrderID, OrderDate, CustomerName, concat_ws(" ",FirstName, LastName) as EmployeeName from orders join Customers on orders.CustomerID = customers.CustomerID join employees on orders.EmployeeID = Employees.EmployeeID;` |
| 5. Supply Chain Overview | Retrieve `ProductName`, `CategoryName`, and `SupplierName` for all products. | `select ProductName, categories.CategoryName, suppliers.SupplierName from Products join Categories on products.CategoryID = Categories.CategoryID join Suppliers on products.SupplierID = suppliers.SupplierID;` |
| 6. Yearly Order Summary – 1996 | Create a report for all orders of 1996, including customer and product information. | `select CustomerName, orders.CustomerID, OrderDate, ProductName from Orders Join Customers on orders.CustomerID = customers.CustomerID join order_details on orders.OrderID = order_details.OrderID join products on order_details.ProductID = products.ProductID Where OrderDate LIKE "1996%";` |
| 7. Product Count by Category | Retrieve all categories along with the number of products in each category. | `select CategoryName, count(ProductName) as TotalQuantity from products join Categories on categories.CategoryID = products.CategoryID group by CategoryName;` |
| 8. Sales Volume Breakdown | Retrieve product prices, names, and the total quantity ordered for each product. | `select Price, sum(Quantity), ProductName from Products join order_details on products.productid = order_details.productID group by ProductName, Price;` |

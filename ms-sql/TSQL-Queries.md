# MS SQL Server T-SQL Queries

## Connection to MS-SQL Sample Database 

1.  Start `SSMS` from Windows Start Menu

    > SSMS is short name for `SQL Server Management Studio` Which is a Default GUI Client for MS-SQL Server Database.

    ```ini
    SQL-Server-Host=sampledb101.database.windows.net
    Authentication=SQL Server Authentication
    Login=sqladmin
    Password=Password@1234      
    ```


We'll cover various operations such as selecting data, filtering, joining tables, aggregating results, and more. Here are some demo examples:

### 1. **Basic SELECT Queries**
   - **Retrieve all products**
     ```sql
     SELECT ProductID, Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate
     FROM SalesLT.Product;
     ```

   - **Retrieve specific columns from the SalesOrderHeader table**
     ```sql
     SELECT SalesOrderID, OrderDate, DueDate, ShipDate, TotalDue
     FROM SalesLT.SalesOrderHeader;
     ```

### 2. **Filtering Data with WHERE Clause**
   - **Retrieve products with a list price greater than $500**
     ```sql
     SELECT ProductID, Name, ProductNumber, ListPrice
     FROM SalesLT.Product
     WHERE ListPrice > 500;
     ```

   - **Retrieve orders shipped after a specific date**
     ```sql
     SELECT SalesOrderID, OrderDate, ShipDate, TotalDue
     FROM SalesLT.SalesOrderHeader
     WHERE ShipDate > '2023-01-01';
     ```

### 3. **Using JOIN to Combine Data from Multiple Tables**
   - **Retrieve order details with product information**
     ```sql
     SELECT soh.SalesOrderID, soh.OrderDate, sod.ProductID, p.Name AS ProductName, sod.OrderQty, sod.UnitPrice
     FROM SalesLT.SalesOrderHeader soh
     JOIN SalesLT.SalesOrderDetail sod ON soh.SalesOrderID = sod.SalesOrderID
     JOIN SalesLT.Product p ON sod.ProductID = p.ProductID;
     ```

   - **Retrieve customer orders with customer details**
     ```sql
     SELECT c.CustomerID, c.FirstName, c.LastName, soh.SalesOrderID, soh.OrderDate, soh.TotalDue
     FROM SalesLT.Customer c
     JOIN SalesLT.SalesOrderHeader soh ON c.CustomerID = soh.CustomerID;
     ```

### 4. **Aggregating Data with GROUP BY and Aggregation Functions**
   - **Total sales amount per customer**
     ```sql
     SELECT c.CustomerID, c.FirstName, c.LastName, SUM(soh.TotalDue) AS TotalSales
     FROM SalesLT.Customer c
     JOIN SalesLT.SalesOrderHeader soh ON c.CustomerID = soh.CustomerID
     GROUP BY c.CustomerID, c.FirstName, c.LastName;
     ```

   - **Count of orders placed per product**
     ```sql
     SELECT p.ProductID, p.Name, COUNT(sod.SalesOrderID) AS OrdersCount
     FROM SalesLT.Product p
     JOIN SalesLT.SalesOrderDetail sod ON p.ProductID = sod.ProductID
     GROUP BY p.ProductID, p.Name;
     ```

### 5. **Using Subqueries**
   - **Retrieve customers who have placed more than 3 orders**
     ```sql
     SELECT c.CustomerID, c.FirstName, c.LastName
     FROM SalesLT.Customer c
     WHERE (SELECT COUNT(soh.SalesOrderID) 
            FROM SalesLT.SalesOrderHeader soh 
            WHERE soh.CustomerID = c.CustomerID) > 3;
     ```

   - **List products that have never been ordered**
     ```sql
     SELECT p.ProductID, p.Name
     FROM SalesLT.Product p
     WHERE NOT EXISTS (
         SELECT 1 
         FROM SalesLT.SalesOrderDetail sod 
         WHERE sod.ProductID = p.ProductID);
     ```

### 6. **Updating Data**
   - **Increase the list price of all red products by 10%**
     ```sql
     UPDATE SalesLT.Product
     SET ListPrice = ListPrice * 1.1
     WHERE Color = 'Red';
     ```

   - **Mark orders as shipped if the ship date is in the past and the status is still pending**
     ```sql
     UPDATE SalesLT.SalesOrderHeader
     SET Status = 5  -- 5 might represent 'Shipped' in this context
     WHERE ShipDate <= GETDATE() AND Status = 1;  -- 1 might represent 'Pending'
     ```

### 7. **Deleting Data**
   - **Remove orders from customers who are no longer active**
     ```sql
     DELETE FROM SalesLT.SalesOrderHeader
     WHERE CustomerID IN (
         SELECT CustomerID 
         FROM SalesLT.Customer 
         WHERE Status = 'Inactive');
     ```

   - **Delete products with no orders**
     ```sql
     DELETE FROM SalesLT.Product
     WHERE ProductID NOT IN (
         SELECT DISTINCT ProductID 
         FROM SalesLT.SalesOrderDetail);
     ```

These examples provide a well-rounded set of demos that showcase different SQL functionalities using the AdventureWorks SalesLT schema. Each example is designed to help learners understand key SQL concepts and how they are applied in real-world scenarios.
### **Answers:**

1. **Retrieve Customer Information**
   ```sql
   SELECT CustomerID, FirstName, LastName, EmailAddress
   FROM SalesLT.Customer
   WHERE LastName LIKE 'S%';
   ```

2. **Product Search by Price**
   ```sql
   SELECT ProductID, Name, ListPrice
   FROM SalesLT.Product
   WHERE ListPrice BETWEEN 100 AND 500
   ORDER BY ListPrice DESC;
   ```

3. **Orders from a Specific Date**
   ```sql
   SELECT SalesOrderID, OrderDate, TotalDue
   FROM SalesLT.SalesOrderHeader
   WHERE OrderDate = '2023-01-01';
   ```

4. **Join Customers with Orders**
   ```sql
   SELECT c.CustomerID, c.FirstName, c.LastName, soh.SalesOrderID, soh.OrderDate
   FROM SalesLT.Customer c
   JOIN SalesLT.SalesOrderHeader soh ON c.CustomerID = soh.CustomerID
   ORDER BY soh.OrderDate;
   ```

5. **Count of Orders per Customer**
   ```sql
   SELECT c.CustomerID, c.FirstName, c.LastName, COUNT(soh.SalesOrderID) AS OrderCount
   FROM SalesLT.Customer c
   JOIN SalesLT.SalesOrderHeader soh ON c.CustomerID = soh.CustomerID
   GROUP BY c.CustomerID, c.FirstName, c.LastName
   ORDER BY OrderCount DESC;
   ```

6. **Total Sales per Product**
   ```sql
   SELECT p.ProductID, p.Name, SUM(sod.OrderQty * sod.UnitPrice) AS TotalSales
   FROM SalesLT.Product p
   JOIN SalesLT.SalesOrderDetail sod ON p.ProductID = sod.ProductID
   GROUP BY p.ProductID, p.Name
   HAVING SUM(sod.OrderQty * sod.UnitPrice) > 0
   ORDER BY TotalSales DESC;
   ```

7. **Subquery: Customers with Large Orders**
   ```sql
   SELECT CustomerID, FirstName, LastName
   FROM SalesLT.Customer
   WHERE CustomerID IN (
       SELECT CustomerID
       FROM SalesLT.SalesOrderHeader
       WHERE TotalDue > 1000
   );
   ```

8. **Products Never Ordered**
   ```sql
   SELECT ProductID, Name
   FROM SalesLT.Product
   WHERE ProductID NOT IN (
       SELECT DISTINCT ProductID
       FROM SalesLT.SalesOrderDetail
   );
   ```

9. **Updating Product Prices**
   ```sql
   UPDATE SalesLT.Product
   SET ListPrice = ListPrice * 1.15
   WHERE ProductCategoryID = (
       SELECT ProductCategoryID
       FROM SalesLT.ProductCategory
       WHERE Name = 'Components'
   );
   ```

10. **Delete Old Orders**
    ```sql
    DELETE FROM SalesLT.SalesOrderHeader
    WHERE OrderDate < '2022-01-01';
    ```

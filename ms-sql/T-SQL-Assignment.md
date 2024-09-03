### **Assignment: SQL Queries with AdventureWorks SalesLT Schema**

#### **Instructions:**
For each of the following tasks, write a SQL query to achieve the desired result. Test your queries against the AdventureWorks SalesLT schema to ensure they return the correct data.

---

### **Tasks:**

1. **Retrieve Customer Information**
   - Write a query to retrieve the `CustomerID`, `FirstName`, `LastName`, and `EmailAddress` of all customers whose last name starts with the letter 'S'.

2. **Product Search by Price**
   - Retrieve the `ProductID`, `Name`, and `ListPrice` of all products that have a list price between $100 and $500. Sort the results by `ListPrice` in descending order.

3. **Orders from a Specific Date**
   - Write a query to retrieve the `SalesOrderID`, `OrderDate`, and `TotalDue` for all orders placed on January 1, 2023.

4. **Join Customers with Orders**
   - Create a query to list `CustomerID`, `FirstName`, `LastName`, `SalesOrderID`, and `OrderDate` for all customers who have placed an order. Sort the results by `OrderDate`.

5. **Count of Orders per Customer**
   - Write a query to count the number of orders (`SalesOrderID`) placed by each customer. Return the `CustomerID`, `FirstName`, `LastName`, and `OrderCount`. Sort the results by `OrderCount` in descending order.

6. **Total Sales per Product**
   - Write a query to calculate the total sales (`TotalSales`) for each product. Return the `ProductID`, `Name`, and `TotalSales` (sum of `OrderQty` multiplied by `UnitPrice`). Only include products that have been ordered. Sort by `TotalSales` in descending order.

7. **Subquery: Customers with Large Orders**
   - Write a query to list the `CustomerID`, `FirstName`, and `LastName` of customers who have placed at least one order with a `TotalDue` greater than $1000.

8. **Products Never Ordered**
   - Create a query to list all products that have never been ordered. Return the `ProductID` and `Name`.

9. **Updating Product Prices**
   - Write a query to increase the `ListPrice` of all products in the 'Components' category by 15%.

10. **Delete Old Orders**
    - Write a query to delete all orders that were placed before January 1, 2022.



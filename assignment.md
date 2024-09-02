### Practical Assignment: PostgreSQL Database

**Objective:**  
To gain hands-on experience in working with PostgreSQL, including creating databases, tables, and performing CRUD (Create, Read, Update, Delete) operations.

---

#### **Assignment Overview:**
You are tasked with creating and managing a PostgreSQL database for a fictional online bookstore. The bookstore needs to store information about its books, customers, and orders. You'll be required to create tables for each of these entities and perform various operations to simulate real-world use cases.

---

### **Part 1: Setting Up PostgreSQL**

1. **Create a Database:**
   
   - Create a database named `BookstoreDB`.

---

### **Part 2: Create Tables and Insert Data**

1. **Create Tables:**
   - Create the following tables:

   **Books Table:**
   ```sql
   CREATE TABLE Books (
       ISBN VARCHAR(13) PRIMARY KEY,
       title VARCHAR(255) NOT NULL,
       author VARCHAR(255),
       publisher VARCHAR(255),
       price NUMERIC(10, 2),
       stock INT
   );
   ```

   **Customers Table:**
   ```sql
   CREATE TABLE Customers (
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       email VARCHAR(255) UNIQUE NOT NULL,
       phone VARCHAR(15),
       address TEXT
   );
   ```

   **Orders Table:**
   ```sql
   CREATE TABLE Orders (
       order_id SERIAL PRIMARY KEY,
       customer_id INT REFERENCES Customers(customer_id),
       order_date DATE,
       total_amount NUMERIC(10, 2)
   );
   ```

   **OrderItems Table:**
   ```sql
   CREATE TABLE OrderItems (
       order_id INT REFERENCES Orders(order_id),
       ISBN VARCHAR(13) REFERENCES Books(ISBN),
       quantity INT,
       PRIMARY KEY (order_id, ISBN)
   );
   ```

2. **Insert Data:**
   - Insert at least 5 records into each table with the following sample structure:

   **Books Table:**
   ```sql
   INSERT INTO Books (ISBN, title, author, publisher, price, stock)
   VALUES ('978-3-16-148410-0', 'Sample Book Title', 'Author Name', 'Publisher Name', 25.99, 100);
   ```

   **Customers Table:**
   ```sql
   INSERT INTO Customers (name, email, phone, address)
   VALUES ('John Doe', 'john.doe@example.com', '123-456-7890', '123 Main St, City, Country');
   ```

   **Orders Table:**
   ```sql
   INSERT INTO Orders (customer_id, order_date, total_amount)
   VALUES (1, '2024-09-01', 51.98);
   ```

   **OrderItems Table:**
   ```sql
   INSERT INTO OrderItems (order_id, ISBN, quantity)
   VALUES (1, '978-3-16-148410-0', 2);
   ```

---

### **Part 3: Perform CRUD Operations**

1. **Create:**
   - Add a new book to the `Books` table.
   - Add a new customer to the `Customers` table.
   - Add a new order to the `Orders` table along with its items in the `OrderItems` table.

2. **Read:**
   - Query the `Books` table to find a book by its `ISBN`.
   - Retrieve all orders placed by a specific customer using their `customer_id`.
   - List all books that are out of stock (i.e., `stock` is 0).

3. **Update:**
   - Update the price of a specific book by `ISBN`.
   - Change the email address of a customer by `customer_id`.
   - Update an order to include an additional book by modifying the `OrderItems` table.

4. **Delete:**
   - Delete a book from the `Books` table using its `ISBN`.
   - Remove a customer from the `Customers` table by `customer_id`.
   - Delete an order from the `Orders` table by `order_id`, ensuring the corresponding entries in `OrderItems` are also removed.

---

### **Part 4: Advanced Queries**

1. **Joins:**
   - Write a query to list all orders along with the customer name and total amount. Use an INNER JOIN between `Orders` and `Customers`.

2. **Aggregation Functions:**
   - Use the `SUM()` function to calculate the total sales amount for each customer.
   - Use the `COUNT()` function to find out how many times each book has been ordered.

3. **Indexing:**
   - Create an index on the `title` field in the `Books` table to optimize search performance.

4. **Views:**
   - Create a view that shows the details of all orders, including customer name, order date, and total amount.

---

### **Part 5: Backup and Restore**

1. **Backup Data:**
   - Use the `pg_dump` command to create a backup of the `BookstoreDB` database.

2. **Restore Data:**
   - Delete existing tables from database `bookstoredb`
   - Use the `psql` command to restore the database from the backup file.

---

### **Submission Guidelines:**

- Submit your SQL scripts used for each part.
- Include screenshots or logs of the operations performed.
- Provide the backup file of the `BookstoreDB` database.



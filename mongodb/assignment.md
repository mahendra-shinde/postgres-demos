### Practical Assignment: MongoDB Database

**Objective:**  
To gain hands-on experience in working with MongoDB, including creating databases, collections, and performing CRUD (Create, Read, Update, Delete) operations.

---

#### **Assignment Overview:**
You are tasked with creating and managing a MongoDB database for a fictional online bookstore. The bookstore needs to store information about its books, customers, and orders. You'll be required to create collections for each of these entities and perform various operations to simulate real-world use cases.

---

### **Part 1: Setting Up MongoDB**

1. **Install MongoDB:**
   - Install MongoDB on your local machine or use a cloud-based service like MongoDB Atlas.

2. **Create a Database:**
   - Create a database named `BookstoreDB`.

---

### **Part 2: Create Collections and Insert Documents**

1. **Create Collections:**
   - Create the following collections:
     - `Books`
     - `Customers`
     - `Orders`

2. **Insert Documents:**
   - Insert at least 5 documents into each collection with the following structure:

   **Books Collection:**
   ```json
   {
       "ISBN": "978-3-16-148410-0",
       "title": "Sample Book Title",
       "author": "Author Name",
       "publisher": "Publisher Name",
       "price": 25.99,
       "stock": 100
   }
   ```

   **Customers Collection:**
   ```json
   {
       "customer_id": 1001,
       "name": "John Doe",
       "email": "john.doe@example.com",
       "phone": "123-456-7890",
       "address": "123 Main St, City, Country"
   }
   ```

   **Orders Collection:**
   ```json
   {
       "order_id": 5001,
       "customer_id": 1001,
       "order_date": "2024-09-01",
       "items": [
           {
               "ISBN": "978-3-16-148410-0",
               "quantity": 2
           }
       ],
       "total_amount": 51.98
   }
   ```

---

### **Part 3: Perform CRUD Operations**

1. **Create:**
   - Add a new book to the `Books` collection.
   - Add a new customer to the `Customers` collection.
   - Add a new order to the `Orders` collection.

2. **Read:**
   - Query the `Books` collection to find a book by its `ISBN`.
   - Retrieve all orders placed by a specific customer using their `customer_id`.
   - List all books that are out of stock (i.e., `stock` is 0).

3. **Update:**
   - Update the price of a specific book by `ISBN`.
   - Change the email address of a customer by `customer_id`.
   - Update an order to include an additional book.

4. **Delete:**
   - Delete a book from the `Books` collection using its `ISBN`.
   - Remove a customer from the `Customers` collection by `customer_id`.
   - Delete an order from the `Orders` collection by `order_id`.




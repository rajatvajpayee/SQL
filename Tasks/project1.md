# Project - Retail Store Management System

Imagine you are a database administrator for a local retail store. Your job is to design, create, and manage a database that stores information about products, customers, and orders. You will use SQL queries to handle tasks like:
✅ Creating and modifying tables
✅ Adding, updating, and deleting records
✅ Filtering and sorting data for better insights
✅ Using aggregations to analyze store performance
✅ Working with dates to track sales trends

By the end of this project, you will have a fully functional database that mimics a real-world retail system. You'll also strengthen your problem-solving skills by debugging and optimizing queries.


## Working

### Task1 : Design the database schema - Table and Fields
There should be 3 tables in this database.

- Products - Stores information about items sold in the retail store.
- Customers - Stores customer details, ensuring unique emails and phone numbers.
- Orders - Tracks purchases, linking customers to their orders.

CREATE the tables with the following fields and constraints:
##### Products

| **Field**      | **Datatype** | **Constraint**                                                          |
| -------------- | ------------ | ----------------------------------------------------------------------- |
| product_id     | INTEGER      | PRIMARY KEY                                                             |
| name           | TEXT         | NOT NULL                                                                |
| category       | TEXT         | CHECK (category IN ('Electronics', 'Clothing', 'Grocery', 'Furniture')) |
| price          | REAL         | NOT NULL CHECK (price > 0)                                              |
| stock_quantity | INTEGER      | CHECK (stock_quantity >= 0)                                             |

##### Customers

| **Field**   | **Datatype** | **Constraint**         |
| ----------- | ------------ | ---------------------- |
| customer_id | INTEGER      | PRIMARY KEY            |
| name        | TEXT         | NOT NULL               |
| email       | TEXT         | UNIQUE NOT NULL        |
| phone       | TEXT         | UNIQUE NOT NULL        |
| address     | TEXT         | DEFAULT 'Not Provided' |

##### Orders

|**Field**|**Datatype**|**Constraint**|
|---|---|---|
|order_id|INTEGER|PRIMARY KEY|
|customer_id|INTEGER|NOT NULL|
|order_date|DATE|DEFAULT CURRENT_DATE|
|total_amount|REAL|CHECK (total_amount > 0)|
|Remarks_if_any|TEXT|DEFAULT 'No Remarks'|
```
/* Update the '_' in the code below */

CREATE TABLE Products (
    product_id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    category TEXT CHECK  (category IN ('Electronics', 'Clothing', 'Grocery', 'Furniture')),
    price REAL NOT NULL CHECK (price > 0),
    stock_quantity INTEGER CHECK (stock_quantity >= 0)
);

CREATE TABLE Customers (
    customer_id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    phone TEXT UNIQUE NOT NULL,
    address TEXT DEFAULT 'Not Provided'
);

CREATE TABLE Orders (
    order_id INTEGER PRIMARY KEY,
    customer_id INTEGER NOT NULL,
    order_date DATE DEFAULT CURRENT_DATE,
    total_amount REAL CHECK (total_amount > 0),
    Remarks_if_any TEXT DEFAULT 'No Remarks'
);

```

### Task-2 Populate the tables with data
```
INSERT INTO Customers (customer_id, name, email, phone, address) 
VALUES
(1, 'John Doe', 'john.doe@email.com', '9876543210', '123 Main St'),
(2, 'Jane Smith', 'jane.smith@email.com', '9823456789', '45 Elm St'),
(3, 'Alice Brown', 'alice.b@email.com', '9988776655', '78 Pine Ave'),
(4, 'Bob Johnson', 'bob.j@email.com', '9765432109', '90 Oak Lane'),
(5, 'Charlie Lee', 'charlie.l@email.com', '9234567890', 'Not Provided'),
(6, 'David White', 'david.w@email.com', '9678991234', '12 Maple St'),
(7, 'Emily Clark', 'emily.c@email.com', '9345678901', 'Not Provided'),
(8, 'Frank Harris', 'frank.h@email.com', '9763214785', '56 Birch Road'),
(9, 'Amit Shah ', 'some1@email.com', '9999999999', 'Add1'),
(10, 'No One', 'nonoe@email.com', '9999999998', 'Add2');

INSERT INTO Products (product_id, name, category, price, stock_quantity) 
VALUES
(101, 'Apple iPhone 15', 'Electronics', 999.99, 10),
(102, 'Samsung Galaxy S23', 'Electronics', 899.99, 15),
(103, 'Leather Jacket', 'Clothing', 149.99, 25),
(104, 'HP Laptop', 'Electronics', 799.99, 8),
(105, 'Wooden Dining Table', 'Furniture', 499.99, 5),
(106, 'Nike Running Shoes', 'Clothing', 129.99, 20),
(107, 'LED TV 55"', 'Electronics', 699.99, 12),
(108, 'Rice 10kg', 'Grocery', 25.99, 50),
(109, 'Sofa Set (3+1+1)', 'Furniture', 999.99, 4),
(110, 'Organic Honey 500ml', 'Grocery', 15.99, 30);

INSERT INTO Orders (order_id, customer_id, order_date, total_amount, Remarks_if_any) 
VALUES
(1001, 1, '2024-01-15', 999.99, 'No Remarks'),
(1002, 2, '2024-01-16', 299.98, 'Delivered'),
(1003, 3, '2024-01-17', 129.99, 'Payment Pending'),
(1004, 4, '2024-01-18', 899.99, 'No Remarks'),
(1005, 5, '2024-01-19', 799.99, 'Cancelled'),
(1006, 6, '2024-01-20', 499.99, 'Delivered'),
(1007, 7, '2024-01-21', 129.99, 'No Remarks'),
(1008, 8, '2024-01-22', 699.99, 'Refund Issued'),
(1009, 9, '2024-01-23', 25.99, 'No Remarks'),
(1010, 10, '2024-01-24', 15.99, 'Delivered');

--Queries for retrieving the first 3 records from the three tables

SELECT * FROM Customers LIMIT 3;
SELECT * FROM Products LIMIT 3;
SELECT * FROM Orders LIMIT 3;
------------------------------------------------------------------------------------------
┌─────────────┬─────────────┬──────────────────────┬────────────┬─────────────┐
│ customer_id │    name     │        email         │   phone    │   address   │
├─────────────┼─────────────┼──────────────────────┼────────────┼─────────────┤
│ 1           │ John Doe    │ john.doe@email.com   │ 9876543210 │ 123 Main St │
│ 2           │ Jane Smith  │ jane.smith@email.com │ 9823456789 │ 45 Elm St   │
│ 3           │ Alice Brown │ alice.b@email.com    │ 9988776655 │ 78 Pine Ave │
└─────────────┴─────────────┴──────────────────────┴────────────┴─────────────┘
┌────────────┬────────────────────┬─────────────┬────────┬────────────────┐
│ product_id │        name        │  category   │ price  │ stock_quantity │
├────────────┼────────────────────┼─────────────┼────────┼────────────────┤
│ 101        │ Apple iPhone 15    │ Electronics │ 999.99 │ 10             │
│ 102        │ Samsung Galaxy S23 │ Electronics │ 899.99 │ 15             │
│ 103        │ Leather Jacket     │ Clothing    │ 149.99 │ 25             │
└────────────┴────────────────────┴─────────────┴────────┴────────────────┘
┌──────────┬─────────────┬────────────┬──────────────┬─────────────────┐
│ order_id │ customer_id │ order_date │ total_amount │ Remarks_if_any  │
├──────────┼─────────────┼────────────┼──────────────┼─────────────────┤
│ 1001     │ 1           │ 2024-01-15 │ 999.99       │ No Remarks      │
│ 1002     │ 2           │ 2024-01-16 │ 299.98       │ Delivered       │
│ 1003     │ 3           │ 2024-01-17 │ 129.99       │ Payment Pending │
└──────────┴─────────────┴────────────┴─────────-────┴─────────────────┘
```

### Task3 : Queries
```

Select top two expensive items 

select * from products 
order by price DESC
LIMIT 2;

┌────────────┬──────────────────┬─────────────┬────────┬────────────────┐
│ product_id │       name       │  category   │ price  │ stock_quantity │
├────────────┼──────────────────┼─────────────┼────────┼────────────────┤
│ 101        │ Apple iPhone 15  │ Electronics │ 999.99 │ 10             │
│ 109        │ Sofa Set (3+1+1) │ Furniture   │ 999.99 │ 4              │
└────────────┴──────────────────┴─────────────┴────────┴────────────────┘


### Task

Add a new column "discount" to the Orders table.  
Set its default value to 0.  
Then, retrieve the order_id, total_amount and discount of the first order from the Orders table.

ALTER TABLE orders 
ADD column discount float default 0;

Select  order_id, total_amount, discount
from orders 
limit 1;

┌──────────┬──────────────┬──────────┐
│ order_id │ total_amount │ discount │
├──────────┼──────────────┼──────────┤
│ 1001     │ 999.99       │ 0.0      │
└──────────┴──────────────┴──────────┘


######## Task

We have deleted all orders that were placed before 2024-01-20.

You need to do the following

- Delete all Customers from the Customer table who have no records in the Orders table.
- Then, retrieve the customer_id and name of all Customers from the Customers table.
-----------------------------------
BEGIN TRANSACTION;
SAVEPOINT S1;
--Savepoint created incase any changes to the the database beyond this point has to be undone in the future.

DELETE FROM Orders
WHERE order_date < '2024-01-20';

/* Update your query here */
DELETE FROM customers
where customer_id not in (select distinct customer_id from orders);

SELECT customer_id, name 
FROM customers;
---------------------------------

### Task-7B Working with NULL values
Check if the customer with customer_id = 10 and name = 'Henry Adams' has NULL in the new_address column.  
If it is NULL, update it to **"23 Walnut Lane"**.  
Then, retrieve all details about that customer from the Customers table.


```



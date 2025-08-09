##### Table Of Contents

---
# Introduction
Structured Query Language (SQL) is a programming language specifically created to access, organise and manipulate data within relational databases.
In a relational database, information is arranged into one or more tables, each containing columns and rows of interconnected data entries that relate to each other in some way.

```
SELECT * FROM DB; < Select all values from the database
```

## Data Types

- INTEGER, a positive or negative whole number
- TEXT, a text string
- VARCHAR, a variable-length text string
- DATE, the date formatted as YYYY-MM-DD
- REAL, a decimal value

##### Note
```
CREATE TABLE (); --- Here, Create table is the caluse which can be called as the command
```

## ER Diagram
- Blueprint of the database, telling that how different piece of information is connected
- Visual representation 
	- How data is organised
	- Maps out the relationships
- Components of ER Diagram
	- Entities
	- Attributes
	- Relationships
![[Pasted image 20250808020147.png]]

## Entity 
- A "thing" or "object" that the real world has
- Entity set : Collection of similar entities

### Characteristics of an Entity Set:
- Contains entities of the same type
- Shares a common structure (attributes)
- Each entity in the set is unique
- Can participate in relationships with other entity sets
### Types of Entities 
1. Strong Entity : 
	1. An entity that can exist independently of other entities. It has attributes that can uniquely identify it; PRIMARY KEY
	2. Defined by Rectangle in ERD
2. Weak Entity
	1. Can not exist independently and must be associated with another strong entity
	2. Does not have unique identified. Generally, relies on FOREIGN KEY
	3. Shown as rectangle with two boxes

## Attributes
Characterstics of an entity : Simply columns in the table while the entity is the table itself
### Key Attributes
- A unique thing which helps to identify each record distinctly
- Represented by an oval with line in ERD
- Points to Remember
	- Must be unique
	- Cannot be null
	- Should rarely change or never change
	- Often used as references in other tables

### Composite Attributes
- When combine multiple simple attributes to form a one meaningful attribute
- Represented by oval in ERD
- Points to Remember - 
	- Can be broken into small pieces
	- Each part has its own meaning
	- Good for organizing related data
- ![[Pasted image 20250808021353.png]]

## Relationships
A relationship is a connection or association between specific entities. In ERD, represented by diamond

## Primary Key
- Is a column (or set of columns) in a database that uniquely identifies each row
- Uniqueness and non-nullability 
- Each table can have only one primary key.
#### Unique
- Ensures that all values in a column are distinct
- Values can be NULL until explicitly marked
- `title VARCHAR(255) UNIQUE`
#### Not NULL
- Prevent a column from having NULL values 
- `id INT not NULL`
#### Default
- Assigns a default value to a column when no value is provided during INSERT operation
- `age INT DEFAULT 13`
#### Auto Increment 
-  Automatically generates a unique sequential value for a column (usually for primary keys).
- `CREATE TABLE users ( id INT AUTO_INCREMENT PRIMARY KEY, );`


---
# Constraints
- **Constraints** provide details about the usage of a column and are applied after specifying the column's data type.  
- They enable the database to reject any inserted data that violates a particular constraint.  
- The following statement is used to impose constraints on the "student" table.

Below is the query to create a table student with a set of constraints.

```sql
     CREATE TABLE  student(
     student_id INTEGER PRIMARY KEY,
     student_Name TEXT UNIQUE,
     department TEXT NOT NULL CHECK (Department IN ('CSE', 'ECE', 'EEE')); 
```

- **PRIMARY KEY** can be utilized to uniquely identify a row in a table.  
    When attempting to insert a row with the same value as an existing row in the table, a constraint violation will occur, preventing the insertion of the new row.
- **UNIQUE** columns contain distinct values for each row, similar to "PRIMARY KEY" columns, but unlike primary key columns, a table can have multiple unique columns..
- **NOT NULL** columns must have a value assigned to them.  
    When attempting to insert a row without providing a value for a "NOT NULL" column, a constraint violation will occur, preventing the insertion of the new row.
- **CHECK** constraint is used to enforce specific conditions on column values in a table. It ensures that only valid data that meets the defined condition can be inserted or updated in the column. If a value violates the condition, the database rejects the operation.  
    Example: _department TEXT CHECK (department IN ('CSE', 'ECE', 'EEE'))_  
    This ensures that the department column can only contain the values 'CSE', 'ECE', or 'EEE'. Any attempt to insert or update a value outside this list will result in an error.
  
To add constraints to existing tables, you can use the `ALTER TABLE` statement. Here's how you can add different types of constraints:
1. **Adding a PRIMARY KEY constraint:**
```
ALTER TABLE table_name 
ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);
```
2. **Adding a UNIQUE constraint:**
```
ALTER TABLE table_name 
ADD CONSTRAINT constraint_name UNIQUE (column_name);
```
3. **Adding a NOT NULL constraint:**
	_Note: Adding a NOT NULL constraint is a bit trickier because the column must not contain any NULL values before you add the constraint._
```
ALTER TABLE table_name 
ALTER COLUMN column_name SET NOT NULL;
```
4. **Adding a CHECK constraint:**
```
ALTER TABLE table_name 
ADD CONSTRAINT constraint_name CHECK (condition);
```

**Example:**

Let's say you have a table named `employee` and you want to add a unique constraint to the `employee_Name` column and a check constraint to the salary column.

```
ALTER TABLE employee 
ADD CONSTRAINT unique_employee_name UNIQUE (employee_Name);  

ALTER TABLE employee 
ADD CONSTRAINT check_salary CHECK (salary > 0);
```

**Complete code for your reference:**

```
-- Adding a PRIMARY KEY constraint: 
ALTER TABLE table_name 
ADD CONSTRAINT constraint_name PRIMARY KEY (column_name);  

-- Adding a UNIQUE constraint: 
ALTER TABLE table_name 
ADD CONSTRAINT constraint_name UNIQUE (column_name);  

-- Adding a NOT NULL constraint: 
ALTER TABLE table_name 
ALTER COLUMN column_name SET NOT NULL;  

-- Adding a CHECK constraint: 
ALTER TABLE table_name 
ADD CONSTRAINT constraint_name CHECK (condition);
```

# Date

### All
```
-- Current date only
SELECT CURRENT_DATE;

-- Current date and time
SELECT CURRENT_TIMESTAMP;

-- In SQLite, same as:
SELECT DATE('now');
SELECT DATETIME('now');

-- Year from a date
SELECT strftime('%Y', '2025-08-08') AS year;

-- Month
SELECT strftime('%m', '2025-08-08') AS month;

-- Day
SELECT strftime('%d', '2025-08-08') AS day;

-- Add 7 days
SELECT DATE('2025-08-08', '+7 days');

-- Subtract 2 months
SELECT DATE('2025-08-08', '-2 months');

-- Add 1 year and 3 days
SELECT DATE('2025-08-08', '+1 year', '+3 days');

-- First day of the month
SELECT DATE('2025-08-08', 'start of month');

-- Last day of the month
SELECT DATE('2025-08-08', 'start of month', '+1 month', '-1 day');

-- First day of the year
SELECT DATE('2025-08-08', 'start of year');

SELECT *
FROM orders
WHERE OrderDate > DATE('now', '-30 days'); -- Last 30 days

SELECT julianday('2025-08-08') - julianday('2025-07-01') AS days_diff;

-- Format: Day/Month/Year
SELECT strftime('%d/%m/%Y', '2025-08-08') AS formatted_date;

-- Format: Month name, Year
SELECT strftime('%m', '2025-08-08') || '-' || strftime('%Y', '2025-08-08') AS month_year;
```

---
# Transaction 
A **transaction** in SQL is a sequence of one or more SQL operations that are treated as a **single unit of work**.  
Either **all** operations succeed (**commit**) or **none** of them take effect (**rollback**).

You usually use transactions when:
- You’re **inserting** into multiple tables.
- You need to **update** multiple rows that must stay consistent.
- You want the ability to **undo** if something goes wrong.

### **ACID Properties**
##### **A – Atomicity**
- _All or nothing_.
- If one part of the transaction fails, the entire transaction is rolled back.
- Example: If you transfer money from account A to account B and the credit to B fails, the debit from A is also undone.
##### **C – Consistency**
- The database moves from one **valid state** to another valid state.
- All integrity constraints (e.g., primary keys, foreign keys, NOT NULL) remain satisfied after the transaction.
##### **I – Isolation**
- Transactions don’t interfere with each other.
- Even if many users run transactions at the same time, the result is the same as if they were run one after another.
##### **D – Durability**
- Once a transaction is committed, the changes are permanent, even if the system crashes immediately after
##### **Why ACID Matters**
Without ACID:
- **Atomicity problem** → You debit one account but don’t credit the other.
- **Consistency problem** → Database ends up with wrong totals.
- **Isolation problem** → Two transfers might overwrite each other’s changes.
- **Durability problem** → You commit the transfer but lose it after a crash.

### **Locking Mechanism**
Locking mechanisms are crucial for maintaining data consistency and integrity in multi-user database environments. They prevent concurrent transactions from interfering with each other and ensure that data is accessed and modified in a predictable and reliable manner.

Two common types of locks are row-level locks and table-level locks.
##### Row-Level Locks
- Restricts to rows within a table
-  This allows multiple transactions to concurrently access and modify different rows of the same table without blocking each other
-  This leads to higher concurrency and improved performance, especially in situations with frequent updates to different rows.

Advantages :
- **High Concurrency:** Multiple transactions can operate on different rows of the same table concurrently.
- **Reduced Contention:** Less blocking and waiting time for transactions.
- **Improved Performance:** Faster transaction processing due to increased concurrency.

Disadvantages of Row-Level Locks:
- **Increased Overhead:** Managing a large number of row-level locks can consume significant system resources.
- **Potential for Deadlocks:** Deadlocks can occur if two or more transactions are waiting for each other to release locks on rows.
##### Table Level Locks
- Locks the entire table
- Can significantly reduce concurrency 

Advantages - 
- **Simpler Management:** Fewer locks to manage compared to row-level locks.
- **Lower Overhead:** Less system resources are required to manage table-level locks.
Disadvantages - 
- **Reduced Concurrency:** Only one transaction can access the table at a time.
- **Increased Contention:** Transactions may have to wait longer for the table to become available.
- **Poorer Performance:** Slower transaction processing due to reduced concurrency.

### **Deadlocks**
- A deadlock occurs when two or more transactions are blocked indefinitely, waiting for each other to release the resources (locks) that they need. 
- Imagine two trains approaching a single-track bridge from opposite directions. Neither can proceed until the other backs up, but neither wants to back up. This is analogous to a deadlock in a database
Conditions for Deadlock:
1. **Mutual Exclusion:** A resource can only be held by one transaction at a time.
2. **Hold and Wait:** A transaction holding a resource can request additional resources.
3. **No Preemption:** Resources cannot be forcibly taken away from a transaction; they must be released voluntarily.
4. **Circular Wait:** A set of transactions exists such that each transaction is waiting for a resource held by another transaction in the set.
Example : Transaction A holds a lock on row 1 and is waiting for a lock on row 2. Transaction B holds a lock on row 2 and is waiting for a lock on row 1. Neither transaction can proceed, resulting in a deadlock.

**Handling Deadlocks**
Databases employ various strategies to handle deadlocks:
- **Deadlock Detection:** The database periodically checks for circular wait conditions.
- **Deadlock Prevention:** Strategies that prevent the four necessary conditions from occurring (e.g., ordering resource requests, limiting hold and wait).
- **Deadlock Avoidance:** Carefully allocating resources to prevent the possibility of deadlocks.
- **Deadlock Resolution (Victim Selection):** Choosing one or more "victim" transactions to be rolled back, releasing their locks and allowing other transactions to proceed. The choice of victim is often based on factors like the transaction's duration, importance, or the amount of work already done.

### **Isolation Levels**
- Isolation levels control the degree to which transactions are isolated from each other. 
- They define the visibility of changes made by one transaction to other concurrent transactions. 
	- Higher isolation levels provide ***greater consistency but can reduce concurrency.*** 
	- Lower isolation levels ***increase concurrency but may lead to various concurrency anomalies.***

Common Isolation Levels :
1. **Read Uncommitted:** The lowest level. Transactions can read uncommitted changes made by other transactions (dirty reads). This level offers the highest concurrency but is most prone to inconsistencies.
2. **Read Committed:** Transactions can only read committed changes made by other transactions. Dirty reads are prevented, but non-repeatable reads and phantom reads can still occur.
3. **Repeatable Read:** Transactions are guaranteed to see the same data throughout their execution. Non-repeatable reads are prevented, but phantom reads can still occur.
4. **Serializable:** The highest level. Transactions appear to execute as if they were running one at a time (serially). This level provides the highest consistency but can significantly reduce concurrency.
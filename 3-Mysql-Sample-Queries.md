**MySQL Sample Queries for Database and Table Operations**

## **Introduction**

This document provides sample MySQL queries for creating databases, tables, inserting data, and retrieving information. These queries will help you get started with MySQL database operations.

---

## **1. Creating a Database**

Before creating tables, you need a database. Run the following command to create a database named `ankita`:

```sql
CREATE DATABASE ankita;
```

To use this database, execute:

```sql
USE ankita;
```

---

## **2. Creating a Table**

Create a table named `Persons` with columns for personal details:

```sql
CREATE TABLE Persons (
    PersonID INT AUTO_INCREMENT PRIMARY KEY,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255) NOT NULL,
    Address VARCHAR(255),
    City VARCHAR(255)
);
```

---

## **3. Inserting Data into the Table**

Insert sample data into the `Persons` table:

```sql
INSERT INTO Persons (LastName, FirstName, Address, City)
VALUES
('Doe', 'John', '123 Main St', 'New York'),
('Smith', 'Jane', '456 Elm St', 'Los Angeles'),
('Brown', 'Charlie', '789 Oak St', 'Chicago');
```

---

## **4. Retrieving Data from the Table**

To view all records in the `Persons` table:

```sql
SELECT * FROM Persons;
```

To retrieve specific columns:

```sql
SELECT FirstName, LastName FROM Persons;
```

To filter records based on a condition:

```sql
SELECT * FROM Persons WHERE City = 'New York';
```

---

## **5. Updating Records**

To update an existing record:

```sql
UPDATE Persons
SET Address = '500 New St', City = 'Boston'
WHERE PersonID = 1;
```

---

## **6. Deleting Records**

To delete a record from the table:

```sql
DELETE FROM Persons WHERE PersonID = 2;
```

To delete all records from the table without deleting the structure:

```sql
DELETE FROM Persons;
```

---

## **7. Dropping a Table**

If you want to remove a table completely:

```sql
DROP TABLE Persons;
```

---

## **8. Dropping a Database**

To delete the entire database along with all tables:

```sql
DROP DATABASE ankita;
```

---

## **Conclusion**

This document provides basic MySQL queries to create, manage, and manipulate databases and tables. These commands are essential for working with MySQL and managing relational data efficiently.

For further details, refer to the [official MySQL documentation](https://dev.mysql.com/doc/).


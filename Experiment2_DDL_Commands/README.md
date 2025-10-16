# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Locations with the following columns:
LocationID as INTEGER
LocationName as TEXT
Address as TEXT

```sql
CREATE TABLE Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**

<img width="1333" height="323" alt="image" src="https://github.com/user-attachments/assets/3441281b-c411-412b-b123-ca1452b3cd32" />

**Question 2**
---
Write a SQL query to Add a new ParentsNumber column  as number and Adhar_Number as Number in the Student_details table.

```sql
ALTER TABLE Student_details
ADD ParentsNumber number;
ALTER TABLE Student_details
ADD Adhar_Number number;
```

**Output:**

<img width="1295" height="357" alt="image" src="https://github.com/user-attachments/assets/929a5e8d-b75a-4c62-bb86-c10632bc206d" />


**Question 3**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

```sql
CREATE TABLE Products(
ProductID PRIMARY KEY,
ProductName NOT NULL,
Price REAL NOT NULL CHECK (Price>0),
Stock INTEGER NOT NULL CHECK (Stock>=0)
);
```

**Output:**

<img width="1122" height="260" alt="image" src="https://github.com/user-attachments/assets/1fd631c7-e48e-4158-ac72-fa3f6b4fd772" />


**Question 4**
---
Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
designation as VARCHAR(50)
net_salary as NUMBER
dob as DATE

```sql
ALTER TABLE Companies
ADD designation varchar(50);

ALTER TABLE Companies
ADD net_salary number;

ALTER TABLE Companies
ADD dob date;
```

**Output:**

<img width="1251" height="330" alt="image" src="https://github.com/user-attachments/assets/f05e6943-8bdb-467f-b649-2d02744c5e85" />


**Question 5**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

```sql
CREATE TABLE Employees(
EmployeeID INTEGER PRIMARY KEY,
FirstName TEXT NOT NULL,
LastName TEXT NOT NULL,
Email TEXT UNIQUE,
Salary REAL CHECK (Salary>0),
DepartmentID  INTEGER,
FOREIGN KEY (DepartmentID)
REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="1335" height="335" alt="image" src="https://github.com/user-attachments/assets/01ef62ce-e1ad-4654-a29a-0acb2b673495" />


**Question 6**
---
Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL

```sql
CREATE TABLE orders(
ord_id TEXT NOT NULL CHECK (LENGTH(ord_id)=4),
item_id TEXT NOT NULL,
ord_date DATE NOT NULL,
ord_qty INTEGER,
cost INTEGER,
PRIMARY KEY(item_id,ord_date)
);
```

**Output:**

<img width="1170" height="203" alt="image" src="https://github.com/user-attachments/assets/6dba7e2e-e87d-4964-aacd-c387f70cd6bc" />


**Question 7**
---
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```sql
INSERT INTO Products(
ProductID,ProductName, Price, Stock)
SELECT ProductID, ProductName, Price, Stock
FROM Discontinued_products
```

**Output:**

<img width="981" height="252" alt="image" src="https://github.com/user-attachments/assets/c1fef863-e13b-4f9e-bc3f-e817b7143a26" />


**Question 8**
---
Insert a book with ISBN 978-1234567890, Title Data Science Essentials, Author Jane Doe, Publisher TechBooks, and Year 2024 into the Books table.

```sql
INSERT INTO Books(
ISBN, Title,Author,Publisher,Year)
VALUES('978-1234567890','Data Science Essentials','Jane Doe','TechBooks',2024)

```

**Output:**

<img width="1176" height="212" alt="image" src="https://github.com/user-attachments/assets/34dc3694-7211-4804-9922-22ac607aa0e5" />


**Question 9**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**
<img width="1124" height="197" alt="image" src="https://github.com/user-attachments/assets/28fd8f3b-06c3-46d9-b300-78bb15284bb9" />


**Question 10**
---
Insert the following products into the Products table:

|Name        |Category     |Price       |Stock|
|----------  |-----------  |----------  |----------|
|Smartphone  |Electronics  |800         |150|
|Headphones  |Accessories  |200         |300|

```sql
INSERT INTO Products(
Name,Category,Price,Stock)
VALUES ('Smartphone','Electronics',800,150);
INSERT INTO Products(
Name,Category,Price,Stock)
VALUES ('Headphones','Accessories',200,300)
```

**Output:**

<img width="1115" height="300" alt="image" src="https://github.com/user-attachments/assets/5b057950-7219-4563-8f48-9262055cb8c7" />

## COMPLETION STATUS

<img width="1138" height="281" alt="image" src="https://github.com/user-attachments/assets/17d8c543-cce4-4c1a-9513-91443c596302" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

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
-- In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
 

For example:

Test	Result
SELECT * FROM Products;
ProductID   Name             Category    Price       Stock
----------  ---------------  ----------  ----------  ----------
106         Fitness Tracker  Wearables
107         Laptop           Electronic  999.99      50
108         Wireless Earbud  Accessorie              100


```sql
-- INSERT INTO Products(ProductID,Name,Category,Price,Stock)
Values(106,'Fitness Tracker','Wearables',NULL,NULL);
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
Values(107,'Laptop','Electronic',999.99,50);
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
Values(108,'Wireless Earbud','Accessorie',NULL,100);
```

**Output:**

![Output1]![Screenshot (137)](https://github.com/user-attachments/assets/b42a9ad2-de12-4bda-ac64-a85bfa282d70)


**Question 2**
---
-- Create a table named Members with the following columns:

MemberID as INTEGER
MemberName as TEXT
JoinDate as DATE
For example:

Test	Result
pragma table_info('Members');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           MemberID    INTEGER     0                       0
1           MemberName  TEXT        0                       0
2           JoinDate    DATE        0                       0

```sql
-- create table Members(
MemberID INTEGER,
MemberName TEXT,
JoinDate DATE);
```

**Output:**

![Output2]![Screenshot (138)](https://github.com/user-attachments/assets/7d02c172-19c3-4ae4-9c1d-ba72f8c3362d)


**Question 3**
---
-- Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Error: FOREIGN KEY constraint failed


```sql
-- create table Shipments(
ShipmentID INTEGER primary key,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
foreign key(SupplierID) references Suppliers(SupplierID),
foreign key(OrderID)references Orders(OrderID));
```

**Output:**

![Output3]![Screenshot (139)](https://github.com/user-attachments/assets/c301b6ad-21b1-4ecc-bbcc-7c6af123f28a)


**Question 4**
---
-- Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.

For example:

Test	Result
SELECT * FROM Employee WHERE EmployeeID = 001;
EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
1           Sarah Parker  Manager     HR          60000

```sql
--insert into Employee (EmployeeID, Name, Position, Department,Salary)
Values(001,'Sarah Parker','Manager','HR',60000);
```

**Output:**

![Output4]![Screenshot (140)](https://github.com/user-attachments/assets/b5d2b48a-75f9-4fa8-94c8-0d052f2d2e11)


**Question 5**
---
--Write a SQL query to modify the Student_details table by adding a new column Email of type VARCHAR(50) and updating the column MARKS to have a default value of 0.

For example:

Test	Result
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS, Email) 
VALUES (104, 'Charlie', 'M', 'History', 88, 'charlie@example.com');
select * from student_details;
RollNo      Name        Gender      Subject     Email                MARKS
----------  ----------  ----------  ----------  -------------------  ----------
104         Charlie     M           History     charlie@example.com  88

```sql
-- INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS, Email)
VALUES (104, 'Charlie', 'M', 'History', 88, 'charlie@example.com');
select * from student_details;
```

**Output:**

![Output5]![Screenshot (147)](https://github.com/user-attachments/assets/5d472108-b6b2-4818-94f8-4dce7f2cbf42)


**Question 6**
---
-- Write a SQL query to Add a new column State as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           State       TEXT        0                       0


```sql
-- alter table Student_details
Add column State TEXT;6
```

**Output:**

![Output6]![Screenshot (141)](https://github.com/user-attachments/assets/9ea88c11-57ea-4e71-9da2-f6d221543293)


**Question 7**
---
-- Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.InvoiceID

```sql
-- create table Invoices(
InvoiceID INTEGER primary key,
InvoiceDate DATE,
DueDate DATE check(DueDate>InvoiceDate),
Amount REAL check(Amount>0));
```

**Output:**

![Output7]![Screenshot (142)](https://github.com/user-attachments/assets/ae1e221f-920e-4e7a-84ae-ad2741359732)


**Question 8**
---
-- Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	Result
select * from Employee;
EmployeeID  Name        Department  Salary
----------  ----------  ----------  ----------
201         John Doe    HR          50000
202         Jane Smith  Engineerin  75000
203         Emily Davi  Marketing   60000


```sql
-- insert into Employee
select EmployeeID, Name, Department, Salary
from Former_employees;
```

**Output:**

![Output8]![Screenshot (143)](https://github.com/user-attachments/assets/2fbe5378-8716-49a6-9a7a-830ed937df3b)


**Question 9**
---
-- Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
For example:

Test	Result
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;
OrderID     OrderDate   CustomerID
----------  ----------  ----------
1           2024-08-01  1

```sql
-- create table Orders(
OrderID INTEGER primary key,
OrderDate DATE not NULL,
CustomerID INTEGER,
foreign key (CustomerID)references Customers(CustomerID));
```

**Output:**

![Output9]![Screenshot (144)](https://github.com/user-attachments/assets/b9b761f7-6ab8-4293-9660-0f1c4f1e069b)


**Question 10**
---
-- Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName


```sql
-- create table Products(
ProductID  primary key,
ProductName NOT NULL,
Price real check(Price>0),
Stock integer check(Stock>=0));
```

**Output:**

![Output10]![image](https://github.com/user-attachments/assets/4f86adb1-79f2-498d-8f3f-e3db8538cb01)

#Module 1 SEB Grade Screenschot:
![Screenshot (146)](https://github.com/user-attachments/assets/c48c1ecb-5628-4154-a6c7-5295b87b2f77)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

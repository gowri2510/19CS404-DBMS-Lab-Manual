# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- CREATE OR REPLACE TRIGGER trg_after_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
INSERT INTO employee_log (emp_id, name, position, salary)
VALUES (:NEW.emp_id, :NEW.name, :NEW.position, :NEW.salary);
END;
/
SELECT table_name FROM user_tables WHERE table_name IN ('EMPLOYEES', 'EMPLOYEE_LOG');
CREATE TABLE employees (
emp_id NUMBER PRIMARY KEY,
name VARCHAR2(100),
position VARCHAR2(100),
salary NUMBER(10, 2)
);
CREATE OR REPLACE TRIGGER trg_after_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
INSERT INTO employee_log (emp_id, name, position, salary)
VALUES (:NEW.emp_id, :NEW.name, :NEW.position, :NEW.salary);
END;
/
INSERT INTO employees (emp_id, name, position, salary)
VALUES (1, 'Alice', 'Engineer', 75000);
SELECT * FROM employee_log
**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.
- ![{60925391-A98E-47A3-9D1F-D9C5160C8361}](https://github.com/user-attachments/assets/dd9287ec-0cc5-4e15-b8d0-2d119fd89205)


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
-
CREATE OR REPLACE TRIGGER prevent_sensitive_data_deletion
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
RAISE_APPLICATION_ERROR(-20001, 'Deletion not allowed on this table.');
END;


**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`
![{CF91E9D2-6EFB-4BAD-B380-EC2B31CE4019}](https://github.com/user-attachments/assets/5eb24405-7f2b-43d0-864a-215758691a7c)

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- CREATE TABLE products (
product_id NUMBER PRIMARY KEY,
product_name VARCHAR2(255),
-- other columns...
last_modified TIMESTAMP
);
CREATE OR REPLACE TRIGGER update_products_timestamp
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
:NEW.last_modified := SYSTIMESTAMP;
END;

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.
![{DE601572-739F-4F63-8C23-9908FEF5EE66}](https://github.com/user-attachments/assets/58373b3a-a7bf-4021-b040-5625dd80d7dc)

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- CREATE TABLE customer_orders (
order_id NUMBER PRIMARY KEY,
customer_id NUMBER,
order_date DATE,
order_total NUMBER,
-- Add other relevant columns as needed
order_status VARCHAR2(20) -- Added a sample column
);
CREATE TABLE audit_log (
table_name VARCHAR2(255),
update_count NUMBER
);
INSERT INTO audit_log (table_name, update_count) VALUES ('customer_orders', 0);
CREATE OR REPLACE TRIGGER customer_orders_update_audit
AFTER UPDATE ON customer_orders
BEGIN
UPDATE audit_log
SET update_count = update_count + 1
WHERE table_name = 'customer_orders';
END;
/
UPDATE customer_orders SET order_status = 'Shipped' WHERE order_id = 1;
SELECT update_count FROM audit_log WHERE table_name = 'customer_orders';
**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
![{AB3E4659-C66B-40AC-944D-718F35CEBC7E}](https://github.com/user-attachments/assets/91f74711-e63b-4cd9-9481-4464d70d61f2)

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- INSERT INTO audit_log (table_name, update_count) VALUES ('customer_orders', 0);
CREATE OR REPLACE TRIGGER customer_orders_update_audit
AFTER UPDATE ON customer_orders
BEGIN
UPDATE audit_log
SET update_count = update_count + 1
WHERE table_name = 'customer_orders';
END;
/
CREATE OR REPLACE TRIGGER check_employee_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
IF :NEW.salary < 3000 THEN
RAISE_APPLICATION_ERROR(-20002, 'Salary below minimum threshold.');
END IF;
END;
/
INSERT INTO employees (employee_id, employee_name, salary) VALUES (1, 'Alice Smith', 3
INSERT INTO employees (employee_id, employee_name, salary) VALUES (2, 'Bob Johnson', 2
SELECT * from employees;

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.
- ![{2F9ED37D-7A77-40E8-B0FB-519BE5CB095A}](https://github.com/user-attachments/assets/5c7948a5-e1f9-4b6b-b763-e4082059442d)


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.

# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;

    v_emp_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;

    no_data BOOLEAN := TRUE; -- To check if any row is fetched

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp_name, v_designation;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Name: ' || v_emp_name || ' | Designation: ' || v_designation);
        no_data := FALSE;
    END LOOP;

    CLOSE emp_cursor;

    IF no_data THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;.

**Output:**  
The program should display the employee details or an error message.
![{C30517B7-6910-44CF-9296-F76C77BD4DE0}](https://github.com/user-attachments/assets/6a8509be-a762-4d08-9e63-bb21efdfbfcc)

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- DECLARE
    -- Define parameterized cursor
    CURSOR emp_cursor(min_salary NUMBER, max_salary NUMBER) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN min_salary AND max_salary;

    -- Variables to hold fetched values
    v_emp_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    v_salary employees.salary%TYPE;

    -- Input parameters
    v_min_salary NUMBER := 40000;
    v_max_salary NUMBER := 70000;

    no_data BOOLEAN := TRUE; -- Flag to check if any rows are fetched

BEGIN
    -- Open and fetch from the cursor
    FOR emp_rec IN emp_cursor(v_min_salary, v_max_salary) LOOP
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name || 
                             ' | Designation: ' || emp_rec.designation || 
                             ' | Salary: ' || emp_rec.salary);
        no_data := FALSE;
    END LOOP;

    -- Raise NO_DATA_FOUND manually if no records were fetched
    IF no_data THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.
![{FD09DFFC-88F9-48DB-B35B-3072332E1DDB}](https://github.com/user-attachments/assets/29c8e394-a1b9-44d9-a34c-b230f410076d)

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- DECLARE
    -- Define parameterized cursor
    CURSOR emp_cursor(min_salary NUMBER, max_salary NUMBER) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN min_salary AND max_salary;

    -- Variables to hold fetched values
    v_emp_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    v_salary employees.salary%TYPE;

    -- Input parameters
    v_min_salary NUMBER := 40000;
    v_max_salary NUMBER := 70000;

    no_data BOOLEAN := TRUE; -- Flag to check if any rows are fetched

BEGIN
    -- Open and fetch from the cursor
    FOR emp_rec IN emp_cursor(v_min_salary, v_max_salary) LOOP
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name || 
                             ' | Designation: ' || emp_rec.designation || 
                             ' | Salary: ' || emp_rec.salary);
        no_data := FALSE;
    END LOOP;

    -- Raise NO_DATA_FOUND manually if no records were fetched
    IF no_data THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.
![{31EEB30C-AE55-4BF2-9C10-CD53A8E1D764}](https://github.com/user-attachments/assets/22d0d61c-7f96-44a0-a602-e098c0e575fb)

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- DECLARE
    -- Cursor to select all employee records
    CURSOR emp_cursor IS
        SELECT * FROM employees;

    -- Variable of cursor's row type
    emp_record emp_cursor%ROWTYPE;

    -- Flag to detect if any row is fetched
    no_data BOOLEAN := TRUE;

BEGIN
    -- Open the cursor
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO emp_record;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('ID: ' || emp_record.emp_id || 
                             ' | Name: ' || emp_record.emp_name || 
                             ' | Designation: ' || emp_record.designation || 
                             ' | Salary: ' || emp_record.salary);
        no_data := FALSE;
    END LOOP;

    CLOSE emp_cursor;

    -- Raise NO_DATA_FOUND if no data was fetched
    IF no_data THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;

**Output:**  
The program should display employee records or the appropriate error message if no data is found.
![{5F943D05-A7EB-43A6-9F5D-4E6CB3F7C58D}](https://github.com/user-attachments/assets/1cf506a5-b9e8-45d1-b16d-8e3b0de2fd56)

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- DECLARE
    CURSOR dept_cursor IS
        SELECT emp_id, salary
        FROM employees
        WHERE dept_no = 10
        FOR UPDATE;

    v_emp_id employees.emp_id%TYPE;
    v_salary employees.salary%TYPE;

    v_updated_count NUMBER := 0;

BEGIN
    FOR emp_rec IN dept_cursor LOOP
        -- Increase salary by 10%
        UPDATE employees
        SET salary = emp_rec.salary * 1.10
        WHERE emp_id = emp_rec.emp_id;

        v_updated_count := v_updated_count + 1;
        DBMS_OUTPUT.PUT_LINE('Updated salary for Employee ID: ' || emp_rec.emp_id);
    END LOOP;

    -- Check if any rows were updated
    IF v_updated_count = 0 THEN
        RAISE NO_DATA_FOUND;
    ELSE
        DBMS_OUTPUT.PUT_LINE(v_updated_count || ' employee(s) salary updated.');
    END IF;

    COMMIT;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified department.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
        ROLLBACK;
END;

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.
![{82756795-97E2-49CA-8FC5-2DCB980A6CBC}](https://github.com/user-attachments/assets/ddd05e71-8757-4813-ad14-fcdcdf5deced)

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 


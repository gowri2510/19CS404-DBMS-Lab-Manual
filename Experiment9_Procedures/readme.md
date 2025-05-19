# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- CREATE OR REPLACE PROCEDURE find_square(p_num IN NUMBER) IS
    v_square NUMBER;
BEGIN
    v_square := p_num * p_num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || p_num || ' is ' || v_square);
END;
BEGIN
    find_square(6);
END;
.

**Expected Output:**  
Square of 6 is 36
![{3998D41B-D0AB-4F93-B57B-841AB0B72B83}](https://github.com/user-attachments/assets/e9808a35-d510-43d7-9b1c-b83afb23bc14)


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- CREATE OR REPLACE FUNCTION get_factorial(p_num IN NUMBER)
RETURN NUMBER
IS
    v_result NUMBER := 1;
BEGIN
    IF p_num < 0 THEN
        RAISE_APPLICATION_ERROR(-20001, 'Factorial is not defined for negative numbers.');
    END IF;

    FOR i IN 1..p_num LOOP
        v_result := v_result * i;
    END LOOP;

    RETURN v_result;
END;
SELECT get_factorial(5) AS factorial_result FROM dual;.

**Expected Output:**  
Factorial of 5 is 120
![{3CB19130-862F-4B45-88AD-81F5881A5382}](https://github.com/user-attachments/assets/41b4bef2-0d92-4077-bdf8-86c4a3aae9db)


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- CREATE OR REPLACE PROCEDURE check_even_odd(p_num IN NUMBER) IS
BEGIN
    IF MOD(p_num, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(p_num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(p_num || ' is Odd');
    END IF;
END;
BEGIN
    check_even_odd(12);
END;
.

**Expected Output:**  
12 is Even
![{8A095045-E138-4789-97FA-7267C1609D32}](https://github.com/user-attachments/assets/62b9da22-05d7-4a5d-a9de-ff5abd7eb5a0)


---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- CREATE OR REPLACE FUNCTION reverse_number(p_num IN NUMBER)
RETURN NUMBER
IS
    v_num      NUMBER := p_num;
    v_reverse  NUMBER := 0;
    v_digit    NUMBER;
BEGIN
    WHILE v_num > 0 LOOP
        v_digit := MOD(v_num, 10);
        v_reverse := (v_reverse * 10) + v_digit;
        v_num := TRUNC(v_num / 10);
    END LOOP;

    RETURN v_reverse;
END;
SELECT reverse_number(1234) AS reversed FROM dual;


**Expected Output:**  
Reversed number of 1234 is 4321
![{560F277C-A5D1-43ED-99E7-D4B8A99AA2BC}](https://github.com/user-attachments/assets/1b8b77c7-4929-4083-affc-14ba6011c6ca)

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
-CREATE OR REPLACE PROCEDURE print_table(p_num IN NUMBER) IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || p_num || ':');
    
    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(p_num || ' x ' || i || ' = ' || (p_num * i));
    END LOOP;
END;
BEGIN
    print_table(5);
END;.

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50
![{94515D0B-EA79-4C89-B90E-6ADCD0776379}](https://github.com/user-attachments/assets/7740bef3-0878-4dd1-80ee-9e2e175e1b3c)

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.

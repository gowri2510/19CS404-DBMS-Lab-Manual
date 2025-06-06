# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

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

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### DECLARE
    num1 NUMBER := 45;
    num2 NUMBER := 80;
BEGIN
    IF num1 > num2 THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
    END IF;
END;

**Expected Output:**  
Greater number is: 80

---output:

![{22F3CD55-6E83-4C78-904E-959DDE0E001A}](https://github.com/user-attachments/assets/6a1f17f5-7a3e-46db-9096-8a1c985bba70)


## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### DECLARE
    n NUMBER := 10;       -- You can change this value as needed
    i NUMBER := 1;
    sum NUMBER := 0;
BEGIN
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
**Expected Output:**  
Sum of first 10 natural numbers is: 55

##`Output

![{AD0A6893-3F62-4843-9F46-3EA77747E68A}](https://github.com/user-attachments/assets/b9c891d1-5c7c-4528-8992-4403da03455e)


---

## 3. Write a PL/SQL program to generate Fibonacci series

### DECLARE
    n NUMBER := 7;        -- Number of terms to generate
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER := 3;        -- Starts from 3 since 0 and 1 are already printed
BEGIN
    DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
    DBMS_OUTPUT.PUT_LINE(a);
    DBMS_OUTPUT.PUT_LINE(b);

    WHILE i <= n LOOP
        c := a + b;
        DBMS_OUTPUT.PUT_LINE(c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;
END;

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8
##output:

![{EC6FA0DF-7E2B-48AD-A901-EB77C5D5D5F2}](https://github.com/user-attachments/assets/bbc1cea4-564a-4190-a0a2-f8c7e833df25)


---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### DECLARE
    n NUMBER := 1535;         -- Original number
    reversed NUMBER := 0;
    digit NUMBER;
    original NUMBER := 1535;  -- Store original value for display
BEGIN
    WHILE n > 0 LOOP
        digit := MOD(n, 10);              -- Get the last digit
        reversed := (reversed * 10) + digit;  -- Build the reversed number
        n := TRUNC(n / 10);               -- Remove the last digit
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('n = ' || original);
    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || reversed);
END;.

**Expected Output:**  
n = 1535  
Reversed number is 5351
**output

![{DCB5A935-6E32-481E-B7F7-67EB2C6F2934}](https://github.com/user-attachments/assets/0b2c91f9-d8e7-4971-bdf1-8150ff75db8d)


---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
    largest NUMBER;
BEGIN
    IF a >= b AND a >= c THEN
        largest := a;
    ELSIF b >= a AND b >= c THEN
        largest := b;
    ELSE
        largest := c;
    END IF;

    DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);
    DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || largest);
END;.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

**output:

![{683E2B77-EB84-4403-B766-D9652E94272C}](https://github.com/user-attachments/assets/07a65f6e-6ae2-42d8-aed5-57cfec811c4a)


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.

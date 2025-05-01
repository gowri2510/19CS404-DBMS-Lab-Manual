# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
-- How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table



For example:

Result
Frequency      TotalPrescriptions
-------------  ------------------
Every 3 weeks  1
Every 6 hours  1
Once           1
Once daily     4
Once daily at  1
Pending        1
Twice daily    1

```sql
-- select Frequency,COUNT(*) as TotalPrescriptions
from Prescriptions
group by Frequency;
```

**Output:**

!![image]![Screenshot (148)](https://github.com/user-attachments/assets/23fe790b-20ec-462c-a64a-63184e94e67e)



**Question 2**
---
-- How many medical records does each doctor have?

Sample table:MedicalRecords Table



For example:

Result
DoctorID    TotalRecords
----------  ------------
3           4
5           1
6           1
7           1
8           3

```sql
-- select DoctorID,COUNT(*) as TotalRecords
from MedicalRecords
group by DoctorID;
```

**Output:**

!![Screenshot (149)](https://github.com/user-attachments/assets/9b4f1c91-6d77-42a5-b63f-7350fa1854aa)


**Question 3**
---
-- How many patients have expired insurance coverage for each insurance company?

Sample table:Insurance Table



For example:

Result
InsuranceCompany  TotalExpiredPatients
----------------  --------------------
ABC Insurance     1
DEF Insurance     1
GHI Insurance     1
JKL Insurance     1
MNO Insurance     1
PQR Insurance     1
STU Insurance     1
VWX Insurance     1
XYZ Insurance     1
YZA Insurance     1

```sql
-- select InsuranceCompany,COUNT(*) as TotalExpiredPatients
from Insurance
group by InsuranceCompany;
```

**Output:**

!![Screenshot (150)](https://github.com/user-attachments/assets/034bb8ac-b19e-489f-82f2-ed7b1771e91d)


**Question 4**
---
-- Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
price_diff
----------
4.65

```sql
-- select (max(price)-min(price))as price_diff
from fruits;
```

**Output:**

!![Screenshot (151)](https://github.com/user-attachments/assets/de316c89-eb11-41e8-9252-d63826a90e14)


**Question 5**
---
-- Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8

```sql
-- select COUNT(*) as COUNT
from customer
where grade is not null;
```

**Output:**

!![Screenshot (152)](https://github.com/user-attachments/assets/dab2bb12-6223-4ca6-8e29-9f6290634a05)


**Question 6**
---
-- Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
4

```sql
-- select COUNT(DISTINCT age) as COUNT
from employee;
```

**Output:**

!![Screenshot (153)](https://github.com/user-attachments/assets/2259c65f-81b5-4bfa-b2b8-b830d318f752)


**Question 7**
---
-- Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
Average_Salary
--------------
1568750.0

```sql
-- select avg(income) as Average_Salary
from employee;
```

**Output:**

!![Screenshot (154)](https://github.com/user-attachments/assets/892f6efd-9189-4a73-871a-79bfea9b8fbb)


**Question 8**
---
-- Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

Sample table: customer1



For example:

Result
address     AVG(salary)
----------  -----------
Bhopal      8500.0
Indore      10000.0
Mumbai      6500.0


```sql
-- select address,AVG(salary) from customer1
group by address
having avg(salary)>5000;
```

**Output:**

!![Screenshot (155)](https://github.com/user-attachments/assets/0cdfd25b-a5c6-4775-b40e-20fbdf0b0263)


**Question 9**
---
-- Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.

Sample table: employee1



For example:

Result
occupation  AVG(workhour)
----------  -------------
Business    10.0
Engineer    12.0

```sql
-- select occupation,AVG(workhour) 
from employee1
group by occupation
having AVG(workhour) between 10 and 12;
```

**Output:**

!![Screenshot (156)](https://github.com/user-attachments/assets/5b475164-3692-4707-a0b2-ed8d1b1dad22)


**Question 10**
---
-- Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

Sample table: products



For example:

Result
category_id  Price
-----------  ----------
3            7.5


```sql
-- select category_id,min(price) as Price
from products
group by category_id
having min(price)<10;
```

**Output:**

!![Screenshot (157)](https://github.com/user-attachments/assets/8bdfe3d4-1447-4c40-a47c-b76c1d25524f)

Module 3 SEB Grade screenscot:
![image]![Screenshot (158)](https://github.com/user-attachments/assets/876c9705-7dcb-4e8f-8702-0f4204978e81)



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

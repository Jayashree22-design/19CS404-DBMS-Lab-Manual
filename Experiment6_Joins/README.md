# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

<img width="642" height="782" alt="image" src="https://github.com/user-attachments/assets/8f119d89-ca24-4253-bb1e-9b1aa76438f2" />


```sql
SELECT 
    s.name AS Salesman,
    c.cust_name AS cust_name,
    s.city
FROM 
    salesman s
JOIN 
    customer c
ON 
    s.city = c.city;
```

**Output:**

<img width="1023" height="615" alt="image" src="https://github.com/user-attachments/assets/d009c2d9-e367-4987-ba3f-3091de879724" />


**Question 2**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

<img width="803" height="727" alt="image" src="https://github.com/user-attachments/assets/fcaabbbd-ed77-4f9e-868c-fc695ee2029c" />


```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM orders AS o
INNER JOIN customer AS c
ON o.customer_id = c.customer_id
INNER JOIN salesman AS s
ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1432" height="655" alt="image" src="https://github.com/user-attachments/assets/a5ea1b82-5552-46a0-a43d-9925ae4da2ad" />


**Question 3**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

<img width="372" height="266" alt="image" src="https://github.com/user-attachments/assets/afada14e-2532-4069-9b6c-4737616ca6a5" />


```sql
SELECT 
    c.cust_name,
    o.ord_no,
    o.ord_date,
    o.purch_amt
FROM customer AS c
LEFT JOIN orders AS o
ON c.customer_id = o.customer_id;

```

**Output:**

<img width="793" height="618" alt="image" src="https://github.com/user-attachments/assets/8d2cb7fc-2fe6-4cc5-a4a3-247a547cf98c" />


**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman with the name 'Mc Lyon'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

<img width="422" height="120" alt="image" src="https://github.com/user-attachments/assets/f2729c2e-8c49-4bfe-b72c-18d437388f30" />


```sql

SELECT c.*
FROM customer AS c
LEFT JOIN salesman AS s
ON c.salesman_id = s.salesman_id
WHERE s.name = 'Mc Lyon' OR s.name IS NULL;

```

**Output:**
<img width="951" height="232" alt="image" src="https://github.com/user-attachments/assets/3c35a4c2-c6e8-4835-9575-1450c20a5dae" />


**Question 5**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

<img width="483" height="435" alt="image" src="https://github.com/user-attachments/assets/b27f7ad8-04dc-4ec8-88c6-9ed5375bc1a7" />


```sql
SELECT 
    c.cust_name,
    c.city AS city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM customer AS c
JOIN salesman AS s
ON c.salesman_id = s.salesman_id
WHERE c.grade < 300
ORDER BY c.customer_id ASC;

```

**Output:**

<img width="908" height="422" alt="image" src="https://github.com/user-attachments/assets/2636a9d3-e323-492a-b421-0c78fce94461" />


**Question 6**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city

<img width="561" height="490" alt="image" src="https://github.com/user-attachments/assets/c8ef1bb5-cce1-4415-88a4-ac1902a1261e" />

```sql
    o.ord_no,
    o.purch_amt,
    c.cust_name,
    c.city
FROM orders AS o
JOIN customer AS c
ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**

<img width="791" height="260" alt="image" src="https://github.com/user-attachments/assets/bbfb431e-d7e2-4bf1-b5f4-68d6b3538707" />

**Question 7**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.

<img width="585" height="320" alt="image" src="https://github.com/user-attachments/assets/bed55447-460c-4bd6-885b-21c525dec4f6" />


```sql
SELECT p.*
FROM patients AS p
INNER JOIN appointments AS a
ON p.patient_id = a.patient_id
WHERE a.appointment_date BETWEEN '2024-02-01' AND '2024-02-28';

```

**Output:**

<img width="1178" height="207" alt="image" src="https://github.com/user-attachments/assets/794ea05a-a8b6-4156-87f6-c77000bff1f0" />


**Question 8**
---
Write the SQL query that achieves the selection of the "nurse_id" from the "nurses" table (aliased as "n") and the "department_name" from the "departments" table, with an inner join on the "department_id" column and conditions filtering for a nurse with the first name 'David' and last name 'Moore'.

<img width="495" height="315" alt="image" src="https://github.com/user-attachments/assets/ae2c712a-d84a-4292-b620-54f8d9496100" />

```sql
SELECT 
    n.nurse_id,
    d.department_name
FROM nurses AS n
INNER JOIN departments AS d
ON n.department_id = d.department_id
WHERE n.first_name = 'David'
  AND n.last_name = 'Moore';
```

**Output:**
<img width="493" height="208" alt="image" src="https://github.com/user-attachments/assets/e60eeef8-5bc5-4076-b913-42e2d384453e" />


**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a date of birth after '1990-01-01'.

<img width="462" height="315" alt="image" src="https://github.com/user-attachments/assets/ab3e74de-e0a2-4296-9fc5-627f0b73ef8a" />


```sql
SELECT 
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM patients AS p
INNER JOIN doctors AS d
ON p.doctor_id = d.doctor_id
WHERE p.date_of_birth > '1990-01-01';

```

**Output:**

<img width="411" height="202" alt="image" src="https://github.com/user-attachments/assets/d56ef2e9-5e0a-4caa-8cd3-6a38ed881bbb" />


**Question 10**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.

<img width="463" height="465" alt="image" src="https://github.com/user-attachments/assets/c28e3c93-2162-46dc-ba3a-e6e401185df0" />

```sql
SELECT 
    c.cust_name,
    c.city AS city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM customer AS c
JOIN salesman AS s
ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;


```

**Output:**

<img width="1025" height="468" alt="image" src="https://github.com/user-attachments/assets/58cf329c-c512-45ca-96f8-33beffed092b" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.

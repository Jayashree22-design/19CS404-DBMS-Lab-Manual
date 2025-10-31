# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

<img width="342" height="628" alt="image" src="https://github.com/user-attachments/assets/fb69cead-d085-424b-947c-10f710b526ca" />


```sql
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id) > 1;

```

**Output:**

<img width="751" height="490" alt="image" src="https://github.com/user-attachments/assets/b963c252-d9be-4a8c-9692-85524fefd64d" />


**Question 2**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)

<img width="990" height="420" alt="image" src="https://github.com/user-attachments/assets/2da4e83d-ca01-41f8-a46f-d667373a5c45" />


```sql
SELECT *
FROM Medications 
WHERE dosage = (
       SELECT MAX(dosage)
       FROM Medications );
```

**Output:**

<img width="1003" height="422" alt="image" src="https://github.com/user-attachments/assets/abca695f-cbea-4b20-a0ee-9083c37e8ed5" />


**Question 3**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

<img width="723" height="590" alt="image" src="https://github.com/user-attachments/assets/fc99a38d-960f-4387-9b4e-9eeec6f8bcfd" />

```sql
SELECT * 
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income >  250000
    );
```

**Output:**

<img width="1233" height="407" alt="image" src="https://github.com/user-attachments/assets/bb535fbe-cb32-438a-a429-ba8ce4996fb5" />

**Question 4**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

<img width="586" height="578" alt="image" src="https://github.com/user-attachments/assets/a0027ffd-b183-472c-9e29-2e76a35639ba" />


```sql
SELECT *
FROM CUSTOMERS
WHERE age <30;
```

**Output:**

<img width="1053" height="471" alt="image" src="https://github.com/user-attachments/assets/7f564934-2e24-4996-9034-802d3e8a036a" />


**Question 5**
---
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

<img width="1053" height="471" alt="image" src="https://github.com/user-attachments/assets/c91ced9b-fb6b-4d3c-a392-d9fe20584eb7" />


```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM orders O
JOIN salesman s ON o.salesman_id  = s.salesman_id
WHERE s.name = 'Paul Adam';
```

**Output:**

<img width="1111" height="303" alt="image" src="https://github.com/user-attachments/assets/61ee1064-8cfb-400d-9a5f-c0073b0bf92b" />


**Question 6**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

<img width="703" height="471" alt="image" src="https://github.com/user-attachments/assets/9d727a40-1c0f-4335-9c67-759ed699f359" />


```sql
SELECT *
FROM GRADES g
WHERE g.grade = (
    SELECT MIN(grade)
    FROM GRADES sub
    WHERE sub.subject = g.subject
);

```

**Output:**

<img width="1165" height="352" alt="image" src="https://github.com/user-attachments/assets/41fe8152-d368-4448-bbbd-e1d7eb489844" />


**Question 7**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

<img width="642" height="476" alt="image" src="https://github.com/user-attachments/assets/e8de9221-e30c-400f-b8e1-e9f396c9d8a5" />


```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 1000000
);
```

**Output:**

<img width="1276" height="352" alt="image" src="https://github.com/user-attachments/assets/e2a02e5a-a28d-45e4-9445-4e12ae77a864" />


**Question 8**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

<img width="430" height="417" alt="image" src="https://github.com/user-attachments/assets/ad8bf06b-2d7b-4a7a-b0ab-3a4c38492b39" />


```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**

<img width="586" height="370" alt="image" src="https://github.com/user-attachments/assets/129f8486-79b1-479c-a2eb-4d902ad4cf29" />


**Question 9**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

<img width="608" height="567" alt="image" src="https://github.com/user-attachments/assets/9e3f9ca4-5496-4c7c-9b0f-0b5168ffcfe6" />


```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM orders O
JOIN salesman s ON o.salesman_id  = s.salesman_id
WHERE s.city = 'New York';
```

**Output:**

<img width="1045" height="393" alt="image" src="https://github.com/user-attachments/assets/01246db2-05c0-4380-8277-31b3f396be54" />

**Question 10**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi
<img width="537" height="487" alt="image" src="https://github.com/user-attachments/assets/18224dc8-d633-4c2a-8e8f-b0baae1e55ad" />

```sql
SELECT *
FROM CUSTOMERS
WHERE address = 'Delhi';
```

**Output:**

<img width="1001" height="285" alt="image" src="https://github.com/user-attachments/assets/14ed8448-f5c0-48fa-a837-5f94dc5569f4" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.

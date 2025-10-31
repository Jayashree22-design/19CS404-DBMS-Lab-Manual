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

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.
Sample table: CUSTOMERS
<img width="1298" height="607" alt="Screenshot 2025-10-31 102606" src="https://github.com/user-attachments/assets/7acdabf4-4d4f-4422-a729-7af0610f16a8" />


```sql

SELECT*FROM CUSTOMERS
WHERE SALARY<2500;
```

**Output:**

<img width="1110" height="407" alt="image" src="https://github.com/user-attachments/assets/7f9c515d-d3ea-4c40-8edd-db9342a3d855" />


**Question 2**

Write a SQL query to List departments with names longer than the average length
Departments Table (attributes: department_id, department_name)

<img width="952" height="410" alt="image" src="https://github.com/user-attachments/assets/05168360-5eb2-420e-9de9-4907cdbdfdce" />

```sql
SELECT department_id, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name))
    FROM Departments
);
```

**Output:**

<img width="601" height="358" alt="image" src="https://github.com/user-attachments/assets/6bd66d35-1535-4dc3-ae7b-885d818cf65f" />


**Question 3**

Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.
Sample table: GRADES (attributes: student_id, student_name, subject, grade)

<img width="1262" height="560" alt="image" src="https://github.com/user-attachments/assets/1e7b4dd6-7a2f-4c03-be25-3451558c3475" />

```sql
SELECT student_name,grade
FROM GRADES g1
WHERE grade IN (SELECT MIN(grade)
FROM GRADES g2
WHERE g2.subject=g1.subject
);

```

**Output:**

<img width="688" height="390" alt="Screenshot 2025-10-31 103232" src="https://github.com/user-attachments/assets/0d1bdff6-7272-4747-bb6b-dd3261b03b5c" />


**Question 4**

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.
Sample table: CUSTOMERS

<img width="903" height="578" alt="image" src="https://github.com/user-attachments/assets/0b9cec2f-5177-4fd2-adec-4a1370a1820b" />

```sql
SELECT*FROM CUSTOMERS
WHERE SALARY=1500;
```

**Output:**

<img width="1117" height="301" alt="image" src="https://github.com/user-attachments/assets/38d89867-de7a-40e4-a094-01ac5d623b52" />


**Question 5**

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30
Sample table: CUSTOMERS

<img width="957" height="585" alt="image" src="https://github.com/user-attachments/assets/96d27380-159c-454f-b7e6-21b8ed8cf6b9" />

```sql
SELECT*FROM CUSTOMERS
WHERE ADDRESS='Delhi'
AND AGE<30
ORDER BY ID;
```

**Output:**

<img width="1115" height="321" alt="image" src="https://github.com/user-attachments/assets/9e1aa9f3-19a0-47d9-971b-1206eba3fb14" />

**Question 6**

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.
Sample table: CUSTOMERS

<img width="920" height="620" alt="image" src="https://github.com/user-attachments/assets/43a0eef4-8a88-459f-95cc-7ca1d1bd1ffe" />

```sql
SELECT*FROM CUSTOMERS
WHERE SALARY>4500;
```

**Output:**

<img width="1112" height="378" alt="image" src="https://github.com/user-attachments/assets/866c0368-5ec5-4c84-bf27-d1c32416bb31" />

**Question 7**

From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.
Note: date should be yyyy-mm-dd format

<img width="1257" height="567" alt="image" src="https://github.com/user-attachments/assets/fd44f1d7-0cc6-49c8-abd2-aa5ee097e1cf" />



```sql
SELECT ord_no,purch_amt,ord_date,customer_id,salesman_id
FROM ORDERS
WHERE purch_amt> (SELECT AVG(purch_amt)
FROM ORDERS
WHERE ord_date='2012-10-10'
);
```

**Output:**

<img width="1157" height="405" alt="image" src="https://github.com/user-attachments/assets/440b84a3-e0ea-4931-a50b-b3c6d2e6ac31" />

**Question 8**

From the following tables write a SQL query to find all orders generated by New York-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id


<img width="1282" height="722" alt="Screenshot 2025-10-31 104441" src="https://github.com/user-attachments/assets/5c7e5088-913d-4b66-b0f6-f9df7d83c4d3" />


```sql

SELECT ord_no,purch_amt,ord_date,customer_id,salesman_id
FROM orders
WHERE salesman_id IN (SELECT(salesman_id)
FROM salesman
WHERE city='New York'
);

```

**Output:**

<img width="1141" height="406" alt="Screenshot 2025-10-31 104550" src="https://github.com/user-attachments/assets/970c4250-4409-48b1-b21c-9445a4c40bdd" />


**Question 9**

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi
Sample table: CUSTOMERS


<img width="836" height="581" alt="image" src="https://github.com/user-attachments/assets/95c68cc7-a666-4759-aa4e-005ec63d31df" />

```sql
SELECT*FROM CUSTOMERS
WHERE ADDRESS='Delhi';

```

**Output:**


<img width="1113" height="308" alt="image" src="https://github.com/user-attachments/assets/d6ea4161-9cd1-4e32-bf84-16a9e8f73592" />

**Question 10**

Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh


<img width="1012" height="607" alt="image" src="https://github.com/user-attachments/assets/fcfa3a48-46ca-4630-bf8f-512de842e3c3" />


```sql
SELECT id,name,age,city,income
FROM Employee
WHERE age < (SELECT AVG(age)
FROM Employee
WHERE income>250000
);
```

**Output:**


<img width="1282" height="447" alt="image" src="https://github.com/user-attachments/assets/b759c240-020c-48b5-bf2b-25f6c9c14538" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.

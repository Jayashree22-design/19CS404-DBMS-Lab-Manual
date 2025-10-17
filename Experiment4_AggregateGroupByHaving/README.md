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

What is the count of male and female patients?

<img width="919" height="433" alt="Screenshot 2025-10-17 112733" src="https://github.com/user-attachments/assets/65a51bfb-bbe3-4305-b19b-24c6447278f4" />

```sql
SELECT
Gender,
COUNT(*) AS TotalPatients
FROM
Patients
GROUP BY
Gender;
```

**Output:**

<img width="583" height="315" alt="Screenshot 2025-10-17 111050" src="https://github.com/user-attachments/assets/993f0e80-68f8-4044-b5f7-7344de93336a" />

**Question 2**

How many prescriptions were written for each medication?

<img width="909" height="582" alt="Screenshot 2025-10-17 111126" src="https://github.com/user-attachments/assets/6793d76f-c163-4d1c-98a2-5bf7fb1100b3" />


```sql
SELECT 
Medication,
COUNT(*) AS TotalPrescriptions
FROM
Prescriptions
GROUP BY
Medication;
```

**Output:**

<img width="688" height="676" alt="Screenshot 2025-10-17 111207" src="https://github.com/user-attachments/assets/1fcc976b-d6ee-4bf8-8d87-d9e80f3e02c0" />


**Question 3**

How many appointments are scheduled for each doctor?

<img width="901" height="493" alt="Screenshot 2025-10-17 111241" src="https://github.com/user-attachments/assets/034d5fa1-3068-4a65-98c9-cce3c3eb50ec" />


```sql
SELECT DoctorID,COUNT(AppointmentID) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;

```

**Output:**

<img width="621" height="574" alt="Screenshot 2025-10-17 111327" src="https://github.com/user-attachments/assets/44a549e5-fec9-437e-bfef-4e2954f59570" />


**Question 4**

Write a SQL query to find the shortest email address in the customer table?

<img width="624" height="423" alt="Screenshot 2025-10-17 111408" src="https://github.com/user-attachments/assets/d01d094f-b844-442f-a41c-a1f997455e69" />


```sql
SELECT name,email,LENGTH(email) AS min_email_length
FROM customer
ORDER BY LENGTH(email) ASC
LIMIT 1;
```

**Output:**

<img width="916" height="276" alt="Screenshot 2025-10-17 111448" src="https://github.com/user-attachments/assets/cfddbd56-ad27-4094-ac6f-6a99fe327889" />


**Question 5**

Write a SQL query to find the number of employees whose age is greater than 32.

<img width="765" height="423" alt="Screenshot 2025-10-17 111528" src="https://github.com/user-attachments/assets/94cb57fb-676b-4573-9bcf-242ae580907b" />


```sql
SELECT COUNT(*) AS COUNT
FROM employee
WHERE age>32;

```

**Output:**

<img width="324" height="277" alt="Screenshot 2025-10-17 111600" src="https://github.com/user-attachments/assets/c4768f11-4f92-4b84-aab2-722d6f25b8d5" />


**Question 6**

Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

<img width="752" height="431" alt="Screenshot 2025-10-17 111654" src="https://github.com/user-attachments/assets/04ea3e82-3ba4-4e53-8f73-79546d8c6ebc" />


```sql
SELECT AVG(income) AS avg_income
FROM employee
WHERE name LIKE 'A%';
```

**Output:**

<img width="335" height="274" alt="Screenshot 2025-10-17 111740" src="https://github.com/user-attachments/assets/8a6a5e4a-4692-459f-a1c5-f3966b1faae7" />


**Question 7**

Write a SQL query to  find the average salary of all employees?

<img width="605" height="449" alt="Screenshot 2025-10-17 111826" src="https://github.com/user-attachments/assets/e401d76b-708f-4a8b-af43-5bd957b702d4" />


```sql
SELECT AVG(income) AS Average_Salary FROM employee;
```

**Output:**

<img width="433" height="270" alt="Screenshot 2025-10-17 111858" src="https://github.com/user-attachments/assets/180fd280-fcaf-4e2d-b8e9-c46d3eceab7f" />


**Question 8**

Write the SQL query that accomplishes the grouping of data by age, calculates the average income for each age group, and includes only those age groups where the average income falls between 300,000 and 500,000.

<img width="1191" height="414" alt="Screenshot 2025-10-17 111943" src="https://github.com/user-attachments/assets/a86b9031-d7c2-4333-93f4-d3cb0c2d9d19" />


```sql
SELECT age,AVG(income) AS 'AVG(income)'
FROM employee
GROUP BY age
HAVING AVG(income) BETWEEN 300000 AND 500000;
```

**Output:**

<img width="538" height="300" alt="Screenshot 2025-10-17 112038" src="https://github.com/user-attachments/assets/329329bf-1400-422b-93b0-fc7c4f13e76a" />


**Question 9**

Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

<img width="1209" height="519" alt="Screenshot 2025-10-17 112112" src="https://github.com/user-attachments/assets/74e118ad-ac06-4dfb-a13f-26c7f2cefdb5" />


```sql
SELECT city,SUM(income) AS Income
FROM employee
GROUP BY city
HAVING SUM(income)>200000;

```

**Output:**

<img width="523" height="469" alt="Screenshot 2025-10-17 112925" src="https://github.com/user-attachments/assets/ea67caf0-aac6-4cfc-b91d-137b74e38c91" />

**Question 10**

Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

<img width="1141" height="486" alt="Screenshot 2025-10-17 112548" src="https://github.com/user-attachments/assets/1eca878e-5133-43c1-b67b-8355f9ebc95f" />


```sql
SELECT occupation,MIN(workhour) AS 'MIN(workhour)'
FROM employee1
GROUP BY occupation
HAVING MIN(workhour)>8;
```

**Output:**

<img width="557" height="419" alt="Screenshot 2025-10-17 112624" src="https://github.com/user-attachments/assets/21d1da1a-1e18-4960-b528-e3155dfca207" />

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**

Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.
<img width="896" height="445" alt="Screenshot 2025-10-17 103021" src="https://github.com/user-attachments/assets/a5de95d6-5f9d-47b4-a54b-9d75ea444205" />


```sql
UPDATE suppliers
SET address='58 Lakeview, Magnolia'
WHERE supplier_id=5;
```

**Output:**

<img width="1345" height="165" alt="Screenshot 2025-10-17 103343" src="https://github.com/user-attachments/assets/f17574d5-82a3-4719-84e5-c5f6bd88e190" />


**Question 2**

Write a SQL statement to Update the grade of all customers in Chennai city as  5. 


<img width="707" height="77" alt="Screenshot 2025-10-17 103936" src="https://github.com/user-attachments/assets/845788be-ff27-48cc-9094-77692d1d2e41" />


```sql
UPDATE Customer
SET grade=5
WHERE city='Chennai';
```

**Output:**

<img width="1271" height="350" alt="Screenshot 2025-10-17 104039" src="https://github.com/user-attachments/assets/f4bba189-2a4e-4dae-97b0-3ac7676b2ecb" />

**Question 3**

Write a SQL statement to change salary of employee to 8000 whose Employee ID is 105, if the existing salary is less than 5000.

<img width="1067" height="481" alt="Screenshot 2025-10-17 104212" src="https://github.com/user-attachments/assets/10697f42-8dfa-467d-8c6d-0d3dd20fdd0c" />


```sql
UPDATE Employees
SET salary=8000
WHERE employee_id=105 AND salary<5000;
```

**Output:**

<img width="1260" height="143" alt="Screenshot 2025-10-17 104305" src="https://github.com/user-attachments/assets/ac34be38-b98c-49cd-828e-104d2dba4529" />

**Question 4**

Write a SQL statement to double the availability of the product with product_id 1.

<img width="708" height="212" alt="Screenshot 2025-10-17 104350" src="https://github.com/user-attachments/assets/1f72e0ea-37bb-4b09-b8cc-df285ab36171" />


```sql
UPDATE products
SET availability=availability*2
WHERE product_id=1;
```

**Output:**

<img width="1185" height="193" alt="Screenshot 2025-10-17 104520" src="https://github.com/user-attachments/assets/e24ff502-9503-4343-8da0-3792ecbda71a" />



**Question 5**

Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.

<img width="1167" height="426" alt="Screenshot 2025-10-17 104624" src="https://github.com/user-attachments/assets/c2a661ca-84cb-4196-8c08-7e4150b454e6" />


```sql
UPDATE products
SET reorder_lvl=20
WHERE quantity<10 AND category='Snacks';
```

**Output:**

<img width="1206" height="274" alt="Screenshot 2025-10-17 104726" src="https://github.com/user-attachments/assets/ccc269c2-9461-43a0-91e4-4bb1c3048265" />


**Question 6**

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.

<img width="1026" height="319" alt="Screenshot 2025-10-17 104831" src="https://github.com/user-attachments/assets/37ebc924-818a-4e1b-9725-473a6698c7a5" />


```sql
DELETE FROM customer WHERE GRADE%2!=0
```

**Output:**

<img width="1884" height="261" alt="Screenshot 2025-10-17 104942" src="https://github.com/user-attachments/assets/ae6633ec-3acb-424b-9a60-03086206e1c2" />


**Question 7**

Write a SQL query to Delete All Doctors with a NULL Last Name

<img width="811" height="544" alt="Screenshot 2025-10-17 105044" src="https://github.com/user-attachments/assets/cc0d5233-3ac0-44eb-be0b-dd6aa5d10ae0" />


```sql
DELETE FROM doctors WHERE last_name is NULL;
```

**Output:**

<img width="1154" height="644" alt="Screenshot 2025-10-17 105131" src="https://github.com/user-attachments/assets/6eecb09d-add4-411c-82ea-afd4a7c687ac" />


**Question 8**

Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

<img width="685" height="415" alt="Screenshot 2025-10-17 105208" src="https://github.com/user-attachments/assets/5083683c-c44f-4b25-b929-e34f69445b54" />

```sql
DELETE FROM doctors WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**

<img width="1183" height="754" alt="Screenshot 2025-10-17 105254" src="https://github.com/user-attachments/assets/adfe6092-eef8-4637-b868-246962395ba9" />


**Question 9**

Write a SQL query to Delete a Specific Surgery whose ID is 3 or surgeon ID is 4.

<img width="806" height="580" alt="Screenshot 2025-10-17 105332" src="https://github.com/user-attachments/assets/72fee2ab-be83-408d-ad87-bb94a2f162ec" />


```sql
DELETE FROM surgeries WHERE surgery_id=3 OR surgeon_id=4;
```

**Output:**

<img width="1159" height="810" alt="Screenshot 2025-10-17 105425" src="https://github.com/user-attachments/assets/261234ad-6f80-4111-afff-e347385f621a" />


**Question 10**

Write a SQL query to Delete customers from 'customer' table where 'CUST_CITY' is not 'New York' and 'OUTSTANDING_AMT' is greater than 5000

<img width="1242" height="372" alt="Screenshot 2025-10-17 105520" src="https://github.com/user-attachments/assets/61003f1b-cd93-448b-bb62-bf1c67c4b13a" />


```sql
DELETE FROM customer WHERE CUST_CITY!='New York'AND OUTSTANDING_AMT>5000;
```

**Output:**

<img width="1722" height="324" alt="Screenshot 2025-10-17 105647" src="https://github.com/user-attachments/assets/4773466e-8c2d-4561-8edb-2d342a01a023" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.

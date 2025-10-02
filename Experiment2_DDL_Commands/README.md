# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**

Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

<img width="583" height="249" alt="Screenshot 2025-10-02 162252" src="https://github.com/user-attachments/assets/72132fb1-702c-4f01-8358-3920252b9139" />

```sql
INSERT INTO Student_details (RollNo,Name,Gender)
VALUES (204,'Samuel Black','M');
```

**Output:**

<img width="1032" height="256" alt="image" src="https://github.com/user-attachments/assets/3a848e72-efd6-4e0a-80b9-1abfce5deb11" />


**Question 2**

Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL

<img width="1269" height="170" alt="Screenshot 2025-10-02 162724" src="https://github.com/user-attachments/assets/d80eadf8-d9f2-4e93-baff-87a36986e7e6" />


```sql
CREATE TABLE orders(
    ord_id TEXT NOT NULL CHECK(LENGTH(ord_id)=4),
    item_id TEXT NOT NULL,
    ord_date DATE NOT NULL,
    ord_qty INTEGER,
    cost INTEGER,
    PRIMARY KEY(item_id,ord_date)
);
```

**Output:**

<img width="1117" height="146" alt="Screenshot 2025-10-02 162839" src="https://github.com/user-attachments/assets/e44cd4a8-fd03-4389-8680-85688d34f8af" />


**Question 3**

Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

<img width="1171" height="131" alt="Screenshot 2025-10-02 163053" src="https://github.com/user-attachments/assets/799ebb8d-8a8a-43f8-82f8-364515fef246" />


```sql
CREATE TABLE ProjectAssignments(
 AssignmentID INTEGER PRIMARY KEY,
 EmployeeID INTEGER,
 ProjectID INTEGER,
 AssignmentDate DATE NOT NULL,
 FOREIGN KEY (EmployeeID)REFERENCES Employees(EmployeeID)
 FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID));
```

**Output:**

<img width="1085" height="116" alt="Screenshot 2025-10-02 163157" src="https://github.com/user-attachments/assets/17c3258d-4426-4c78-a076-438cd46e8f1d" />


**Question 4**

Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

<img width="1253" height="159" alt="Screenshot 2025-10-02 163257" src="https://github.com/user-attachments/assets/192535d4-127d-442e-ac34-4cff01e38d1a" />

```sql
CREATE TABLE Attendance(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate DATE,
    Status TEXT CHECK(Status IN('Present','Absent','Leave')),
    FOREIGN KEY(EmployeeID)REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1082" height="127" alt="Screenshot 2025-10-02 163402" src="https://github.com/user-attachments/assets/956b0395-2250-455f-b593-6b59f8df64bd" />

**Question 5**

Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

<img width="651" height="230" alt="Screenshot 2025-10-02 163449" src="https://github.com/user-attachments/assets/0fc4a6c8-d32e-4081-9a70-550529027e65" />

```sql
INSERT INTO Products(ProductID,ProductName,Price,Stock)
SELECT ProductID,ProductName,Price,Stock
FROM Discontinued_products;
```

**Output:**

<img width="1200" height="251" alt="Screenshot 2025-10-02 163533" src="https://github.com/user-attachments/assets/446b87f7-baa9-4694-b308-2de7cd8b0118" />

**Question 6**

Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

<img width="947" height="300" alt="Screenshot 2025-10-02 163644" src="https://github.com/user-attachments/assets/fd033c96-ab0f-4add-b8a8-f470cb13dffe" />

```sql
ALTER TABLE Student_details
ADD Mobilenumber number;
```

**Output:**

<img width="1212" height="221" alt="Screenshot 2025-10-02 163753" src="https://github.com/user-attachments/assets/0c1d3864-74a7-4a17-9f15-2da1d6493a81" />

**Question 7**

Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

<img width="904" height="322" alt="Screenshot 2025-10-02 163831" src="https://github.com/user-attachments/assets/57567e67-d68f-4ec5-9aa8-7b51f1bc1c06" />

```sql
ALTER TABLE Companies RENAME COLUMN name TO first_name;
ALTER TABLE Companies ADD COLUMN mobilenumber number;
ALTER TABLE Companies ADD COLUMN DOB Date;
```

**Output:**

<img width="1303" height="300" alt="Screenshot 2025-10-02 163921" src="https://github.com/user-attachments/assets/789e1b34-20ef-4ac1-b369-52f2a2619e9a" />

**Question 8**

Create a table named Employees with the following constraints:
EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

<img width="1196" height="183" alt="Screenshot 2025-10-02 164024" src="https://github.com/user-attachments/assets/4c4f4e4d-96ba-4b16-849b-19d763b7f43c" />


```sql
CREATE TABLE Employees(
    EmployeeID INTEGER PRIMARY KEY,
    FirstName TEXT NOT NULL,
    LastName TEXT NOT NULL,
    Email TEXT UNIQUE,
    Salary REAL CHECK(Salary>0),
    DepartmentID INTEGER,
    FOREIGN KEY(DepartmentID) REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="1294" height="261" alt="Screenshot 2025-10-02 164123" src="https://github.com/user-attachments/assets/9a05aa9e-1e8d-4a8e-bd68-b042a9f974b5" />


**Question 9**

In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

<img width="920" height="235" alt="Screenshot 2025-10-02 164213" src="https://github.com/user-attachments/assets/13ec0348-cecf-4498-9be2-9188f7220d76" />


```sql
INSERT INTO BOOKS(ISBN,Title,Author,Publisher,Year)
VALUES('978-1234567890','Introduction to AI','John Doe',NULL,NULL);
INSERT INTO BOOKS(ISBN,Title,Author,Publisher,Year)
VALUES('978-9876543210','Deep Learning','Jane Doe','TechPress',2022);
INSERT INTO BOOKS(ISBN,Title,Author,Publisher,Year)
VALUES('978-1122334455','Cybersecurity Essentials','Alice Smith',NULL,2021);
```

**Output:**

<img width="1247" height="173" alt="Screenshot 2025-10-02 164338" src="https://github.com/user-attachments/assets/c4f2e2ad-d97b-4b1c-8099-34255d659ded" />


**Question 10**

Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE

<img width="862" height="224" alt="Screenshot 2025-10-02 164435" src="https://github.com/user-attachments/assets/c75ca1f8-e720-4846-ab7f-0e0ca98b62c5" />

```sql
CREATE TABLE Events(
EventID INTEGER,
EventName TEXT,
EventDate DATE);
```

**Output:**

<img width="1282" height="239" alt="Screenshot 2025-10-02 164533" src="https://github.com/user-attachments/assets/a3eb1b74-765a-4350-8031-5e309a67b894" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

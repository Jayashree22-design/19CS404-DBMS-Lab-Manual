# Experiment 1: Entity-Relationship (ER) Diagram

### 🎯 Objective:
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

### 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.


---

# 🧪Scenario : Restaurant Table Reservation and Ordering

Modern restaurants need efficient systems to manage reservations, table allocations, food ordering, billing, and staff assignments. Relying on manual methods often leads to booking conflicts, delayed service, billing errors, and overall customer dissatisfaction. To overcome these challenges, a structured restaurant management database is required.

**User Requirements:**  

- Store customer details and reservation history.
- Allow booking of tables with date, time, and number of guests.
- Manage tables with unique numbers and seating capacity.
- Record food orders linked to reservations.
- Maintain a menu of dishes with name, category, and price.
- Generate a single bill per reservation with payment details.
- Assign one waiter per reservation, while a waiter can serve many reservations.
- Ensure no double-booking of tables and maintain accurate data links.

## 📝Tasks:
1.Identify entities, relationships, and attributes.

2.Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).

3.Include:
    Cardinality & participation constraints
    Each reservation generates one bill, capturing total amount, payment method, and billing date.
    
4.Explain:
    Why you chose the entities and relationships.
    How you modeled prerequisites or billing.


### ER Diagram:
*Paste or attach your diagram here*  
<img width="709" height="431" alt="Screenshot 2025-09-27 084701" src="https://github.com/user-attachments/assets/5f637312-a81c-42f7-9548-7a68c85c3f9d" />


### Entities and Attributes

Customer: Attributes: CustomerID (Primary Key), Name, Phone, Email

Reservation: Attributes: ReservationID (Primary Key), Date, Time, NumberOfGuests, CustomerID (Foreign Key), TableID (Foreign Key), WaiterID (Foreign Key)

Table: Attributes: TableID (Primary Key), TableNumber, Capacity

Order: Attributes: OrderID (Primary Key), OrderDate, Status, TotalAmount, ReservationID (Foreign Key)

Dish: Attributes: DishID (Primary Key), DishName, Category, Price

Bill: Attributes: BillID (Primary Key), Amount, BillDate, PaymentMethod, ReservationID (Foreign Key)

Waiter: Attributes: WaiterID (Primary Key), Name, Shift, Experience

### Relationships and Constraints

Makes (Customer ↔ Reservation)

Cardinality: 1 Customer : N Reservations

Participation: Partial for Customer, Total for Reservation (every reservation must be made by a customer)

Assigned_To (Reservation ↔ Table)

Cardinality: 1 Reservation : 1 Table, but a Table can have multiple reservations over time

Participation: Total for Reservation

Includes (Reservation ↔ Order)

Cardinality: 1 Reservation : N Orders

Participation: Total for Order

Contains (Order ↔ Dish)

Cardinality: M:N (an order can contain multiple dishes, a dish can appear in multiple orders)

Requires a bridge entity (Order_Details)

Generates (Reservation ↔ Bill)

Cardinality: 1 Reservation : 1 Bill

Ensures one bill per reservation

Serves (Waiter ↔ Reservation)

Cardinality: 1 Waiter : N Reservations

### Extension (Billing):
Each reservation generates one bill capturing all orders and payment details.

### Design Choices:
Entities: Chose Customer, Reservation, Table, Order, Dish, Bill, and Waiter to represent key parts of a restaurant management system.

Relationships:

Customer Makes Reservation (1:N) – A customer can make multiple reservations.

Reservation Assigned to Table (1:1) – Each reservation is for one table, but tables can have multiple reservations over time.

Reservation Includes Order (1:N) – A reservation can have multiple orders.

Order Contains Dish (M:N) – Orders can include multiple dishes, and dishes can appear in multiple orders.

Reservation Generates Bill (1:1) – Each reservation produces a single bill.

Waiter Serves Reservation (1:N) – A waiter can serve multiple reservations.

Assumptions:

Each reservation is linked to exactly one table and one waiter.

Customers may have multiple reservations.

Bills are generated per reservation, not per order or dish.

Orders are created only for confirmed reservations.

### RESULT
Thus, this project effectively models a restaurant table reservation and ordering system through an ER diagram, clearly representing the relationships among customers, reservations, tables, orders, dishes, bills, and waiters.
Participation: Total on Reservation, Partial on Waiter


# Retail Database SQL

Two team projects from my Bachelor of Business Analytics covering the full relational database lifecycle for a fictional retail chain, Big M: first designing the data model, then implementing it in MySQL and querying it. Each project has a PDF write-up showing the design, code and results.

| Project | Focus | File |
|---|---|---|
| 1. Big M database design | ERD (Crow's Foot notation), assumptions, normalisation to 3NF | [Big M Database - ERD and Normalisation.pdf](./Big%20M%20Database%20-%20ERD%20and%20Normalisation.pdf) |
| 2. Big M database implementation | MySQL schema, data loading, SQL queries, data manipulation | [Big M Database - SQL Implementation.pdf](./Big%20M%20Database%20-%20SQL%20Implementation.pdf) |

---

## The business case

Big M is a retail chain with stores across Australia. Each store has several departments and employees, sells a range of products, and takes orders from customers in store and online. Management needed a database to track stores, departments, staff, products, customers and orders.

---

## 1. Database Design: ERD and Normalisation

**My contribution:** I led this project. I built the ERD and wrote the business assumptions, and reviewed the normalisation analysis completed by a teammate.

**What we did:** Turned the written business rules into a logical data model, then checked every entity against the normal forms.

**Approach**
1. Identified the entities: store, department, employee, product, customer and order.
2. Defined attributes, primary keys and foreign keys for each entity.
3. Resolved many-to-many relationships with junction entities.
4. Modelled recursive relationships (employee supervises employee, store supervises store).
5. Set connectivity and participation for each relationship, and recorded assumptions where the business rules were silent.
6. Validated the design with normalisation.

**Highlights**
- **Junction entities:** STOREDEPARTMENT resolves the store and department relationship, and ORDERPRODUCT resolves the order and product relationship. Ready and pick-up dates sit on ORDERPRODUCT because they can differ for each product in the same order.
- **Recursive relationships** capture the supervisor hierarchy for employees and for stores.
- **All eight entities are in 3NF**, with the reasoning for each documented in a normalisation table.

**Skills and tools:** Entity relationship modelling, Crow's Foot notation, keys, connectivity and participation, normalisation, documenting assumptions.

---

## 2. Database Implementation: MySQL

**My contribution:** We planned the build and loaded the data together as a team. I wrote queries 1, 4, 7 and 10 (staff listed by hourly salary, customers with no orders, total quantity sold up to a given date, and the latest payslips), and reviewed the data manipulation statements.

**What we did:** Built the database in MySQL (managed with phpMyAdmin), loaded the supplied data, wrote ten analytical queries, and ran four data manipulation statements.

**Database build**
- Created 10 tables with primary keys, foreign keys, composite keys and self-referencing keys.
- Loaded the data in dependency order so that no foreign key constraint was violated.
- Generated the physical model (designer view) to confirm all tables and relationships.

**Queries (10)**
- Joins across up to four tables (for example, Sports department supervisors by store)
- Subqueries with `NOT IN`, `AVG` and `MAX` (customers with no orders, products below the average price, latest payslips)
- Aggregation with `GROUP BY` and `SUM` (available stock per product, quantity sold up to a given date)
- Formatting with `CONCAT`, `DATE_FORMAT` and `CAST`, plus calculated values such as a 7.5% salary increase

**Data manipulation (4):** Inserted a new customer, an order and an order line, then updated the order line's pick-up date, following the foreign key chain from customer to order to order line.

**Skills and tools:** MySQL, phpMyAdmin, SQL DDL and DML, joins, subqueries, aggregation, data types and constraints.

---

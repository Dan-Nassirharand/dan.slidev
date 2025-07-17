---
layout: intro
---

# SQL
Dan Nassirharand

---

# Overview

- Relational Algebra (RA)
  - Relations
  - Operations
- Database Management System (DBMS)
- SQL
- Practicum


---

# Database

<div>
  "A database is an organized collection of structured information, or data, typically stored electronically in a computer system." - <a href="https://www.oracle.com/database/what-is-database/" target="_blank">Oracle</a>
</div>
<br><br><br>

- Tables (a.k.a. Relations)
  - Relational Schema
  - Attribute
  - Record

---

# Relational Schema

<div>
  "A database schema defines how data is organized within a relational database" - <a href="https://www.ibm.com/think/topics/database-schema" target="_blank">IBM</a>
</div>
<br><br>

- Acts as the blueprint for your database
  - What does it look like?
  - What type of data is stored?

<img src="/assets/table/schema.png" class="m-15 h-40" />

---

# Attribute

- Attributes are properties or characteristics of an entity
- Attributes are used to describe the entity.

\- <a href="https://www.geeksforgeeks.org/dbms/attributes-in-dbms/" target="_blank">GFG</a>


<img src="/assets/table/attribute.png" class="m-15 h-40" />

---

# Record

- An entity that exists within the relation

<img src="/assets/table/record.png" class="m-15 h-40" />
---

# Relational Algebra
https://www.geeksforgeeks.org/dbms/introduction-of-relational-algebra-in-dbms/

The main purpose of relational algebra is to define operators that transform one or more input relations to an output relation. - <a href="https://en.wikipedia.org/wiki/Relational_algebra" target="_blank">Wikipedia</a>

## Operations
- Selection (σ)
- Projection (π)
- Union (U)
- Set Difference (-)
- More ...

---

# SQL

<div>
SQL is a domain-specific language used to manage data, especially in a relational database management system (RDBMS). - <a href="https://en.wikipedia.org/wiki/SQL" target="_blank">Wikipedia</a>
</div>
<br><br>

- Defines a standard that is implemented by a DBMS
  - An implementation will differ from one DBMS to another
  - Most do not fully adhere to the standard


---

# Database Management System (DBMS)

<div>
  "A DBMS is a system that allows users to create, modify, and query databases while ensuring data integrity, security, and efficient data access." - <a href="https://www.geeksforgeeks.org/dbms/introduction-of-dbms-database-management-system-set-1/" target="_blank">GFG</a>
</div>
<br><br>

- Data Modeling
- Data Storage and Retrieval
- Concurrency Control
- Data Integrity and Security
- Backup and Recovery


---

# Practicum

---

### Staff

| SSO | Role | YOE | Team    |
|-----|------|-----|---------|
| 1   | P1   | 2   | Laundry |
| 2   | P2   | 1   | WiFi    |
| 3   | P3   | 3   | Cooking |
| 4   | P2   | 2   | Laundry |
| 5   | P1   | 1   | WiFi    |
| 6   | P3   | 2   | Cooking |

---

### Building

| Building | Team    |
|----------|---------|
| AP1      | Laundry |
| AP3      | Cooking |
| AP5      | WiFi    |

---

### Assignment

| SSO | Function |
|-----|----------|
| 1   | Software |
| 2   | QA       |
| 3   | Software |
| 4   | Software |
| 5   | Electrical |
| 6   | Mechanical |

---

### Function

| Function   | Description          | No. Staff |
|------------|----------------------|-----------|
| Software   | Writes code          | 57 |
| Electrical | Works on circuits    | 43 |
| Mechanical | Designs hardware     | 28 |
| QA         | Tests products       | 13 |

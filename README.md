# Nextcare General SQL Case Study

## Project Overview

This project involves writing optimized SQL queries against a fictional relational database schema for Nextcare & Allianz Partners. The goal was to demonstrate technical proficiency in querying relational databases, applying best practices for performance optimization, and ensuring query efficiency through proper indexing and execution plan analysis. 

## Business Tasks

The analysis aimed to:
1. Write a `SELECT` statement showing staff details for staff IDs 105, 108, 110, and 113.
2. Write a `SELECT` statement showing the member's full name, the number of orders for that member, and the total price.
3. Write a `SELECT` statement showing the order details, name and last name of the member, and the order promotion (if it exists).
4. Optimize the queries and propose supporting indexes to improve load times.

---

## Database Schema

<img width="600" height="400" alt="Database Schema" src="https://github.com/user-attachments/assets/12c3cc06-bc0b-4330-81ce-f543bcc594c0" />

*The schema consists of tables for Members, MembershipClub, Promotion, Staff, MemberOrder, and Roster.*

---

## Query 1: Staff Details

**Task:** Write a select statement showing staff details for staff 105, 108, 110 and 113.

```sql
SELECT s.StaffNo, s.Name, s.TelephoneNo, s.Email, s.Address 
FROM Staff AS s 
WHERE s.StaffNo IN (105, 108, 110, 113);
```

### Optimization Choices

| Rule | Description |
|------|-------------|
| Explicit Columns | Avoids using `SELECT *`, reducing I/O and network traffic. |
| Index Seek | Uses the `IN` operator with unquoted integers so the database can use an index seek on the primary key, avoiding a full table scan. |

---

## Query 2: Member Order Aggregation

**Task:** Write a select statement showing member full name, the number of orders for that member and total price.

```sql
SELECT 
    m.MemberNo, 
    m.FirstName + ' ' + m.LastName AS FullName, 
    o.OrderCount, 
    o.TotalPrice
FROM Members AS m
INNER JOIN (
    SELECT MemberNo, COUNT_BIG(*) AS OrderCount, SUM(Price) AS TotalPrice
    FROM MemberOrder
    GROUP BY MemberNo
) AS o ON o.MemberNo = m.MemberNo;
```

### Optimization Choices

| Rule | Description |
|------|-------------|
| Aggregate Before Join | The `MemberOrder` table is aggregated in a subquery *before* joining to `Members`. This prevents data duplication and reduces the memory footprint of the join. |
| COUNT_BIG | Used instead of `COUNT` to return a `bigint` and prevent arithmetic overflow on large datasets. |
| No Text in Aggregation | Text columns (`FirstName`, `LastName`) are excluded from the `GROUP BY` clause, keeping the aggregation operation highly efficient. |

---

## Query 3: Order Details with Optional Promotion

**Task:** Write a select statement showing the order details, name and last name of the member and the order promotion if it exists.

```sql
SELECT 
    o.OrderNo, 
    o.ShippingAddress, 
    o.Price, 
    m.FirstName, 
    m.LastName, 
    p.PromotionID, 
    p.PromotionType, 
    p.PromotionDate
FROM MemberOrder AS o
INNER JOIN Members AS m ON m.MemberNo = o.MemberNo
LEFT JOIN Promotion AS p ON p.PromotionID = o.PromotionID;
```

### Optimization Choices

| Rule | Description |
|------|-------------|
| INNER JOIN vs LEFT JOIN | Used `INNER JOIN` for `Members` because an order must have a member (mandatory). Used `LEFT JOIN` for `Promotion` because an order might not have a promotion (optional). |
| Driver Table | `MemberOrder` drives the query, which is the most efficient execution path for this specific dataset. |

---

## Performance Optimization & Indexing

To ensure the best possible load times, the following two covering indexes were proposed:

1. **`IX_MemberOrder_MemberNo`** 
   `ON MemberOrder (MemberNo) INCLUDE (Price)`
   *Why?* This acts as a covering index for Query 2. It allows the database engine to retrieve both the grouping key (`MemberNo`) and the aggregation value (`Price`) directly from the index, without ever touching the main table.

2. **`IX_MemberOrder_PromotionID`** 
   `ON MemberOrder (PromotionID)`
   *Why?* This index supports the `LEFT JOIN` in Query 3, allowing the optimizer to quickly find matching promotions (or nulls) for every order.

**Verification:** All queries and indexes should be verified using actual execution plans and `SET STATISTICS IO ON` to confirm logical reads are minimized.

---

## Tools & Technologies

- **SQL Server (T-SQL)** – Query writing, subqueries, joins, and aggregation.
- **Execution Plans** – Query performance tuning and index analysis.

## Project Structure
```
Nextcare-Allianz-Task3-SQL/
│
├── Assets/
│ └── database_schema.png
│
├── SQL Answer-Task3.pdf
├── SQL Answer-Task3.docx
└── README.md
```

# Author
**Mahmoud Abdallah**
Data Intelligence Reporting Specialist @ Nextcare Allianz Partners

## Any Questions
**Mahmoud_Abdallah20@outlook.com**

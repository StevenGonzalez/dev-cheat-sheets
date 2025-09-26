# SQL Cheat Sheet

Fast, practical reference for writing and understanding SQL across common relational databases (PostgreSQL, MySQL/MariaDB, SQL Server, SQLite). Examples aim to be portable; dialect-specific notes are called out where relevant.

## Table of Contents

- [Basics](#basics)
- [Query Fundamentals](#query-fundamentals)
- [Filtering and Predicates](#filtering-and-predicates)
- [Sorting and Limiting](#sorting-and-limiting)
- [Joins](#joins)
- [Aggregation](#aggregation)
- [Window Functions](#window-functions)
- [Subqueries and CTEs](#subqueries-and-ctes)
- [Modifying Data](#modifying-data)
- [Schema (DDL)](#schema-ddl)
- [Constraints](#constraints)
- [Indexes](#indexes)
- [Transactions](#transactions)
- [Dates and Times](#dates-and-times)
- [Strings and Patterns](#strings-and-patterns)
- [JSON (brief)](#json-brief)
- [Dialect Differences and Portability](#dialect-differences-and-portability)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Tools & References](#tools--references)

## Basics

Tables used in examples:

```text
users(id, name, email, created_at)
orders(id, user_id, total_cents, status, created_at)
```

## Query Fundamentals

```sql
-- Select specific columns
SELECT id, name FROM users;

-- Remove duplicates
SELECT DISTINCT status FROM orders;

-- Derived column (alias with AS)
SELECT id, total_cents / 100.0 AS total_dollars FROM orders;

-- Basic arithmetic and conditional
SELECT id,
       CASE WHEN status = 'refunded' THEN -total_cents ELSE total_cents END AS net_cents
FROM orders;
```

## Filtering and Predicates

```sql
-- Comparisons and logical operators
SELECT * FROM users
WHERE created_at >= DATE '2024-01-01' AND name <> 'Admin';

-- NULL handling
SELECT * FROM users WHERE email IS NULL;     -- use IS [NOT] NULL, not = NULL
SELECT COALESCE(email, 'n/a') AS email_or_na FROM users;  -- first non-NULL

-- IN, BETWEEN, LIKE
SELECT * FROM orders WHERE status IN ('new', 'paid', 'shipped');
SELECT * FROM orders WHERE total_cents BETWEEN 1000 AND 100000; -- inclusive
SELECT * FROM users WHERE name LIKE 'Jo%';    -- prefix; use ESCAPE for literal %/_
```

## Sorting and Limiting

```sql
SELECT id, total_cents
FROM orders
ORDER BY total_cents DESC, id ASC;

-- Pagination (syntax varies)
-- ANSI/PG/SQLite/MySQL
SELECT * FROM orders ORDER BY id LIMIT 10 OFFSET 20;
-- SQL Server
-- SELECT * FROM orders ORDER BY id OFFSET 20 ROWS FETCH NEXT 10 ROWS ONLY;
```

## Joins

```sql
-- Inner join: only matching rows
SELECT u.id, u.name, o.id AS order_id, o.total_cents
FROM users u
JOIN orders o ON o.user_id = u.id;

-- Left join: all left rows, NULLs for missing right
SELECT u.id, u.name, o.id AS order_id
FROM users u
LEFT JOIN orders o ON o.user_id = u.id;

-- Right/Full joins (not in SQLite)
-- RIGHT JOIN ...
-- FULL [OUTER] JOIN ...

-- Cross join (Cartesian product)
SELECT * FROM users CROSS JOIN orders;

-- Self join
SELECT a.id, b.id
FROM users a
JOIN users b ON b.id <> a.id;
```

## Aggregation

```sql
-- Basic aggregates with GROUP BY
SELECT user_id, COUNT(*) AS order_count, SUM(total_cents) AS total_cents
FROM orders
GROUP BY user_id;

-- Filter groups with HAVING
SELECT user_id, COUNT(*) AS order_count
FROM orders
GROUP BY user_id
HAVING COUNT(*) >= 5;

-- Grouping with expressions
SELECT DATE(created_at) AS day, SUM(total_cents) AS revenue
FROM orders
GROUP BY DATE(created_at)
ORDER BY day;
```

Common aggregate functions: COUNT, SUM, AVG, MIN, MAX.

## Window Functions

```sql
-- Running totals per user
SELECT user_id,
       created_at,
       total_cents,
       SUM(total_cents) OVER (PARTITION BY user_id ORDER BY created_at
                              ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total
FROM orders;

-- Rankings
SELECT id, total_cents,
       ROW_NUMBER() OVER (ORDER BY total_cents DESC) AS rn,
       RANK()       OVER (ORDER BY total_cents DESC) AS rnk
FROM orders;

-- LAG/LEAD to compare rows
SELECT id, user_id, total_cents,
       LAG(total_cents)  OVER (PARTITION BY user_id ORDER BY created_at) AS prev_total,
       LEAD(total_cents) OVER (PARTITION BY user_id ORDER BY created_at) AS next_total
FROM orders;
```

## Subqueries and CTEs

```sql
-- Subquery in WHERE
SELECT * FROM users
WHERE id IN (SELECT user_id FROM orders WHERE status = 'paid');

-- Correlated subquery
SELECT u.id, u.name,
       (SELECT COUNT(*) FROM orders o WHERE o.user_id = u.id) AS order_count
FROM users u;

-- CTE (Common Table Expression)
WITH totals AS (
  SELECT user_id, SUM(total_cents) AS total
  FROM orders
  GROUP BY user_id
)
SELECT u.id, u.name, t.total
FROM users u
JOIN totals t ON t.user_id = u.id
ORDER BY t.total DESC;
```

## Modifying Data

```sql
-- INSERT (single and multi-row)
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
INSERT INTO users (name, email) VALUES
  ('Bob', 'bob@example.com'),
  ('Carol', NULL);

-- UPDATE
UPDATE orders SET status = 'shipped'
WHERE id = 123 AND status = 'paid';

-- DELETE
DELETE FROM orders WHERE created_at < DATE '2023-01-01';

-- Upsert (dialect-specific)
-- PostgreSQL
-- INSERT INTO users (id, name, email) VALUES (1, 'A', 'a@x')
-- ON CONFLICT (id) DO UPDATE SET name = EXCLUDED.name, email = EXCLUDED.email;
-- MySQL/MariaDB
-- INSERT INTO users (id, name, email) VALUES (1, 'A', 'a@x')
-- ON DUPLICATE KEY UPDATE name = VALUES(name), email = VALUES(email);
-- SQL Server (use MERGE or TRY...CATCH pattern carefully)
```

## Schema (DDL)

```sql
-- Create table (portable types shown; adjust for your DB)
CREATE TABLE users (
  id          INTEGER PRIMARY KEY,
  name        VARCHAR(100) NOT NULL,
  email       VARCHAR(255) UNIQUE,
  created_at  TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE orders (
  id           INTEGER PRIMARY KEY,
  user_id      INTEGER NOT NULL,
  total_cents  INTEGER NOT NULL CHECK (total_cents >= 0),
  status       VARCHAR(20) NOT NULL,
  created_at   TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_orders_users FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Alter / Drop
ALTER TABLE users ADD COLUMN is_active BOOLEAN DEFAULT TRUE;
ALTER TABLE users DROP COLUMN is_active;         -- not supported in some older engines
DROP TABLE orders;
```

## Constraints

- PRIMARY KEY: unique identifier for each row
- NOT NULL: disallow NULLs
- UNIQUE: enforce uniqueness
- CHECK: validate column/expression
- FOREIGN KEY: reference to parent table (enforce referential integrity)

```sql
-- Examples
ALTER TABLE users ADD CONSTRAINT users_name_unique UNIQUE (name);
ALTER TABLE orders ADD CONSTRAINT non_negative_total CHECK (total_cents >= 0);
```

## Indexes

```sql
-- Basic index
CREATE INDEX idx_orders_user_id ON orders(user_id);

-- Composite index (column order matters!)
CREATE INDEX idx_orders_user_created ON orders(user_id, created_at);

-- Unique index
CREATE UNIQUE INDEX idx_users_email ON users(email);

-- Partial/filtered (dialect-specific; e.g., PostgreSQL)
-- CREATE INDEX idx_orders_paid ON orders(created_at) WHERE status = 'paid';
```

Guidelines:

- Index columns used in joins and selective filters.
- Prefer narrower indexes; avoid indexing columns with low selectivity (e.g., boolean) unless part of composite.
- Keep indexes updated; too many hurt writes.

## Transactions

```sql
-- Basic transaction
BEGIN;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;

-- Rollback on error
BEGIN;
  -- ...statements...
ROLLBACK;

-- Savepoint (nested rollback)
SAVEPOINT sp1;
-- ...
ROLLBACK TO SAVEPOINT sp1;
```

Isolation levels (support/keywords vary): READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE. Default differs by engine.

## Dates and Times

```sql
-- Current date/time
SELECT CURRENT_DATE, CURRENT_TIME, CURRENT_TIMESTAMP;

-- Extract parts
SELECT EXTRACT(YEAR FROM created_at) AS yyyy,
       EXTRACT(MONTH FROM created_at) AS mm
FROM orders;

-- Date arithmetic (syntax varies)
-- PostgreSQL
-- SELECT created_at + INTERVAL '7 days' FROM orders;
-- SQLite (date functions)
-- SELECT DATE(created_at, '+7 days') FROM orders;
```

## Strings and Patterns

```sql
-- Common string functions
SELECT LENGTH(name) AS len,
       SUBSTRING(name FROM 1 FOR 3) AS first3,
       LOWER(name) AS lower_name,
       TRIM(name) AS trimmed
FROM users;

-- Concatenation (varies):
-- PostgreSQL / SQLite: 'Hello ' || name
-- MySQL: CONCAT('Hello ', name)
-- SQL Server/MySQL: 'Hello ' + name (beware NULL concatenation rules)

-- LIKE patterns (case sensitivity depends on collation/dialect)
SELECT * FROM users WHERE name LIKE '%son%';
```

## JSON (brief)

JSON support is dialect-specific. Examples:

```sql
-- PostgreSQL: -> (get by key), ->> (text), #> (path)
-- SELECT data->>'name' AS name FROM events;

-- MySQL: JSON_EXTRACT / ->>
-- SELECT JSON_EXTRACT(data, '$.name') AS name FROM events;

-- SQL Server: JSON_VALUE
-- SELECT JSON_VALUE(data, '$.name') AS name FROM events;
```

## Dialect Differences and Portability

- LIMIT/OFFSET vs OFFSET/FETCH (SQL Server)
- Upsert syntax differs (ON CONFLICT vs ON DUPLICATE KEY vs MERGE)
- String concatenation operators/functions differ
- Data types and default values vary (e.g., BOOLEAN, TIMESTAMP)
- Full outer join not supported in all engines (e.g., SQLite)

Tip: When sharing SQL across engines, state the intended dialect and provide minimal notes for portability.

## Best Practices

- Select only the columns you need; avoid SELECT \* in production queries.
- Filter early and use appropriate indexes; check query plans (EXPLAIN / EXPLAIN ANALYZE).
- Prefer explicit JOIN syntax over implicit joins in WHERE.
- Use CTEs for readability; materialize only when necessary.
- Be cautious with OR on indexed columns (may inhibit index usage); consider UNION ALL.
- Normalize data appropriately; denormalize for analytics with care.
- Validate inputs to prevent SQL injection; use prepared statements/parameters.

## Troubleshooting

- Unexpected NULL behavior: remember `= NULL` is never true; use `IS NULL`.
- GROUP BY errors: include non-aggregated selected columns in GROUP BY (or aggregate them).
- Join explosions/duplicates: verify join keys and use DISTINCT only as a last resort.
- Collation/case-sensitivity surprises: check database/column collation.
- Timezone confusion: store UTC, convert at edges; prefer timestamptz where available.

## Tools & References

- Mode SQL Tutorial
- SQLBolt interactive lessons
- PostgreSQL, MySQL, SQLite, SQL Server official docs
- Use your DB’s EXPLAIN/EXPLAIN ANALYZE and graphical plan viewers

---

Quick tip: Keep a scratch file with sample tables and data (CREATE TABLE + INSERTs) to iterate on queries safely.

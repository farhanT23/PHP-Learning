# 📘 Basic SQL Documentation (MySQL)

## 🔰 Introduction

**SQL (Structured Query Language)** is the language used to interact with relational databases. Basic SQL forms the foundation for querying, retrieving, and filtering data.

This section covers the most commonly used commands that every developer should master before diving into more complex SQL.

---

## 📄 1. SELECT Statement

Used to retrieve data from one or more tables.

```sql
SELECT column1, column2 FROM table_name;
```

### Example:
```sql
SELECT name, email FROM users;
```

---

## 📄 2. SELECT * (All Columns)

Retrieves **all columns** from a table.

```sql
SELECT * FROM users;
```

---

## 🔍 3. WHERE Clause

Filters rows based on conditions.

```sql
SELECT * FROM users WHERE is_active = 1;
```

### Comparison Operators:
- `=` equals
- `!=` or `<>` not equal
- `<`, `>`, `<=`, `>=`
- `LIKE` (for partial matches)
- `IN` (match against multiple values)
- `BETWEEN` (range check)
- `IS NULL`, `IS NOT NULL`

---

## 🧠 4. Logical Operators

- `AND`: both conditions must be true
- `OR`: either condition can be true
- `NOT`: negates the condition

```sql
SELECT * FROM users
WHERE is_active = 1 AND is_verified = 1;
```

---

## 📊 5. ORDER BY

Sorts results in ascending (`ASC`) or descending (`DESC`) order.

```sql
SELECT * FROM users ORDER BY created_at DESC;
```

---

## ✨ 6. LIMIT

Restricts the number of rows returned.

```sql
SELECT * FROM users LIMIT 10;
```

### Use with OFFSET (for pagination):
```sql
SELECT * FROM users LIMIT 10 OFFSET 10;
```

---

## 🏷️ 7. Aliases (AS)

Rename a column or table temporarily in the result.

```sql
SELECT name AS username FROM users;
```

---

## 🧪 8. Sample Practice Queries

```sql
-- Get all active users
SELECT * FROM users WHERE is_active = 1;

-- Get top 5 newest users
SELECT name, email FROM users ORDER BY created_at DESC LIMIT 5;

-- Find users with name starting with 'A'
SELECT * FROM users WHERE name LIKE 'A%';

-- Get users with email in a specific list
SELECT * FROM users WHERE email IN ('a@example.com', 'b@example.com');
```

# 📘 SQL: Data Manipulation Language (DML)

## 🔰 Introduction

**DML (Data Manipulation Language)** consists of SQL commands used to **insert**, **update**, and **delete** data from a database. These commands do **not change the structure** of the table, only the data inside it.

---

## 📥 1. INSERT INTO

Used to add new records to a table.

### 🔹 Syntax:

```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```

### 🔹 Example:

```sql
INSERT INTO users (name, email, password)
VALUES ('Fahim', 'fahim@example.com', '123456');
```

> ✅ You must match the **column list** and **value list** order.

---

## ✏️ 2. UPDATE

Used to modify existing records.

### 🔹 Syntax:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2
WHERE condition;
```

### 🔹 Example:

```sql
UPDATE users
SET is_active = 0
WHERE id = 5;
```

> ⚠️ **Always use `WHERE`** with UPDATE to avoid changing all rows.

---

## ❌ 3. DELETE

Used to remove one or more records.

### 🔹 Syntax:

```sql
DELETE FROM table_name
WHERE condition;
```

### 🔹 Example:

```sql
DELETE FROM users
WHERE email = 'test@example.com';
```

> ⚠️ `DELETE` without a `WHERE` will **remove all records**.

---

## 🔁 4. REPLACE INTO

Acts like INSERT, but replaces the row if the **primary key or unique key** already exists.

### 🔹 Example:

```sql
REPLACE INTO users (id, name, email, password)
VALUES (1, 'Fahim', 'fahim@example.com', 'secret');
```

---

## ⛔ 5. TRUNCATE TABLE

Removes **all data** from a table — faster than `DELETE` but cannot be rolled back (no `WHERE` allowed).

```sql
TRUNCATE TABLE users;
```

---

## 🧪 Sample Practice Queries

```sql
-- Add a new user
INSERT INTO users (name, email, password) VALUES ('Anny', 'anny@example.com', 'abcd1234');

-- Deactivate all unverified users
UPDATE users SET is_active = 0 WHERE is_verified = 0;

-- Delete users with null emails
DELETE FROM users WHERE email IS NULL;

-- Replace a record (if exists, it will overwrite)
REPLACE INTO users (id, name, email, password) VALUES (10, 'Admin', 'admin@site.com', 'admin123');
```

---

## 🧠 Best Practices

| Practice                    | Why it's important                          |
|----------------------------|---------------------------------------------|
| Always use `WHERE`         | Prevents unintended full-table changes      |
| Use `LIMIT` with `UPDATE/DELETE` when testing | Avoids massive changes |
| Use transactions if needed | Ensures changes are atomic and safe         |
| Validate input in apps     | Prevents invalid data insertion             |
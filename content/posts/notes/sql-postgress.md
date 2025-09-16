
+++
authors = ["Devendran Nehru"]
title = "Kick start your SQL Journey with PostreSQL"
date = "2025-07-30"
description = "Notes for PostgreSQL"
tags = [
    "rdbms",
    "notes",
    "sql",
]
categories = [
    "Database",
    "StudyNotes",
]
series = ["StudyNotes"]
+++


# SQL Data Types Overview

SQL data types define the kind of data that can be stored in a column of a table. Choosing the correct data type is crucial for data integrity, performance, and efficient storage.

---

## 🧮 Numeric Data Types

| Data Type       | Description                               | Example Values      |
|-----------------|-------------------------------------------|---------------------|
| `INT` / `INTEGER`| Whole numbers (positive/negative)        | 1, -20, 5000        |
| `SMALLINT`       | Smaller range of whole numbers           | -32,768 to 32,767   |
| `BIGINT`         | Very large integers                      | Useful for IDs      |
| `DECIMAL(p,s)`   | Exact numeric value with fixed precision | DECIMAL(5,2) → 123.45 |
| `NUMERIC(p,s)`   | Same as DECIMAL                          |                     |
| `FLOAT(n)`       | Approximate floating-point               | 3.14159             |
| `REAL`           | Less precision than FLOAT                |                     |
| `BIT`            | Boolean-like (0 or 1)                    | 1, 0                |

---

## 🔤 Character/String Data Types

| Data Type         | Description                                           | Example        |
|-------------------|-------------------------------------------------------|----------------|
| `CHAR(n)`         | Fixed-length string (padded with spaces)             | CHAR(10)       |
| `VARCHAR(n)`      | Variable-length string                               | VARCHAR(255)   |
| `TEXT`            | Long text data (non-standard in some SQL engines)    |                |
| `NCHAR(n)`        | Fixed-length Unicode string                          |                |
| `NVARCHAR(n)`     | Variable-length Unicode string                       |                |
| `NTEXT`           | Deprecated in some systems (e.g., SQL Server)        |                |

---

## 📅 Date and Time Data Types

| Data Type         | Description                          | Example            |
|-------------------|--------------------------------------|--------------------|
| `DATE`            | Only date (YYYY-MM-DD)               | 2025-07-31         |
| `TIME`            | Only time (HH:MM:SS)                 | 14:25:36           |
| `DATETIME`        | Date and time                        | 2025-07-31 14:25:36|
| `TIMESTAMP`       | Usually stores UTC time; auto-update |                    |
| `YEAR`            | Only year (2-digit or 4-digit)       | 2025               |

---

## 📦 Binary Data Types

| Data Type         | Description                     |
|-------------------|---------------------------------|
| `BINARY(n)`       | Fixed-length binary             |
| `VARBINARY(n)`    | Variable-length binary          |
| `BLOB`            | Binary Large Object             |

---

## ✅ Boolean Data Type

| Data Type | Description                        |
|-----------|------------------------------------|
| `BOOLEAN` | TRUE or FALSE (often 1/0 behind)   |

---

## 🧪 Example Table

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    birth_date DATE,
    salary DECIMAL(10,2),
    is_active BOOLEAN
);
```

---

## 🔍 Notes
- SQL data types vary slightly by database system (e.g., MySQL, PostgreSQL, SQL Server, Oracle).
- Always use `VARCHAR` instead of `CHAR` unless you need fixed-length data.

# Extras
# SQL Data Types Comparison Across DBMSs

This document compares SQL data types across major database management systems: **MySQL**, **PostgreSQL**, **SQL Server**, and **Oracle**.

---

## 🧮 Numeric Data Types

| SQL Standard  | MySQL           | PostgreSQL            | SQL Server           | Oracle               |
|---------------|------------------|------------------------|------------------------|----------------------|
| `INT`         | `INT`, `INTEGER` | `INTEGER`, `INT`       | `INT`, `INTEGER`       | `NUMBER(p,0)`        |
| `SMALLINT`    | `SMALLINT`       | `SMALLINT`             | `SMALLINT`             | `NUMBER(5,0)`        |
| `BIGINT`      | `BIGINT`         | `BIGINT`               | `BIGINT`               | `NUMBER(19,0)`       |
| `DECIMAL(p,s)`| `DECIMAL`, `NUMERIC` | Same             | `DECIMAL`, `NUMERIC`   | `NUMBER(p,s)`        |
| `FLOAT`       | `FLOAT`, `DOUBLE`| `FLOAT`, `DOUBLE PRECISION` | `FLOAT(n)`         | `BINARY_FLOAT`       |
| `REAL`        | `REAL`           | `REAL`                 | `REAL`                 | `BINARY_DOUBLE`      |

---

## 🔤 String Data Types

| SQL Standard  | MySQL             | PostgreSQL             | SQL Server             | Oracle                |
|---------------|-------------------|-------------------------|-------------------------|------------------------|
| `CHAR(n)`     | `CHAR(n)`         | `CHAR(n)`               | `CHAR(n)`               | `CHAR(n)`              |
| `VARCHAR(n)`  | `VARCHAR(n)`      | `VARCHAR(n)`            | `VARCHAR(n)`            | `VARCHAR2(n)`          |
| `TEXT`        | `TEXT`, `TINYTEXT`, etc. | `TEXT`           | `TEXT`, `VARCHAR(MAX)`  | `CLOB`                 |
| `NCHAR(n)`    | `NCHAR(n)`        | `NCHAR(n)`              | `NCHAR(n)`              | `NCHAR(n)`             |
| `NVARCHAR(n)` | `NVARCHAR(n)`     | `VARCHAR(n)` with UTF8  | `NVARCHAR(n)`           | `NVARCHAR2(n)`         |

---

## 📅 Date and Time Data Types

| SQL Standard  | MySQL           | PostgreSQL              | SQL Server             | Oracle                 |
|---------------|------------------|--------------------------|--------------------------|--------------------------|
| `DATE`        | `DATE`           | `DATE`                   | `DATE`                   | `DATE` (includes time)  |
| `TIME`        | `TIME`           | `TIME [WITHOUT TZ]`      | `TIME`                   | `DATE` with format      |
| `DATETIME`    | `DATETIME`       | `TIMESTAMP`              | `DATETIME`               | `DATE` or `TIMESTAMP`   |
| `TIMESTAMP`   | `TIMESTAMP`      | `TIMESTAMP [WITH TZ]`    | `DATETIME2`, `TIMESTAMP`| `TIMESTAMP`             |
| `YEAR`        | `YEAR(4)`        | Not directly supported   | Use `SMALLINT`           | Use `NUMBER(4)`         |

---

## 📦 Binary / Large Object Data Types

| SQL Standard | MySQL              | PostgreSQL        | SQL Server           | Oracle            |
|--------------|--------------------|-------------------|-----------------------|--------------------|
| `BLOB`       | `TINYBLOB`, `BLOB` | `BYTEA`           | `VARBINARY(MAX)`      | `BLOB`             |
| `VARBINARY`  | `VARBINARY(n)`     | `BYTEA`           | `VARBINARY(n)`        | `RAW(n)`           |
| `CLOB`       | `TEXT`             | `TEXT`            | `VARCHAR(MAX)`, `TEXT`| `CLOB`             |

---

## ✅ Boolean Data Type

| SQL Standard | MySQL             | PostgreSQL       | SQL Server     | Oracle             |
|--------------|------------------|------------------|----------------|---------------------|
| `BOOLEAN`    | `TINYINT(1)` (0/1)| `BOOLEAN`        | `BIT` (0 or 1) | `NUMBER(1)` (0 or 1)|

---

## 🚀 Auto-Increment/Identity

| Feature             | MySQL            | PostgreSQL         | SQL Server         | Oracle                        |
|---------------------|------------------|---------------------|---------------------|-------------------------------|
| Auto-Increment ID   | `AUTO_INCREMENT` | `SERIAL`, `BIGSERIAL` | `IDENTITY`       | `SEQUENCE` + `TRIGGER`        |

---

## ✅ Summary Table

| Feature         | MySQL        | PostgreSQL     | SQL Server     | Oracle         |
|-----------------|--------------|----------------|----------------|----------------|
| Rich Text       | TEXT types   | TEXT types     | TEXT, VARCHAR(MAX) | CLOB       |
| Unicode Support | NVARCHAR     | Full UTF-8     | NVARCHAR       | NCHAR/NVARCHAR2|
| Boolean Support | Emulated     | Native         | BIT (0/1)      | Emulated       |
| Auto-Increment  | AUTO_INCREMENT | SERIAL       | IDENTITY       | SEQUENCE       |
| Rich Date Types | Moderate     | Very rich      | Rich           | Very rich      |

---

> 💡 SQL data type names and behaviors may vary slightly depending on the exact version and configuration of your DBMS.

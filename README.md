# 🗄️ SQL Basics

> A concise reference guide covering the foundational SQL commands every developer should know.

---

## 📋 Table of Contents

- [SELECT](#-select)
- [Filtering with WHERE](#-filtering-with-where)
- [Aggregations](#-aggregations)
- [Combining It All](#-combining-it-all)
- [Quick Reference](#-quick-reference)

---

## 🔍 SELECT

The `SELECT` statement retrieves data from one or more tables.

### Syntax

```sql
SELECT column1, column2
FROM table_name;
```

### Examples

**Select all columns:**

```sql
SELECT *
FROM employees;
```

**Select specific columns:**

```sql
SELECT first_name, last_name, salary
FROM employees;
```

**Select with an alias:**

```sql
SELECT first_name AS "First Name", salary AS "Annual Salary"
FROM employees;
```

**Select distinct values (no duplicates):**

```sql
SELECT DISTINCT department
FROM employees;
```

---

## 🔎 Filtering with WHERE

The `WHERE` clause filters rows based on a condition.

### Syntax

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

### Comparison Operators

| Operator | Meaning               | Example                        |
|----------|-----------------------|--------------------------------|
| `=`      | Equal to              | `WHERE salary = 50000`         |
| `!=` / `<>` | Not equal to       | `WHERE department != 'HR'`     |
| `>`      | Greater than          | `WHERE salary > 60000`         |
| `<`      | Less than             | `WHERE age < 30`               |
| `>=`     | Greater than or equal | `WHERE salary >= 50000`        |
| `<=`     | Less than or equal    | `WHERE age <= 40`              |

### Logical Operators

**AND — both conditions must be true:**

```sql
SELECT *
FROM employees
WHERE department = 'Engineering'
  AND salary > 70000;
```

**OR — at least one condition must be true:**

```sql
SELECT *
FROM employees
WHERE department = 'Sales'
   OR department = 'Marketing';
```

**NOT — negates a condition:**

```sql
SELECT *
FROM employees
WHERE NOT department = 'HR';
```

### Special Filtering Keywords

**BETWEEN — within a range (inclusive):**

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 80000;
```

**IN — matches any value in a list:**

```sql
SELECT *
FROM employees
WHERE department IN ('Sales', 'Marketing', 'Engineering');
```

**LIKE — pattern matching:**

```sql
-- Names starting with 'A'
SELECT * FROM employees WHERE first_name LIKE 'A%';

-- Names ending in 'son'
SELECT * FROM employees WHERE last_name LIKE '%son';

-- Names with exactly 5 characters
SELECT * FROM employees WHERE first_name LIKE '_____';
```

> `%` matches any number of characters. `_` matches exactly one character.

**IS NULL / IS NOT NULL — check for missing values:**

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

---

## 📊 Aggregations

Aggregate functions perform calculations across a set of rows and return a single value.

### Common Aggregate Functions

| Function  | Description                           |
|-----------|---------------------------------------|
| `COUNT()` | Counts the number of rows             |
| `SUM()`   | Adds up numeric values                |
| `AVG()`   | Returns the average of numeric values |
| `MIN()`   | Returns the smallest value            |
| `MAX()`   | Returns the largest value             |

### Examples

```sql
-- Total number of employees
SELECT COUNT(*) AS total_employees
FROM employees;

-- Total salary payroll
SELECT SUM(salary) AS total_payroll
FROM employees;

-- Average salary
SELECT AVG(salary) AS avg_salary
FROM employees;

-- Highest and lowest salaries
SELECT MAX(salary) AS highest_salary,
       MIN(salary) AS lowest_salary
FROM employees;
```

### GROUP BY

`GROUP BY` groups rows that share a value so aggregates apply per group.

```sql
SELECT department, COUNT(*) AS headcount, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

### HAVING

`HAVING` filters groups after aggregation (like `WHERE`, but for grouped results).

```sql
-- Only departments with more than 10 employees
SELECT department, COUNT(*) AS headcount
FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```

> 💡 **WHERE vs HAVING**: Use `WHERE` to filter individual rows *before* grouping. Use `HAVING` to filter groups *after* aggregation.

---

## 🔗 Combining It All

A typical query uses all three concepts together. SQL evaluates clauses in this order:

```
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
```

### Full Example

```sql
SELECT   department,
         COUNT(*)       AS headcount,
         AVG(salary)    AS avg_salary,
         MAX(salary)    AS top_salary
FROM     employees
WHERE    hire_date >= '2020-01-01'       -- filter rows first
GROUP BY department                       -- then group
HAVING   AVG(salary) > 60000             -- then filter groups
ORDER BY avg_salary DESC;                -- finally, sort results
```

---

## 📌 Quick Reference

```sql
-- Basic SELECT
SELECT col1, col2 FROM table;

-- Filter rows
SELECT * FROM table WHERE condition;

-- Common filters
WHERE col = 'value'
WHERE col BETWEEN 10 AND 50
WHERE col IN ('a', 'b', 'c')
WHERE col LIKE 'A%'
WHERE col IS NULL

-- Aggregations
SELECT COUNT(*), SUM(col), AVG(col), MIN(col), MAX(col) FROM table;

-- Group & filter groups
SELECT col, COUNT(*) FROM table
GROUP BY col
HAVING COUNT(*) > 5;
```

---

## 📚 Further Reading

- [SQL Tutorial – W3Schools](https://www.w3schools.com/sql/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQLZoo – Interactive Practice](https://sqlzoo.net/)

---

*Made with ❤️ for anyone learning SQL from scratch.*

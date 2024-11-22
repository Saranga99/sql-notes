### **Detailed Explanation of `UNION` in SQL**

#### **What is `UNION`?**
The `UNION` operator is used in SQL to combine the results of two or more `SELECT` statements. It removes duplicate rows by default and ensures the final result includes only unique records.

#### **Syntax:**
```sql
SELECT column1, column2, ...
FROM table1
WHERE condition
UNION
SELECT column1, column2, ...
FROM table2
WHERE condition;
```

#### **Key Points:**
1. **Column Matching:**
   - The number of columns in all `SELECT` statements must be the same.
   - The columns must also have compatible data types (e.g., integers with integers, strings with strings).

2. **Default Behavior:**
   - Removes duplicate rows automatically. If you want to keep duplicates, use `UNION ALL`.

3. **Ordering Results:**
   - To sort the combined results, use `ORDER BY` at the end of the last `SELECT` statement.

---

#### **Examples:**

##### 1. **Basic `UNION`:**
Combine data from two tables:
```sql
SELECT name, department FROM Employees
WHERE department = 'IT'
UNION
SELECT name, department FROM Contractors
WHERE department = 'IT';
```

- **Output:** A list of unique names and departments from both employees and contractors in the IT department.

---

##### 2. **Using `UNION ALL`:**
Keep duplicates in the result set:
```sql
SELECT name, department FROM Employees
WHERE department = 'IT'
UNION ALL
SELECT name, department FROM Contractors
WHERE department = 'IT';
```

- **Output:** Includes duplicates if the same name exists in both tables.

---

##### 3. **Sorting with `UNION`:**
Sort the combined results:
```sql
SELECT name, department FROM Employees
WHERE department = 'IT'
UNION
SELECT name, department FROM Contractors
WHERE department = 'IT'
ORDER BY name ASC;
```

- **Output:** Combined and sorted list of names.

---

#### **When to Use `UNION`:**

1. **Merge Results from Similar Tables:**
   Use `UNION` when you want a unified view of similar data from different tables.

2. **Avoid Duplicates:**
   If duplicates in the results are not allowed, use the default `UNION`.

3. **Retain Duplicates for Analysis:**
   Use `UNION ALL` if duplicate records are meaningful and need to be preserved.

---

#### **Practical Use Case:**
Combine lists of full-time and part-time employees to get a unified employee list:
```sql
SELECT employee_id, name FROM FullTimeEmployees
UNION
SELECT employee_id, name FROM PartTimeEmployees;
```

- This ensures the final list contains unique employee IDs and names.

---

#### **Limitations of `UNION`:**
1. Performance can be slower for large datasets because `UNION` performs an additional step to remove duplicates.
2. Columns must be of compatible data types.

---

#### **`UNION` vs. `JOIN`:**
- **`UNION`:** Combines rows vertically (results from different tables).
- **`JOIN`:** Combines rows horizontally (matches records based on relationships).

Example of their difference:
- `UNION`:
  - Table A: {1, 2}, Table B: {3, 4} → Result: {1, 2, 3, 4}.
- `JOIN`:
  - Table A: {1, 2}, Table B: {1, 3} → Result depends on matching criteria.

---

### **Advanced Example: Full Outer Join with `UNION`:**
MySQL does not support `FULL OUTER JOIN` directly. You can use `UNION` to achieve similar functionality:
```sql
SELECT a.id, a.name, b.salary
FROM TableA a
LEFT JOIN TableB b ON a.id = b.id
UNION
SELECT a.id, a.name, b.salary
FROM TableA a
RIGHT JOIN TableB b ON a.id = b.id;
```
- **Result:** Combines both unmatched rows from `LEFT JOIN` and `RIGHT JOIN`.



### Simplified Notes on SQL (Lectures 5–7)

#### Lecture 05: **Simple SQL Queries**
1. **Database Management System (DBMS):** 
   - Tools to define (DDL), manipulate (DML), and control (DCL) databases.
   - Examples: MySQL, Oracle.

2. **CRUD Operations:**
   - Create, Read, Update, Delete records in database tables.

3. **Basic SQL Commands:**
   - Create Tables: `CREATE TABLE tableName (...)`.
   - Insert Data: `INSERT INTO tableName VALUES (...)`.
   - Select Data: `SELECT columns FROM tableName;`.
   - Conditional Retrieval: Use `WHERE` with comparison operators like `=`, `>`, and logical operators `AND`, `OR`.

4. **Sorting Data:**
   - Use `ORDER BY` to sort (default: ascending).
   - Descending: `ORDER BY column DESC`.

5. **Aliases and Functions:**
   - Rename columns: `AS "AliasName"`.
   - Combine columns: `CONCAT(column1, ' ', column2)`.

6. **Handling NULL Values:**
   - Check for null: `column IS NULL`.

7. **Eliminating Duplicates:**
   - Use `DISTINCT` in `SELECT`.

#### Lecture 06: **Join Queries**
1. **Joins Overview:**
   - Combine data from multiple tables using relationships.

2. **Types of Joins:**
   - **Inner Join:** Match records in both tables:  
     `SELECT columns FROM Table1 JOIN Table2 ON condition;`.
   - **Left Join:** Include all records from the left table. 
   - **Right Join:** Include all records from the right table.
   - **Full Join:** Include all records from both tables (not supported in MySQL, emulate with `UNION`).

3. **Self-Joins:**
   - Use when a table relates to itself.
   - Example: Find employees and their managers:  
     ```sql
     SELECT A.name, B.name FROM Emp A JOIN Emp B ON A.mgrId = B.empId;
     ```

4. **Three-Way Joins:**
   - Combine data from three tables.
   - Example: Retrieve data across Dept, Emp, and Device tables using:  
     ```sql
     SELECT Dept.name, Emp.name, Device.model FROM Dept 
     JOIN Emp ON Dept.id = Emp.deptId 
     JOIN Device ON Emp.id = Device.empId;
     ```

#### Lecture 07: **Complex Queries**
1. **Group Functions:**
   - Perform operations on groups of data.
   - Examples:
     - Minimum: `MIN(column)`
     - Maximum: `MAX(column)`
     - Average: `AVG(column)`
     - Total: `SUM(column)`
     - Count: `COUNT(column)`

2. **Grouping Data:**
   - Use `GROUP BY` to group rows.
   - Example:  
     ```sql
     SELECT deptNo, AVG(salary) FROM Emp GROUP BY deptNo;
     ```

3. **Restricting Group Results:**
   - Use `HAVING` to filter grouped data.
   - Example:  
     ```sql
     SELECT deptNo, AVG(salary) FROM Emp GROUP BY deptNo HAVING AVG(salary) > 5000;
     ```

4. **Subqueries:**
   - A query inside another query.
   - Single-row subqueries: Return one row.
   - Multiple-row subqueries: Use operators like `ANY`, `ALL`.
   - Example: Find employees earning more than the average salary:  
     ```sql
     SELECT name FROM Emp WHERE salary > (SELECT AVG(salary) FROM Emp);
     ```

5. **Combining Data from Multiple Queries:**
   - Use `UNION` to combine results from multiple queries.
